# Poker GTO Intelligence — Current State

> **默认恢复入口。** 当用户说“查看当前进度 / 继续项目 / 教我下一阶段”时，优先读取本文件；需要双语言课程细节时，再读取 `docs/PYTHON_LISP_COURSE.md`。

更新时间：2026-08-08

状态：`● 已完成/已验证` · `◐ 当前进行/已讲解待验证` · `○ 未开始`

## 1. 当前总体路线

课程已从“单 Python 入门”调整为：

```text
Python 主线
    ↓
真正开发 Poker GTO Intelligence
    ↓
数据 / Solver / NumPy / PyTorch / AI

Common Lisp（SBCL）副线
    ↓
用同一个 Poker 问题重新观察函数、表达式、递归、组合、符号和 code-as-data
    ↓
把更清晰的结构思维带回 Python
```

**Python 仍是正式项目主语言；Common Lisp 是正式学习副线，不替代 Python 工程主线。**

详细双语言课程：`docs/PYTHON_LISP_COURSE.md`

## 2. 大地图进度

| Phase | 模块 | 状态 |
|---:|---|:---:|
| 00 | 零基础地基 / 开发环境 | ● 基本完成，终端按需复习 |
| 01A | Python 入门 / Card Engine 基础 | ◐ 当前，已接近第一版 Card Engine |
| 01B | Common Lisp 桥接课程 | ○ 即将开始 |
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

## 3. Python 小地图进度

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
| `len()` / `set()` 检查 | ● |
| `def` / 函数调用 | ● |
| 函数参数 `rank, suit` | ● |
| `return` = 把函数结果交出去 | ● |
| `def card(rank, suit): return rank + suit` 最小骨架 | ● |
| 循环中调用 `card(rank, suit)` | ● PyCharm 已验证（As / Ah / Ks / Kh） |
| `create_deck()` 内部建立 `deck` 并 return | ● 用户确认 PyCharm 运行正常 |
| 函数内一层 `for`：A × 4 suits | ● 已讲解并继续通过 |
| 函数内两层 `for`：2 ranks × 4 suits | ● 用户确认通过 |
| 完整 `create_deck()`：13 × 4 = 52 | ● 之前已有 PyCharm 验证记录 |
| 函数内 / 外同名 `deck` 的作用域区别 | ● 已理解 |
| **函数组合：`create_deck()` 调用 `create_card()`** | ◐ 已讲解，尚未贴出实际运行结果 |
| Card Engine 第一版整理 | ○ 下一步之一 |

## 4. Common Lisp 小地图

选择：**Common Lisp + SBCL**。

| 当前任务 | 状态 |
|---|:---:|
| 确定 Lisp 作为正式学习副线 | ● |
| PyCharm 继续作为统一编辑器 | ● 方案确定 |
| SBCL 安装 / 可执行验证 | ○ 下一课 |
| `lisp/main.lisp` 建立并运行 | ○ |
| S-expression / 表达式结构 | ○ |
| Lisp 字符串 / list | ○ |
| `defun` 定义 `card` | ○ |
| 输入 / 返回值与 Python 对照 | ○ |
| `let` 局部绑定 | ○ |
| `dolist` / `loop` 与 Python `for` 对照 | ○ |
| Lisp 版最小 Deck | ○ |
| 递归 / 高阶函数 / code-as-data | ○ 后续 |

**注意：SBCL 目前尚未实际安装 / 验证，因此不能记录为完成。**

## 5. 最近明确验证的 Python 结果

### A. `create_deck()` + `return deck`

已贴出 PyCharm 输出：

```text
第一张牌: As
最后一张牌: 2c
牌的数量: 52

Process finished with exit code 0
```

### B. 循环中调用 `card()`

已贴出 PyCharm 输出：

```text
As
Ah
Ks
Kh

Process finished with exit code 0
```

### C. 函数内部创建 deck

用户明确确认以下小步骤运行没有问题：

```python
def create_deck():
    deck = []
    deck.append("As")
    return deck
```

随后继续完成一层 / 两层循环教学。

## 6. 当前最重要的代码骨架

Python：

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
```

这一版本的知识目标是：

```text
create_card
负责一张牌

create_deck
负责一副牌

create_deck
    ↓ 调用
create_card
```

该“函数调用函数”版本已讲解，但目前没有新的 PyCharm 输出证据，所以保持 `◐`。

## 7. 新课程近期顺序

当前不继续无止境堆 Python 新语法，先建立双语言桥梁：

```text
L00  配置 / 验证 SBCL，并在现有 PokerGTOAI 项目建立 lisp/main.lisp
↓
L01  看懂最小 S-expression：函数 / 输入 / 表达式结果
↓
L02  用 Common Lisp 重写已经熟悉的 card 功能
↓
回 Python
↓
P11  实际验证 create_deck() 调用 create_card()
↓
Python / Lisp 各完成一个最小 Deck
↓
比较 for / dolist、局部变量、返回值
↓
整理 Python Card Engine 第一版
```

## 8. 当前开发方式

- 项目目录：`C:\PokerGTOAI`
- Python：`C:\PokerGTOAI\src\main.py`
- Lisp 计划：`C:\PokerGTOAI\lisp\main.lisp`
- 默认 IDE：**PyCharm**
- Python：PyCharm Run
- Common Lisp：计划使用 **SBCL**；初期优先从 PyCharm Terminal 运行，插件不是前置条件
- PowerShell：路径、Git、环境排查时使用

## 9. 当前教学约定

- 默认只显示**小地图表格**，除非用户主动要求大地图。
- **正式可运行代码放最上面，保持干净；解释放代码下面。**
- 遇到不懂的代码，先压缩到**不能再压的最小核心**。
- 固定优先识别：`功能名字 / 输入 / 处理 / 输出`。
- 每次只增加一个主要新概念；理解后再补下一层。
- Python 代码可结合 PyCharm 语法颜色解释角色，同时区分灰色 Inlay Hints / usages 与真正代码。
- 遇到 Python 提供 / 规定的名字，要说明来源：关键字、内置函数、list 方法、特殊方法、库提供名称或项目自定义名称。
- 不同作用域变量如果同名容易误解，教学版优先先换成不同名字讲清楚，再映射回真实项目代码。
- Common Lisp 现在是**正式副线**，不是只拿来画 S-expression 结构图；但每个 Lisp 概念都尽量绑定到已经理解的 Poker / Python 问题。
- 不机械地把 Lisp 逐行翻译成 Python；比较的是同一个功能的结构与数据流。
- 真正的 Solver / Dataset / NumPy / PyTorch / GPU AI 继续以 Python 为主。

## 更新规则

每完成一个可验证的小步骤，优先更新本文件。双语言课程结构发生变化时，再同步 `docs/PYTHON_LISP_COURSE.md`；教学规则发生变化时，再同步 `docs/LEARNING_METHOD.md`。