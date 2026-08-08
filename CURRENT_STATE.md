# Poker GTO Intelligence — Current State

> **默认恢复入口。** 当用户说“查看当前进度 / 继续项目 / 教我下一阶段”时，优先读取本文件；随后读取 `docs/TEACHING_SOP.md` 恢复教学方式；涉及双语言教学时，再读取 `docs/PYTHON_LISP_COURSE.md`；进入 AI 架构、模型、训练、搜索、CFR 等内容时，再读取 `docs/AI_LANGUAGE_POSITIONING.md` 恢复 Python / Lisp 的长期分工。

更新时间：2026-08-08

状态：`● 已完成/已验证` · `◐ 当前进行/已讲解待验证` · `○ 未开始`

## 1. 当前总体路线

```text
Python 主线
    ↓
真正开发 Poker GTO Intelligence

Common Lisp 同步副线
    ↓
直接对齐当前 Python 学习进度
    ↓
用已经会的 Python 理解 Lisp
```

**Python 仍是正式项目主语言；Lisp 默认在 GPT 内教学，不接入本地 Poker 项目。**

长期 AI 语言定位见：`docs/AI_LANGUAGE_POSITIONING.md`。

一句话：

```text
Python = 把 AI 真正做出来
Common Lisp = 帮助把 AI 的结构想清楚
```

## 2. 当前 Python 小地图

| 当前任务 | 状态 |
|---|:---:|
| 变量 / 字符串 / print | ● |
| 字符串索引 Rank / Suit | ● |
| list | ● |
| for | ● |
| 两层 for：Rank × Suit | ● |
| deck / append / len / set | ● |
| def / 参数 / return | ● |
| `create_card(rank, suit)` | ● |
| `create_deck()` 内部建立 deck | ● |
| 两层循环生成 Deck | ● |
| 函数内 / 外同名 deck 的作用域区别 | ● |
| **`create_deck()` 调用 `create_card()`** | ◐ 当前，已讲解待实际运行确认 |
| Card Engine 第一版整理 | ○ |

## 3. 当前 Python 代码进度

```python
def create_card(rank, suit):
    return rank + suit


def create_deck():
    ranks = ["A", "K"]
    suits = ["s", "h"]
    deck = []

    for rank in ranks:
        for suit in suits:
            card = create_card(rank, suit)
            deck.append(card)

    return deck


deck = create_deck()
print(deck)
```

预期：

```text
['As', 'Ah', 'Ks', 'Kh']
```

当前知识目标：

```text
create_card
负责一张牌

create_deck
负责一副牌

create_deck
    ↓ 调用
create_card
```

## 4. Lisp 同步进度

Lisp 不从零重新学，而是**直接对齐上面的 Python 整段代码**。

当前完整对齐版本：

```lisp
(defun create-card (rank suit)
  (concatenate 'string rank suit))

(defun create-deck ()
  (let ((ranks '("A" "K"))
        (suits '("s" "h"))
        (deck '()))
    (dolist (rank ranks)
      (dolist (suit suits)
        (let ((card (create-card rank suit)))
          (setf deck (append deck (list card))))))
    deck))

(let ((deck (create-deck)))
  (format t "~S~%" deck))
```

概念输出：

```text
("As" "Ah" "Ks" "Kh")
```

该 Lisp 代码目前用于 GPT 内教学与对照；如果没有真实 Lisp 解释器执行，就不能标记为“已运行验证”。

## 5. 当前教学 SOP

完整教学执行规范统一读取：

`docs/TEACHING_SOP.md`

当前最重要的 SOP 核心：

### 六镜头

```text
① 正式 Python
② 完整 Lisp 对齐版（涉及 Lisp 时）
③ 局部颜色结构对照
④ 人话执行流程
⑤ 树 / 层级 / 结构图
⑥ 真实数据跑一轮
```

卡住时额外使用：

```text
压缩版 ↔ 展开版
正向执行 ↔ 逆向追踪
```

### 固定语义颜色

| 标记 | 角色 |
|---|---|
| 🟦 | 功能 / 函数名字 |
| 🟩 | 输入 / 参数 |
| 🟨 | 处理 / 表达式 |
| 🟥 | 输出 / 返回结果 |
| 🟪 | 循环 / 条件 / 控制结构 |
| 🟧 | 数据容器 / 局部变量 / 状态 |

原则：**同一个结构角色，同一种教学颜色。**

### 视觉化语言

