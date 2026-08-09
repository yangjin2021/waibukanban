# Poker GTO Intelligence — Current State

> **默认恢复入口。** 当用户说“查看当前进度 / 继续项目 / 教我下一阶段”时，优先读取本文件；随后读取 `docs/TEACHING_SOP.md` 恢复教学方式，并读取 `docs/PYTHON_LEARNING_MAP.md` 恢复课程级小地图。需要环境、Solver 参数、模型字段、架构或 Bug 信息时，再通过 `REFERENCE_INDEX.md` 进入对应 Source of Truth。

更新时间：2026-08-09

状态：`● 稳定/已验证` · `◐ 已会但混合场景仍需巩固` · `△ 已见过` · `○ 未开始`

## 1. 永远记住的最终目标

```text
只用 Python 学习和开发
        ↓
逐步建立 Poker 数据、规则、状态、决策与 AI 能力
        ↓
最终做出一个类似 Solver 的 Poker GTO 智能系统
```

Python 不是学习终点，而是把这个系统真正造出来的主工具。

以后每个新知识都尽量连接到：

```text
Card / Combo
→ Range
→ Action / State
→ Solver 数据
→ Dataset
→ Model
→ Game Tree / CFR / Search
→ 推理与决策
→ Solver-like Poker GTO Intelligence
```

正式编程教学只使用 Python。

## 2. 课程架构已经改为“螺旋式 +15%”

完整课程级小地图：

`docs/PYTHON_LEARNING_MAP.md`

以后不再使用“学完一个知识点就永久离开”的直线课程，而使用：

```text
约 85% 已学知识
+
约 15% 新知识
↓
同一课内部继续分层递进
↓
交互测试
↓
Poker Boss
↓
根据答题结果自动调速
```

这里的 85% / 15% 是教学设计目标，不机械按字数计算。

同一课固定尽量按：

```text
Level 1 旧知识复测
↓
Level 2 易混变式
↓
Level 3 本课约 15% 新知识
↓
Level 4 新旧混合
↓
Level 5 Poker Boss
```

当前层明显不稳时，不强行继续加新知识；先 Diagnose → Backfill → Re-test。

## 3. 当前 Python 小地图：以“稳定度”而不是“讲过”判断

最近交互测试说明：用户已经见过并使用过不少后续知识，但 `list / dict / in / 取值后重新判断类型` 在混合代码里还没有完全自动化。因此当前不是整章倒退，而是进行**螺旋式回补**。

| 能力 | 状态 | 当前判断 |
|---|:---:|---|
| 变量 / `=` / `print` | ● | 基础可用 |
| `int` / `str` | ◐ | 单独判断基本会，混合结构仍需复测 |
| `list` | ◐ | 知道概念；取值后最外层判断偶尔出错 |
| 嵌套 list | ◐ | 当前重点之一 |
| `dict` key / value | ◐ | 已会基础，混合取值需强化 |
| `state["key"]` | ◐ | 已会，需继续自动化 |
| `[]` 创建 list vs 取值 | ◐ | 当前重点之一 |
| list 索引 `[0] / [1]` | △/◐ | 最新加入的约 15% 新知识 |
| `in` 当前层规则 | ◐ | 当前明显薄弱点 |
| `==` | ◐ | 已见过；正在强化 False vs Error |
| False vs `TypeError` | △/◐ | 当前新补知识 |
| `.get()` | ◐ | 已会基础，继续和 State / Range 混合 |
| `if / else` | ◐ | 已见过，待数据结构稳定后继续整合 |
| `append()` | ●/◐ | 已实际用于 Deck，后续继续复用 |
| `for` | ●/◐ | 已学过，后续作为 85% 熟悉材料复用 |
| 两层 `for` | ●/◐ | 已学过，后续生成 Deck / Combo 继续复用 |
| `range()` / `len()` | ●/◐ | 已学过，继续在索引课复用 |
| `def` / 参数 / `return` | ●/◐ | 已学过，后续继续函数化 |
| `create_card()` | ● | 已实际运行 |
| `create_deck()` | ● | 小型版本已实际运行 |
| `create_combo()` | ◐ | 已理解，仍需项目化验证 |
| 从 Deck 生成不重复 Combo | ◐ | 原项目主线，待基础层稳定后返回 |
| Range 数据结构 | ◐ | 已开始接触，当前正作为数据结构练习材料 |

