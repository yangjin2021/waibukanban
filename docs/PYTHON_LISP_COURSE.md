# Python + Common Lisp 双语言课程路线

更新时间：2026-08-08

## 1. 总原则

Poker GTO Intelligence 的**正式工程主线继续使用 Python**；Common Lisp 作为 GPT 内的同步学习副线。

Lisp 不要求接入本地 `C:\PokerGTOAI` 项目，也不要求为了课程安装 SBCL、PyCharm Lisp 插件或新建本地 Lisp 目录。

默认目标：

```text
Python 项目现在走到哪里
        ↓
Lisp 教学就直接对齐到同一知识进度
        ↓
先用已经懂的 Python 理解 Lisp
        ↓
同时继续推进 Python 正式项目
```

Python 负责真正落地项目、Solver、数据、NumPy / PyTorch / AI；Common Lisp 用来训练函数、表达式、递归、列表、组合、符号处理和 code-as-data 思维。

## 2. 不从头重学 Lisp

不要因为加入 Lisp，就重新从与项目无关的 Hello World、纯算术或独立基础课开始慢慢追赶 Python。

如果某个 Lisp 基础语法是理解当前代码必需的，就在**当前 Poker 代码里顺手解释**。

例如当前 Python 已经会：

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

那么 Lisp 直接从功能上对齐这一整段，而不是只讲 `(+ 1 2)`。

## 3. 当前完整 Lisp 对齐版本

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

对应结果概念上为：

```text
("As" "Ah" "Ks" "Kh")
```

该版本优先追求和当前 Python 数据流容易一一对照；以后再逐步介绍更 Lisp 风格、更高效的写法，例如 `push` + `nreverse`、`loop`、`mapcar` 等。

## 4. 当前 Python ↔ Lisp 对照

| Python | Common Lisp | 当前意义 |
|---|---|---|
| `def` | `defun` | 定义函数 |
| `create_card` | `create-card` | 函数名字 |
| `(rank, suit)` | `(rank suit)` | 输入参数 |
| `return rank + suit` | 最后一个表达式 | 函数结果 |
| `ranks = [...]` | `let` + list | 局部数据 |
| `for rank in ranks` | `dolist (rank ranks)` | 遍历 |
| 两层 `for` | 两层 `dolist` | Rank × Suit |
| `create_card(rank, suit)` | `(create-card rank suit)` | 函数调用 |
| `deck.append(card)` | 当前教学版用 `append` 组合回 `deck` | 放入 Deck |
| `return deck` | 函数最后的 `deck` | 返回 Deck |
| `print(deck)` | `format` | 显示结果 |

## 5. 固定语义颜色图例

Python ↔ Lisp 双语言对照时，同一个结构角色使用同一个教学颜色：

| 标记 | 角色 | Python ↔ Lisp 例子 |
|---|---|---|
| 🟦 | 功能 / 函数名字 | `create_card` ↔ `create-card` |
| 🟩 | 输入 / 参数 | `rank, suit` ↔ `rank suit` |
| 🟨 | 处理 / 表达式 | `rank + suit` ↔ `concatenate ...` |
| 🟥 | 输出 / 返回结果 | `return` ↔ 最后表达式结果 |
| 🟪 | 循环 / 控制结构 | `for` ↔ `dolist` / `loop` |
| 🟧 | 数据容器 / 局部变量 | `deck/ranks/suits` ↔ Lisp 对应绑定 |

示例：

```text
Python                    Common Lisp
🟦 create_card             🟦 create-card
🟩 rank, suit              🟩 rank suit
🟨 rank + suit             🟨 concatenate ...
🟥 return                  🟥 最后表达式的结果
```

颜色规则：

- 相同结构角色跨语言保持同色。
- 正式代码块保持干净；颜色主要用于对照表、结构图、人话执行流程和解释。
- ChatGPT / Markdown / PyCharm 的真实代码高亮可能不同，**固定的是这套语义颜色，不是 IDE 主题颜色**。
- 不只靠颜色表达；颜色旁边仍写“函数名 / 参数 / 处理 / 输出 / 循环 / 数据”等文字。
- 一个片段有多个作用时，按当前课程重点标主要角色，其余用文字补充。
- PyCharm 自带语法颜色和本课程语义颜色是两套不同系统。

