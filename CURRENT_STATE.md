# Poker GTO Intelligence — Current State

> **默认恢复入口。** 当用户说“查看当前进度 / 继续项目 / 教我下一阶段”时，优先读取本文件；随后读取 `docs/TEACHING_SOP.md` 恢复教学方式。需要环境、Solver 参数、模型字段、架构或 Bug 信息时，再通过 `REFERENCE_INDEX.md` 进入对应 Source of Truth。

更新时间：2026-08-09

状态：`● 已完成/已验证` · `◐ 当前进行/已讲解待验证` · `○ 未开始`

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

正式编程教学只使用 Python，不再引入第二门编程语言辅助解释。

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
| `create_deck()` 调用 `create_card()` | ● 2026-08-08 用户实际运行确认 |
| Card Engine v1：完整 52 张 + 函数组合 | ◐ 已讲解，尚未单独确认实际运行 |
| `create_combo(card1, card2)`：两张 Card 组成 Combo | ◐ 用户已确认理解，尚未实际运行验证 |
| **从 Deck 生成不重复 Combo** | ◐ 当前 |
| Range 数据结构 | ○ |

## 3. 已实际验证的函数组合

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

## 4. 当前 Card / Combo 结构

当前 Card Engine v1 目标：

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

Combo 最小结构已经讲解且用户确认理解：

```python
def create_combo(card1, card2):
    return [card1, card2]
```

结构：

```text
Card = 一张牌
Combo = 两张 Card 组成的一手具体手牌
```

当前不把“理解”误记成“实际运行验证”。

## 5. 当前教学 SOP

完整教学执行规范统一读取：

`docs/TEACHING_SOP.md`

当前最重要规则：

```text
只用 Python
↓
正式 Python
↓
最小核心 Python
↓
功能名字 / 输入 / 处理 / 输出
↓
人话动作流程（需要时）
↓
树 / 箭头 / 盒子 / 表格（需要时）
↓
真实数据跑一轮
↓
逐层补回
↓
回到真实 Poker AI 项目
```

如果某行不能再删，要明确说：

> **这一行是核心，不能再砍了。**

一次只增加一个主要新概念。

## 6. 当前视觉与理解规则

固定语义角色：

```text
功能 / 函数名字
输入 / 参数
处理 / 表达式
输出 / 返回结果
循环 / 条件 / 控制结构
数据容器 / 局部变量 / 状态
```

可按需要使用：

```text
箭头 → 数据流
树 → 嵌套 / 归属
盒子 → 变量 / 容器
表格 → 组合
流水线 → 处理步骤
时间轴 → 循环逐轮执行
压缩 ↔ 展开
正向 ↔ 逆向追踪
```

## 7. 当前命名教学规则

Python 提供 / 规定的名字要说明来源，例如：

```text
def / return / for / in
→ Python 关键字

print / len / range
→ Python 内置函数

append
→ list 自带方法

card / combo / deck / i / j
→ 程序员自己起的名字
```

重点帮用户判断：

> **这个必须这么写吗？这个名字能不能换？**

## 8. 当前课程：从 Deck 生成不重复 Combo

当前只增加一个主要概念：**用索引位置控制两张牌的配对，避免同一张牌配自己，也避免 As+Kh 与 Kh+As 重复出现。**

先用小数据理解：

```python
cards = ["As", "Ah", "Ks", "Kh"]

for i in range(len(cards)):
    for j in range(i + 1, len(cards)):
        print(cards[i], cards[j])
```

预期得到 6 个不重复组合：

```text
As Ah
As Ks
As Kh
Ah Ks
Ah Kh
Ks Kh
```

理解后再接入真实 `create_deck()` 和 `create_combo()`，生成完整 52 张牌的 1326 个 Combo。

## 9. 下一步路线

```text
先理解小型 4 张牌为什么只产生 6 个不重复 Combo
↓
把索引循环接入 create_combo
↓
扩到 52 张牌
↓
实际确认 Combo 数量 = 1326
↓
进入 Range 数据结构
```

不要为了学习语法而偏离这条路线。

## 10. 更新规则

每完成一个明确验证的小步骤，优先更新本文件。

- 教学执行规则变化 → `docs/TEACHING_SOP.md`
- 高层教学哲学 / 最终路线变化 → `docs/LEARNING_METHOD.md`
- 环境、Solver、模型字段、Bug 等长期事实 → 按 `REFERENCE_INDEX.md` 更新对应 Source of Truth

最后检查：

> **今天学会的东西，怎样让我们更接近用 Python 做出一个类似 Solver 的 Poker GTO 智能系统？**
