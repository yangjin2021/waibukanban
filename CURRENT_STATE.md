# Poker GTO Intelligence — Current State

> **默认恢复入口。** 当用户说“查看当前进度 / 继续项目 / 教我下一阶段”时，优先读取本文件；涉及双语言教学时，再读取 `docs/PYTHON_LISP_COURSE.md` 和 `docs/LEARNING_METHOD.md`。

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

## 5. 双语言教学固定规则

每次涉及 Lisp 时：

```text
① 先看当前 Python 正式代码
② 顺手给与当前 Python 进度完整对齐的 Lisp 全代码
③ 再截取今天真正要学的最小 Python ↔ Lisp 局部核心
④ 用已经会的 Python 解释 Lisp
⑤ 一次只深入一个主要 Lisp 新概念
⑥ Python 主线继续推进时，Lisp 完整对齐版同步升级
```

核心原则：

> **局部版负责学懂，完整版负责不迷路。**

## 6. Lisp 运行位置

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

## 7. 下一步课程

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

## 8. 当前教学约定

- 默认只显示小地图。
- 正式代码放上面，解释放下面。
- 遇到不懂代码先压到最小核心。
- 优先识别：功能名字 / 输入 / 处理 / 输出。
- 一次只增加一个主要新概念。
- Python 提供 / 规定的名字要说明来源。
- 不同作用域同名变量容易混淆时，教学版优先先换不同名字。
- Lisp 直接对齐当前 Python 项目学习进度，不从无关基础重新开始。
- 每次 Lisp 教学同时提供局部核心和完整对齐版。
- Solver / Dataset / NumPy / PyTorch / GPU AI 继续以 Python 为主。

## 更新规则

每完成一个明确验证的小步骤，优先更新本文件。课程结构变化时同步 `docs/PYTHON_LISP_COURSE.md`；教学规则变化时同步 `docs/LEARNING_METHOD.md`。