原则：

> **同一个结构角色，同一种教学颜色。**

## 6. 强制双语言教学格式

当一节 Python 课程包含 Lisp 对照时，默认同时提供两种尺度：

### A. 当前正在解释的最小局部对照

例如只讲函数：

```python
def create_card(rank, suit):
    return rank + suit
```

```lisp
(defun create-card (rank suit)
  (concatenate 'string rank suit))
```

这一层用于真正理解当前新概念。

### B. 完整进度对齐版

在同一节里，还要顺手给出**与当前 Python 项目学习进度完整对齐的 Lisp 代码**。

也就是说，即使这节只详细解释 `defun`，用户仍然可以在下面看到完整的 Lisp `create-card + create-deck + 调用 + 输出` 版本。

目的：

```text
局部代码
→ 看懂今天的新东西

完整代码
→ 随时知道它在整个程序中的位置
```

完整 Lisp 版本不是要求一次学懂全部 Lisp 语法；没有讲到的部分可以先当作“未来会拆开的结构”。

## 7. Python 推进时 Lisp 必须同步推进

以后 Python 主线每增加一个真实项目知识点，Lisp 对齐版本也同步更新到同一层级。

例如：

```text
Python 加入 if / Card 合法性
→ Lisp 同步展示对应条件逻辑

Python Card 从字符串升级成更结构化数据
→ Lisp 同步展示对应数据表示

Python 进入 Combo / Range
→ Lisp 同步给完整功能对齐版本
```

但是：

- Python 仍是项目正式实现。
- Lisp 不要求逐行机械翻译。
- 两边要保持**功能、输入、处理、输出、数据流**对齐。
- 如果 Python 使用的是第三方 AI / 数据生态，而 Lisp 没有合理直接对应，不为了形式强行翻译。

## 8. 教学顺序

每次默认：

1. 只显示当前小地图。
2. 先给干净、可运行的当前 Python 正式代码（如果本课涉及 Python）。
3. 给当前 Lisp 完整对齐代码。
4. 再缩小到今天真正要学的 Python ↔ Lisp 局部核心。
5. 用固定语义颜色标出两边对应结构。
6. 用已经掌握的 Python 解释 Lisp 新语法。
7. 解释功能名字 / 输入 / 处理 / 输出 / 数据流。
8. 一次只深入一个主要 Lisp 新概念。
9. 用户理解后，Python 主线继续推进，同时 Lisp 完整版跟着更新。

## 9. Lisp 运行与验证规则

Lisp 学习默认发生在 GPT 中，不要求写入用户本地 Poker 项目。

如果当前环境没有真实 Common Lisp 解释器：

- 可以教学、分析和给出标准 Common Lisp 代码。
- 可以说明预期结果。
- **不能把没有实际执行过的 Lisp 代码标为“已运行验证”。**

如果之后出现可用 Lisp 执行环境，再把实际运行结果和语法验证纳入进度。

## 10. 近期同步路线

当前起点已经对齐到：

```text
create_card
+ 参数
+ 函数结果
+ list
+ 两层循环
+ create_deck
+ create_deck 调用 create_card
+ 外部调用并打印
```

接下来不是单独推进 Lisp 基础课，而是：

```text
当前 Python 函数组合继续学透
↓
同步拆 Lisp defun / 参数 / 自动返回
↓
同步拆 let / list
↓
同步拆 dolist / 嵌套 dolist
↓
Python Card Engine 第一版
↓
完整 Lisp 对齐版同步升级
↓
继续进入 Card 表示 / Combo Engine
```

## 11. 判断是否真正学会

不以背 Lisp 术语为主，优先看能否：

```text
看到 Lisp
→ 找到对应的 Python 结构
→ 找出功能名字 / 输入 / 处理 / 输出
→ 看懂数据怎么流
→ 知道两种语言哪里一样、哪里不同
→ 最后把这种结构理解带回 Python 项目
```

最终目标不是同时维护两个正式 Poker 工程，而是：**用 Python 做项目，用 Lisp 帮助形成更强的程序结构思维。**