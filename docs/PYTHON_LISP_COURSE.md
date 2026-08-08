# Python + Common Lisp 双语言课程路线

更新时间：2026-08-08

> 本文件只负责“双语言课程怎么同步推进”。
>
> 具体教学执行方式——六镜头、颜色、视觉化语言、比喻、最小核心递增、真实数据跑一轮、压缩/展开、正向/逆向追踪——统一遵循 `docs/TEACHING_SOP.md`。
>
> Python / Lisp 在 AI 学习与工程中的长期角色分工，统一遵循 `docs/AI_LANGUAGE_POSITIONING.md`。

## 1. 总原则

Poker GTO Intelligence 的**正式工程主线继续使用 Python**；Common Lisp 作为 GPT 内的同步学习副线。

Lisp 不要求接入本地 `C:\PokerGTOAI` 项目，也不要求为了课程安装 SBCL、PyCharm Lisp 插件或新建本地 Lisp 目录。

长期定位：

```text
Python = 把 AI 真正做出来
Common Lisp = 帮助把 AI 的结构想清楚
```

这不是双主语言路线，也不是 50/50 平均学习。

默认目标：

```text
Python 项目现在走到哪里
        ↓
Lisp 教学就直接对齐到同一知识进度
        ↓
先用已经懂的 Python 理解 Lisp
        ↓
遇到结构问题时用 Lisp 增加一个观察角度
        ↓
回到 Python 正式项目继续推进
```

Python 负责真正落地项目、Solver、数据、NumPy / PyTorch / AI；Common Lisp 用来训练函数、表达式、递归、列表、组合、符号处理和 code-as-data 思维。

### AI 内容的默认语言偏向

```text
数据 / 模型 / 训练 / GPU / 部署
→ Python

状态 / 树 / 搜索 / 规则 / 递归 / 符号 / CFR 结构
→ Lisp 辅助思考 + Python 落地

数学原理
→ 先语言无关解释 + Python 实现
```

详细规则见 `docs/AI_LANGUAGE_POSITIONING.md`。

## 2. 不从头重学 Lisp

不要因为加入 Lisp，就重新从与项目无关的 Hello World、纯算术或独立基础课开始慢慢追赶 Python。

如果某个 Lisp 基础语法是理解当前代码必需的，就在**当前 Poker 代码里顺手解释**。

当前 Python 已经到：

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

因此 Lisp 直接从功能上对齐这一整段，而不是回到 `(+ 1 2)` 重新排队学习。

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

如果当前 GPT 环境没有真实 Common Lisp 解释器，该结果只能标为“预期 / 概念结果”，不能标成已运行验证。

## 4. 当前 Python ↔ Lisp 功能对齐

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

语义颜色、树图、人话流程、真实数据展开等展示方式不在本文件重复维护，统一见 `docs/TEACHING_SOP.md`。

## 5. 强制双语言同步规则

每次涉及 Lisp，课程内容必须保持两种尺度：

### A. 当前最小局部核心

今天真正要理解的一小段。

例如：

```python
def create_card(rank, suit):
    return rank + suit
```

```lisp
(defun create-card (rank suit)
  (concatenate 'string rank suit))
```

### B. 当前完整对齐版

同一节还要顺手给出**和当前 Python 学习进度完整对应的 Lisp 全代码**。

原则：

> **局部版负责学懂，完整版负责不迷路。**

## 6. Python 推进时 Lisp 同步推进

以后 Python 主线每增加一个真实项目知识点，Lisp 对齐版本同步升级到同一功能层级。

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
- Lisp 不逐字符机械翻译。
- 两边保持功能、输入、处理、输出、数据流对齐。
- 如果进入第三方 AI / GPU / PyTorch 等生态而 Lisp 没有合理教学价值，不为了形式强行翻译。
- 如果进入 Game Tree / Search / State Transition / Rules / CFR 结构等内容，可以提高 Lisp 的辅助比重，但最后仍回到 Python 正式工程。

## 7. 当前课程顺序

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

接下来：

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

每一节的具体展示、六镜头选择、颜色规则、比喻和视觉化全部按 `docs/TEACHING_SOP.md` 执行。

## 8. AI 阶段的课程防偏规则

当课程进入真正 AI 阶段时，不再要求每个知识点都有完整 Lisp 翻译。

默认判断：

```text
这是工程实现问题？
→ Python 主讲

这是程序 / 智能结构问题？
→ Lisp 辅助思考

这是数学问题？
→ 先讲数学本身，再 Python 实现
```

如果是混合型问题：

```text
Lisp / 图 / 人话
先把结构想清楚
↓
Python
正式实现与工程化
```

这条规则优先级高于“为了双语言形式而机械同步”。

## 9. 判断是否真正学会

不以背 Lisp 术语为主，优先看能否：

```text
看到 Lisp
→ 找到对应的 Python 结构
→ 找出功能名字 / 输入 / 处理 / 输出
→ 看懂数据怎么流
→ 知道两种语言哪里一样、哪里不同
→ 最后把这种结构理解带回 Python 项目
```

最终目标不是同时维护两个正式 Poker 工程，而是：

> **Python 是主战语言；Common Lisp 是程序设计健身房和 AI 架构草稿纸。**
