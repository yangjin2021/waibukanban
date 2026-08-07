# Poker GTO Intelligence 技术宪法

这份文档记录项目中已经确定、以后不应轻易推翻的核心设计原则。

## 1. 最终产品不是运行时 Solver

训练阶段可以使用已有 PioSolver `.cfr` 结果作为老师；使用阶段目标是让神经网络直接推理：

```text
Poker State
    ↓
GTO Neural Model
    ↓
Combo × Action Strategy Matrix
+ Combo EV
+ Range information
```

运行时不要求重新 CFR 迭代或重新 solve。

## 2. 内部始终保持 Combo 级精度

- 统一使用 1326 个 preflop Combo 槽位。
- 公共牌或已知手牌造成的冲突使用 blocker / valid mask 标记。
- 13×13 Range 表只负责展示，不作为内部最高精度表示。

## 3. 一次推理批量输出整个 Range

模型接口长期目标不是“一手牌调用一次”，而是一次输出整个合法 Combo 空间的策略：

```text
[1326 Combos] × [Legal Actions]
```

每个 Combo 至少保留：

- range weight
- action probabilities
- EV
- valid / blocker mask

## 4. Range 必须成为条件输入

长期版本不把 BTN / BB Range 永久写死。

模型输入应逐步支持：

- IP Range `[1326]`
- OOP Range `[1326]`
- Board
- Pot
- Stack
- Position
- Action History
- Legal Actions
- Bet Sizes

目标是学习“状态到策略”的规律，而不是背固定 184 张答案表。

## 5. Solver 配置是输入，不是模型身份

不希望形成：

`150BB → 模型1`、`100BB → 模型2`、`CO vs BB → 模型3`。

长期目标是一个条件模型，让不同 Stack、Position、Range、Pot、下注树通过输入描述。

## 6. Action-Aware 设计

早期教学模型可以固定输出 `Check / B33 / B66 / B100`。

长期版本要尽量把 action 本身编码成数据，使新的下注尺寸不必永久增加一个新的固定输出口。

思路：

```text
State Representation + Action Representation
                ↓
              Score
```

对所有合法 Action 得分后再归一化为策略概率。

## 7. Policy + EV 双输出

模型核心输出至少包括：

- Policy：每个合法动作的混合频率
- EV / Value：Combo 在当前状态下的价值

后续可扩展 Equity、reach probability 等辅助目标。

## 8. AI 大脑与 UI 解耦

核心模型只返回统一数据协议。

外层可以自由连接：

- 13×13 Range Viewer
- Combo 明细表
- 桌面软件
- Web / API
- 训练工具
- 未来自然语言解释层

UI 改变不要求重做 AI 大脑。

## 9. 新 Solver 数据用于持续学习

新增 100BB、其他位置或其他 Range 的 Solver 数据时，优先：

`旧模型 + 新数据 + 代表性旧数据 → 继续训练 → 新模型版本`

通常不要求参数量随着 Solver 数量线性增长。

只有问题复杂度超过模型容量时，才考虑增大模型。

## 10. 防止灾难性遗忘

不能长期只用最新配置继续训练。

至少采用：

- 新数据
- 代表性旧数据 replay / rehearsal

未来再按需要研究更高级 continual learning 方法。

## 11. Solver 是最终裁判

不能用“看起来像”判断模型是否学会 GTO。

评估至少包括：

- Combo Strategy Error
- Range Strategy Error
- EV Error
- Board Category Error
- Bet Size Error

高级阶段加入：

- Best Response
- Exploitability
- 将 AI Strategy 回送 Solver 验证

## 12. 数据切分按整棵 Tree

同一棵 Flop Tree 的节点不能同时被随意拆到 train 和 test，避免信息泄露。

Train / Validation / Test 应优先按整棵 Flop Tree 划分，并让各牌面类别在测试集中有代表。

## 13. 研发策略：Small → Correct → Scale

硬件当前为 RTX 2060 SUPER 8GB / 32GB RAM。

因此：

1. 先 1 棵树跑通数据提取。
2. 再 5 / 20 / 50 / 184 棵逐步扩大。
3. 先 Tiny / Small 模型验证架构。
4. 只有模型容量确实成为瓶颈时才扩大网络或升级硬件。

## 14. 数据工程优先于大模型

已有 Solver 很大，但训练时不把全部数据同时放进内存/显存。

使用流式读取、小 Batch、紧凑数据格式；`.cfr` 原始文件不复制进代码仓库。

## 15. 统一 API 是最终工程边界

长期 Poker AI Engine 的职责：

```text
Input State
  ↓
Neural GTO Model
  ↓
Combo × Action Strategy
Combo EV
Range
  ↓
统一 API
```

所有其他项目只依赖这个 API，而不依赖模型内部实现。
