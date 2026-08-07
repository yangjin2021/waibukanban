# Poker GTO Intelligence — 输入 / 输出规范

本文档记录当前已经确认的核心接口思想。后续模型、API、UI 都应尽量围绕这一规范演进。

## 1. 一句话定义

Poker GTO Intelligence 的本质是：

```text
一组牌局状态参数 x
        ↓
   神经网络 AI(x)
        ↓
一组我们需要的 GTO 参数 y
```

我们真正训练的是中间的 **神经网络及其内部参数（Parameters）**。

训练阶段利用 Solver 给出的 `(输入状态 x, 正确答案 y)` 调整网络参数；推理阶段只需要把新的状态送入已经训练好的网络，经过一次前向计算即可快速得到结果。

---

## 2. 最终输入 State

长期目标下，一个完整状态应能包含：

- Street：Preflop / Flop / Turn / River
- Board
- Acting Player
- Position
- Effective Stack
- Pot
- IP Range：1326 Combo 权重
- OOP Range：1326 Combo 权重
- Action History
- Legal Actions
- Bet / Raise Size
- Blocker / Valid Combo Mask

第一代模型不会一次实现全部输入，而是从最小问题逐步扩展。

### PokerAI 0.1 最小输入

```text
Flop Board
+
Hero Combo
```

在固定 150BB、BTN vs BB、固定 Range、固定下注树的前提下先验证模型是否能学习 Solver。

---

## 3. 神经网络内部

可以把模型暂时理解成：

```text
数字化输入
  ↓
矩阵运算 + 非线性变换
  ↓
隐藏表示
  ↓
更多矩阵运算
  ↓
策略 / EV 输出
```

训练的核心不是“保存每一张 Solver 答案表”，而是调整这些矩阵中的大量参数，使模型学会从牌局状态映射到接近 Solver 的结果。

---

## 4. 最底层原始输出

长期版本优先保留最细的 Combo 级结果。

### 4.1 Combo × Action Policy Matrix

例如某节点允许：

- Check
- Bet 33%
- Bet 66%
- Bet 100%

则输出可以表示为：

| Combo | Check | B33 | B66 | B100 |
|---|---:|---:|---:|---:|
| AsKh | 12% | 61% | 19% | 8% |
| AsKd | 15% | 59% | 18% | 8% |
| AhKs | 8% | 65% | 21% | 6% |

同一 Combo 的合法动作概率之和应为 100%。

### 4.2 Action EV

长期希望同时输出每个 Combo 在每个动作下的 EV，例如：

| Combo | Check EV | B33 EV | B66 EV | B100 EV |
|---|---:|---:|---:|---:|
| AsKh | 6.31 | 6.37 | 6.35 | 6.29 |

### 4.3 Range Weight

`Range Weight` 回答的是：

> 这个具体 Combo 在当前节点的 Range 中还保留多少权重？

它和动作频率不是同一个概念。

例如：

```text
AhKs
Range Weight = 74%
B33 Strategy = 40%
```

表示该 Combo 当前有 74% 的 Range 权重，而这 74% 中有 40% 在当前节点选择 B33。

### 4.4 Valid / Blocker Mask

内部长期保留固定 1326 Combo 槽位。

若 Board 已经占用某张牌，则冲突 Combo 标记为：

```text
valid = false
mask = 0
```

这样 Preflop / Flop / Turn / River 可以尽量使用统一数据结构。

---

## 5. 一次输出整个 Range

最终目标不是逐手调用 1326 次，而是一次输入完整 State 后，批量得到当前玩家所有合法 Combo 的结果：

```text
State
  ↓
GTO Model
  ↓
1326 Combo × Legal Actions
+
EV
+
Range Weight
+
Mask
```

这是未来对接其他项目的核心能力。

---

## 6. 给人看的输出形式

模型只负责产生底层结构化数据；UI 只是同一份数据的不同视图。

### 6.1 第一层：总体策略频率

例如：

```text
Check       24.6%
Bet 33%     48.3%
Bet 66%     15.7%
Bet 100%    11.4%
```

这是整个当前 Range 的加权行动频率。

### 6.2 第二层：13×13 Range 主视图

169 格用于人类快速观察整体范围；每格通过颜色 / 面积表现混合策略。

原则：

> 169 格负责看，Combo 负责算。

### 6.3 第三层：Combo 明细表

点击 `AKo` 等 169 格后，可展开具体花色 Combo：

| Combo | Range Weight | X | B33 | B66 | B100 | EV |
|---|---:|---:|---:|---:|---:|---:|
| AsKh | 100% | 12% | 61% | 19% | 8% | 6.37 |
| AsKd | 100% | 15% | 59% | 18% | 8% | 6.32 |
| AhKs | 74% | 8% | 65% | 21% | 6% | 6.41 |

### 6.4 第四层：单 Combo 详情

可显示：

- Range Weight
- Strategy
- 每个 Action 的 EV
- 后续可扩展 Equity / Blocker 属性等

### 6.5 Board / Frequency Analysis

同一份底层 Combo 数据还可以汇总成：

- 单牌面总体频率表
- 对子牌面频率表
- 单色牌面频率表
- A 高干燥 / 高张动态 / 中低动态等牌面类别统计
- 不同 Bet Size 的范围构成

这些是统计 / 展示层，不需要重新训练一套模型。

---

## 7. Range Propagation

当实际选择一个动作时，Range 可以沿博弈树传播。

对于某 Combo：

```text
新权重 = 当前 Range Weight × 当前动作概率
```

再根据需要归一化或保留 reach 权重。

因此系统可以形成：

```text
State₀
 ↓
Strategy₀
 ↓
选择 Action
 ↓
Range 更新
 ↓
State₁
 ↓
再次推理
```

最终一路支持 Flop → Turn → River。

---

## 8. 对外 API 思想

最终不让其他项目直接依赖 PyTorch Tensor，而是通过 Poker AI Engine 返回稳定结构化结果。

概念示例：

```json
{
  "board": ["8s", "7h", "7d"],
  "actions": ["check", "bet_0.33", "bet_0.66", "bet_1.00"],
  "combos": {
    "AsKh": {
      "valid": true,
      "range_weight": 1.0,
      "policy": [0.12, 0.61, 0.19, 0.08],
      "action_ev": [6.31, 6.37, 6.35, 6.29]
    }
  }
}
```

UI、桌面程序、训练软件、网站或其他 AI 都只需要认识这个接口即可。

---

## 9. 当前正式理解

- **输入**：牌局状态，被编码成数字。
- **神经网络**：我们真正训练的映射函数。
- **参数**：神经网络学习到的知识载体。
- **输出**：Combo 级 Policy、EV、Range Weight 等结构化结果。
- **13×13、Combo 表、频率表、EV 表**：底层输出的不同展示 / 汇总方式。
- **训练慢，推理快**：训练阶段不断调整参数；最终使用阶段只做一次或少量前向矩阵计算。