## 4. 当前最重要的阅读公式

以后遇到复杂表达式，默认强制按：

```text
先求值
↓
看取出来的完整对象
↓
判断最外层类型
↓
看当前层直接元素
↓
再判断 == / in / + / if 等操作
↓
最后决定 value / True / False / Error
```

当前典型例子：

```python
state = {
    "position": "CO",
    "combo": ["132"]
}

current_range = [
    ["123"],
    ["132"]
]
```

必须能区分：

```text
state["combo"]
→ ["132"]
→ list

"132" in current_range
→ False

["132"] in current_range
→ True
```

以及：

```text
"132" == ["132"]
→ False
→ 不一定报错

"132" + 1
→ TypeError
```

## 5. 已实际验证的函数组合

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

用户实际确认结果：

```text
['As', 'Ah', 'Ks', 'Kh']
```

## 6. Card / Combo 主线仍保留

Card Engine v1：

```python
def create_card(rank, suit):
    return rank + suit


def create_deck():
    ranks = ["A", "K", "Q", "J", "T", "9", "8", "7", "6", "5", "4", "3", "2"]
    suits = ["s", "h", "d", "c"]
    deck = []

    for rank in ranks:
        for suit in suits:
            card = create_card(rank, suit)
            deck.append(card)

    return deck
```

Combo 最小结构：

```python
def create_combo(card1, card2):
    return [card1, card2]
```

原项目路线没有被废弃，只是现在会把当前数据结构基础穿插进去，以 85% 旧知识 + 15% 新知识的方式重新走回：

```text
Card
→ Deck
→ Combo
→ 1326 Combos
→ Range
→ State
→ Action
→ Dataset / Model
```

## 7. 当前教学执行规则

完整教学 SOP：

`docs/TEACHING_SOP.md`

高层教学方法：

`docs/LEARNING_METHOD.md`

课程级螺旋小地图：

`docs/PYTHON_LEARNING_MAP.md`

当前最重要规则：

```text
SHOW CODE
↓
语法颜色 / token / 符号辅助读码
↓
85% 已知结构
↓
15% 新知识
↓
同课层层递进
↓
交互作答
↓
错因诊断
↓
Poker Boss
↓
下一课根据结果自动调速
```

交互式教学是默认方式，不只是考试时使用。

## 8. 当前下一课方向

当前课已经开始加入：

```text
list 索引 [0] / [1]
```

同时继续强化：

```text
取值后重新判断类型
嵌套 list 当前层
in 当前层
False vs TypeError
.get()
```

下一轮如果这些题稳定通过，再新增约 15%：

```text
True / False
!=
not in
.get() 默认值真正触发
```

随后重新整合进：

```text
if / else
→ Range decision
→ Play / Fold
```

再返回原主线：

```text
Deck → 不重复 Combo → 1326 → Range
```

## 9. 当前命名 / 颜色 / 符号教学规则

每课继续辅助判断：

```text
Python 关键字
Python 内置函数
标准类型方法
程序员自己起的变量 / 函数名
字符串 / 数字字面量
[] / () / {} / : / , / . / = / == 等符号在当前上下文中的真实作用
```

代码和交互题尽量使用语法着色；颜色是辅助，token 属性才是真正含义。

## 10. 更新规则

每完成一个明确验证的小步骤，优先更新本文件。

- 当前学到哪里 / 哪个知识是否稳定 → `CURRENT_STATE.md`
- 完整课程顺序 / 85%+15% 小地图 → `docs/PYTHON_LEARNING_MAP.md`
- 教学执行规则变化 → `docs/TEACHING_SOP.md`
- 高层教学哲学 → `docs/LEARNING_METHOD.md`
- 环境、Solver、模型字段、Bug → 按 `REFERENCE_INDEX.md` 更新对应 Source of Truth

最后检查：

> **今天新增的约 15% 知识，怎样建立在旧知识上，又怎样让我们更接近用 Python 做出一个类似 Solver 的 Poker GTO 智能系统？**
