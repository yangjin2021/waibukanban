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

当前阶段：**Phase 01 Python 入门**，已经开始用扑克 Deck 作为学习载体。

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
| 嵌套 `for`：13 Rank × 4 Suit | ● |
| 生成并打印完整 52 张 Deck | ● |
| `len()` 检查数量 | ● 已学会（用户确认） |
| `set()` 检查重复牌 | ● 已学会（用户确认） |
| `def create_deck()` | ◐ 已讲解，未保留运行输出 |
| `return deck` | ◐ 当前知识点，待 PyCharm 验证 |
| 函数参数 | ○ 下一步 |
| Card Engine 结构化 | ○ |

当前 Sprint 目标：把“生成 52 张牌”从脚本式代码逐步整理成可复用函数，并继续理解函数、参数和数据流。

## 3. 当前开发方式

- 项目目录：`C:\PokerGTOAI`
- Python 代码：`C:\PokerGTOAI\src\main.py`
- **当前默认 IDE：PyCharm**
- 默认教学流程优先按 PyCharm 编辑 / Run，不再默认要求用 Notepad + PowerShell 运行。
- PowerShell 保留为辅助工具：路径、Git、环境排查或命令行任务时再使用。
- 如果新开终端需要回项目：`cd C:\PokerGTOAI`

## 4. 最后一次明确验证的代码

用户已在终端明确贴出完整 52 张牌输出，从 `As / Ah / Ad / Ac` 一直到 `2s / 2h / 2d / 2c`。

对应代码：

```python
ranks = ["A", "K", "Q", "J", "T", "9", "8", "7", "6", "5", "4", "3", "2"]
suits = ["s", "h", "d", "c"]

for rank in ranks:
    for suit in suits:
        card = rank + suit
        print(card)
```

这证明用户已经实际掌握 / 使用：

- list
- for
- 嵌套 for
- 字符串拼接
- Rank × Suit 生成 Card

## 5. 当前目标代码（待 PyCharm 验证）

```python
# 定义一个“生成整副牌”的功能
def create_deck():

    # 准备所有 Rank 和 Suit
    ranks = ["A", "K", "Q", "J", "T", "9", "8", "7", "6", "5", "4", "3", "2"]
    suits = ["s", "h", "d", "c"]

    # 准备空列表，用来收集生成的牌
    deck = []

    # 每个 Rank 都和 4 个 Suit 组合
    for rank in ranks:
        for suit in suits:
            card = rank + suit
            deck.append(card)

    # 把生成好的整副牌交回函数外面
    return deck


# 调用函数，并接住 return 回来的结果
deck = create_deck()

# 正常打印结果；注释不会出现在输出里
print("牌的数量:", len(deck))
print("不重复牌的数量:", len(set(deck)))
```

目标输出：

```text
牌的数量: 52
不重复牌的数量: 52
```

> 注意：“明确验证”与“已讲解 / 用户口头确认学会”继续分开记录，避免把没有运行证据的代码误写成已验证。

## 6. 当前教学约定

- 每次教学回复**只显示小地图表格**；除非用户主动要求，不重复显示大地图。
- 伪代码逻辑与正式 Python 代码**放在同一个代码块里**。
- 用 `# 中文注释` 写“人话逻辑 / Python 此时在做什么”。
- 注释只帮助理解，不通过额外 `print()` 打出来，因此实际运行结果保持干净。
- 优先解释“为什么这样写 / 不这样写会怎样”，尤其是缩进、循环、变量和数据流。
- 一次只推进一个小知识点，用户理解后再进入下一课。
- 当前默认使用 **PyCharm**：给代码 → 在 PyCharm 运行 → 看正常输出 → 再解释 / 推进。

## 更新规则

每完成一个可验证的小步骤，优先更新本文件。只有涉及详细阶段规划、环境、Bug、模型或技术规范时，再同步更新对应详细文档。