优先按需要使用：

```text
箭头 → 数据流
树 → 嵌套 / 归属
盒子 → 变量 / 容器
表格 → Rank × Suit 组合
流水线 → 处理步骤
时间轴 → 循环逐轮执行
```

### 比喻

按知识点选 1～3 个最适合的比喻，例如：

```text
🏭 工厂 / 流水线
👨‍🍳 厨房 / 菜谱
🚚 快递 / 物流
📦 盒子 / 仓库
🎭 临时工牌
🎰 组合表格
🧩 乐高
🗺️ 地图 / 房间
🧠 数学函数
```

完整选择规则与边界以 `docs/TEACHING_SOP.md` 为准。

## 6. AI 教学语言定位

长期规则统一见：`docs/AI_LANGUAGE_POSITIONING.md`。

默认偏向：

```text
数据 / Solver / NumPy / Pandas / Dataset / Tensor
神经网络 / PyTorch / JAX / Loss / Optimizer / GPU / 部署
→ Python 主讲、正式实现

状态 / Game Tree / Action Tree / Search / 递归
规则 / 符号 / DSL / code-as-data / CFR 结构
→ Lisp 辅助思考，再回 Python 落地

概率 / EV / 向量 / 矩阵 / Softmax / Gradient / Backpropagation
→ 先语言无关解释，再 Python 实现；Lisp 只在能明显帮助结构理解时加入
```

不采用 Python / Lisp 50:50 平均教学，也不为了双语言形式机械翻译 PyTorch / CUDA。

AI 新模块默认先问：

> **这是工程实现问题，还是结构设计问题？**

再决定主要使用哪种语言。

## 7. 双语言教学固定规则

每次涉及 Lisp 时：

```text
① 先看当前 Python 正式代码
② 顺手给与当前 Python 进度完整对齐的 Lisp 全代码
③ 再截取今天真正要学的最小 Python ↔ Lisp 局部核心
④ 用固定语义颜色标记两边对应结构
⑤ 用已经会的 Python 解释 Lisp
⑥ 一次只深入一个主要 Lisp 新概念
⑦ Python 主线继续推进时，Lisp 完整对齐版同步升级
```

核心原则：

> **局部版负责学懂，完整版负责不迷路。**

## 8. Lisp 运行位置

默认：

```text
Python 正式项目 → 现有 Poker 项目 / PyCharm
Lisp 学习实验   → GPT 内
```

不再默认要求：

- `C:\PokerGTOAI\lisp\`
- 本地 SBCL
- PyCharm Lisp 插件

除非用户以后明确要求本地 Lisp 环境。

## 9. 下一步课程

继续从当前 Python 函数组合出发，同时拆 Lisp 对应概念：

```text
Python: create_deck() 调用 create_card()
↓
Lisp: defun / 参数 / 最后表达式返回
↓
Lisp: let / list
↓
Lisp: dolist / 嵌套 dolist
↓
Python Card Engine 第一版
↓
Lisp 完整对齐版同步升级
```

## 10. 当前教学约定

- 默认只显示小地图。
- 正式代码放上面，解释放下面。
- 遇到不懂代码先压到最小核心。
- 优先识别：功能名字 / 输入 / 处理 / 输出。
- 一次只增加一个主要新概念。
- 重要新结构优先使用六镜头。
- 用户卡住时优先增加视觉、比喻、展开或逆向追踪，而不是增加术语。
- Python 提供 / 规定的名字要说明来源。
- 不同作用域同名变量容易混淆时，教学版优先先换不同名字。
- Lisp 直接对齐当前 Python 项目学习进度，不从无关基础重新开始。
- 每次 Lisp 教学同时提供局部核心和完整对齐版。
- Python ↔ Lisp 同角色固定使用同一种语义颜色。
- Python 是 AI 正式工程主战语言；Lisp 是程序设计健身房和 AI 架构草稿纸。
- Solver / Dataset / NumPy / PyTorch / GPU AI 继续以 Python 为主。

## 更新规则

每完成一个明确验证的小步骤，优先更新本文件。

- 教学执行规则变化 → 更新 `docs/TEACHING_SOP.md`
- 双语言课程结构变化 → 更新 `docs/PYTHON_LISP_COURSE.md`
- AI 语言角色 / 教学偏向变化 → 更新 `docs/AI_LANGUAGE_POSITIONING.md`
- 高层教学哲学变化 → 更新 `docs/LEARNING_METHOD.md`
