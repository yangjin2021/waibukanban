# Poker GTO Intelligence — Current State

> **默认恢复入口。** 当用户说“查看当前进度 / 继续项目 / 教我下一阶段”时，优先只读取本文件。除非问题需要更详细参数，否则不要默认加载整个仓库。

更新时间：2026-08-08

状态：`● 已完成/已验证` · `◐ 当前进行/已讲解待验证` · `○ 未开始`

## 1. 大地图进度

| Phase | 模块 | 状态 |
|---:|---|:---:|
| 00 | 零基础地基 / 开发环境 | ● 基本完成，终端按需复习 |
| 01 | Python 入门 | ◐ 当前 |
| 02 | 扑克牌表示 | ○ |
| 03 | Combo Engine（1326） | ○ |
| 04 | Range Engine | ○ |
| 05 | Solver 数据读取 | ○ |
| 06 | GTO Dataset | ○ |
| 07 | 第一次机器学习 | ○ |
| 08 | 神经网络 / PokerAI 0.1 | ○ |
| 09 | Policy Model | ○ |
| 10 | Value / EV Model | ○ |
| 11 | Range Intelligence | ○ |
| 12 | 未见 Flop 泛化 | ○ |
| 13 | Turn / River 多街 | ○ |
| 14 | Solver 级验证 | ○ |
| 15 | 多 Range / 多配置 | ○ |
| 16 | 多 Stack / 多位置 | ○ |
| 17 | 高级 AI（按需） | ○ |
| 18 | CFR / 博弈论深入 | ○ |
| 19 | Fast GTO Engine | ○ |

当前阶段：**Phase 01 Python 入门**，继续用 Poker Card / Deck 作为学习载体。

## 2. 小地图进度

| 当前任务 | 状态 |
|---|:---:|
| Python / 本地项目目录建立 | ● |
| `src/main.py` 创建并运行 | ● |
| 变量、字符串、`print()` | ● |
| 字符串索引：`card[0] / card[1]` | ● |
| `Kh → Rank / Suit` | ● |
| `list` 保存多张牌 | ● |
| `for` 循环逐张处理 | ● |
| 嵌套 `for`：Rank × Suit | ● |
| 生成并打印完整 52 张 Deck | ● |
| `len()` 检查数量 | ● |
| `set()` 检查重复牌 | ● |
| `def create_deck()` | ● |
| `return deck` | ● PyCharm 已验证 |
| 函数参数 `rank, suit` | ● 已理解 |
| `def card(rank, suit): return rank + suit` 最小函数骨架 | ● 已理解 |
| 循环中调用 `card(rank, suit)` | ● PyCharm 已验证（2×2 输出 As/Ah/Ks/Kh） |
| 两层 `for` 的二维组合 / 笛卡尔积直觉 | ● 已理解 |
| `create_deck()` 无参数 → 返回整副牌 | ◐ 当前知识点，最小版已讲解待验证 |
| Card Engine 结构化 | ○ |

当前 Sprint 目标：把已经掌握的“单张牌函数 + 循环组合 + deck 列表”重新组合成一个清晰的 `create_deck()` 函数，建立稳定的“输入 → 处理 → 输出”代码骨架感。

## 3. 当前开发方式

- 项目目录：`C:\PokerGTOAI`
- Python 代码：`C:\PokerGTOAI\src\main.py`
- **当前默认 IDE：PyCharm**
- 默认教学流程：在 PyCharm 编辑 → Run → 看实际输出 → 再推进。
- PowerShell 只在路径、Git、环境排查或命令行任务时使用。
- 如果新开终端需要回项目：`cd C:\PokerGTOAI`

## 4. 最近明确验证的运行结果

### A. `create_deck()` + `return deck`

已在 PyCharm 验证：

```text
第一张牌: As
最后一张牌: 2c
牌的数量: 52

Process finished with exit code 0
```

### B. 循环中调用函数

核心代码：

```python
def card(rank, suit):
    return rank + suit

ranks = ["A", "K"]
suits = ["s", "h"]

for rank in ranks:
    for suit in suits:
        print(card(rank, suit))
```

用户已贴出 PyCharm 实际输出：

```text
As
Ah
Ks
Kh

Process finished with exit code 0
```

这证明用户已经实际跑通：

- 函数参数作为输入
- `return` 作为输出
- 函数调用
- 外层 / 内层 `for`
- 循环变量每轮重新绑定当前值
- 循环中调用函数
- `2 × 2` 组合生成四个结果

## 5. 当前知识点

当前正在学习：**把整副 Deck 重新封装成一个无参数函数**。

当前最小核心：

```python
def create_deck():
    return ["As", "Ah"]
```

只理解：

```text
create_deck = 功能名字
()          = 不需要输入
return      = 把结果交出去
```

该最小版目前已讲解，但用户还没有贴出运行结果，因此保持 `◐`，不要误写为已验证。

下一层才逐步补回：

```text
空 deck
→ 循环制造牌
→ append 放入 deck
→ return deck
```

不要直接一次跳回完整 52 张版本。

## 6. 当前教学约定

- 每次教学回复默认**只显示小地图表格**；用户主动要求时才显示大地图。
- **真正可运行的 Python 代码放在最上面，保持干净。**
- 代码下面再放：运行结果 → 人话伪代码 / 执行流程 → PyCharm 颜色或灰色提示解释 → 为什么这样写。
- 不再默认把大量教学注释塞进正式 Python 代码里；必要时只保留极少数关键注释。
- 遇到不懂的代码，必须先尝试压缩到**不能再压的最小核心**；如果某行不能删，要明确说明“这一行是核心，不能再砍了”。
- 默认按：**最小核心 → 看懂骨架 → 只增加一层 → 再增加一层 → 回到完整项目代码**。
- 优先帮助识别：`功能名字 / 输入 / 处理 / 输出`。
- 高频使用自然中文伪代码解释数据流，例如“拿出来 / 交进去 / 做成 / 放进盒子 / return 交回来”。
- 可以结合 PyCharm 语法高亮解释代码角色；必须区分“真正代码”和 PyCharm 的灰色 Inlay Hints / usages 提示。
- 可以在合适时用 Lisp / S-expression 作为结构透视图，帮助理解函数、绑定、循环和数据流；Python 仍是 Poker GTO AI 项目的主语言。
- 一次只推进一个主要新概念；用户说“懂了 / 继续 / 下一课”再增加复杂度。
- 可以偶尔用 1～2 个短问题抽查已经讲过的概念，不出陷阱题。

## 更新规则

每完成一个可验证的小步骤，优先更新本文件。只有涉及详细阶段规划、环境、Bug、模型或技术规范时，再同步更新对应详细文档。
