# 项目式学习方法

本项目不是先学完整数学、完整 Python、完整 Lisp、完整 AI 再开始开发，而是始终围绕 Poker GTO Intelligence 的下一步功能学习。

当前课程采用：

```text
Python 主线 + Common Lisp 同步教学副线
```

Python 负责真正的 Poker GTO AI 工程；Common Lisp 用来训练函数、表达式、递归、组合、符号处理和 code-as-data 思维，并把这些结构能力带回 Python。

Lisp 默认在 GPT 内教学，不要求接入本地 Poker 项目，不要求为了课程安装 SBCL 或 PyCharm Lisp 插件。

详细双语言课程见：`docs/PYTHON_LISP_COURSE.md`。

## 1. 每次继续项目时

默认优先读取：

`CURRENT_STATE.md`

如果当前课程涉及 Python / Lisp 对照，再读取：

`docs/PYTHON_LISP_COURSE.md`

教学展示规则：

1. 默认只显示**小地图表格**。
2. 用户明确要求完整规划时，再显示大地图。
3. 先看当前已验证进度，再进入下一小课。
4. 不重复教学已经明确掌握的内容。

## 2. 强制教学规则：最小核心递增法

当用户看不懂一段代码时，第一件事不是逐行解释完整代码，而是先问：

> 这段代码最核心、最小的样子是什么？

默认顺序：

```text
最小核心
→ 看懂骨架
→ 只增加一层
→ 再增加一层
→ 最后回到完整项目代码
```

例如：

```python
def create_card(rank, suit):
    card = rank + suit
    return card

result = create_card("K", "h")
print(result)
```

先压成：

```python
def card(rank, suit):
    return rank + suit
```

只解释：

```text
card        = 功能名字
rank, suit  = 输入
rank + suit = 处理
return      = 输出
```

用户理解以后，再补函数调用、接收返回值、打印、循环和真实项目数据。

### 简化规则

- 简化不能改变原逻辑。
- 如果删除某一行会改变核心逻辑，就不能再删。
- 如果已经压到极限，要明确说明：**这一行是核心，不能再砍了。**
- 一层最多增加一个主要新概念。

## 3. 正式代码放上面，解释放下面

以后默认顺序：

```text
① 干净、可运行的正式代码
② 预期 / 实际运行结果
③ 人话伪代码 / 执行流程
④ 功能名字 / 输入 / 处理 / 输出
⑤ PyCharm 颜色或灰色提示解释（需要时）
⑥ 为什么这样写 / 不这样写会怎样
```

不要默认把大量中文教学注释塞进正式代码。

必要时可以保留极少数关键注释，但正式代码首先要保持清楚、可复制、可运行。

## 4. 人话伪代码

当 Python 或 Lisp 的语法壳挡住理解时，优先把程序翻译成自然动作。

例如：

```python
for rank in ranks:
    for suit in suits:
        deck.append(rank + suit)
```

翻译成：

```text
每拿一个 rank
    就把所有 suit 都走一遍
        做成一张牌
        放进 deck
```

优先使用：

```text
准备
拿出
交给
接住
组合
判断
放进
取出
重复
返回
最后得到
```

伪代码的缩进尽量与真实代码层级一一对应。

## 5. 建立“代码骨架感”

每遇到一个函数，优先识别：

```text
功能名字
输入
处理
输出
```

再看：

```text
谁调用它
数据从哪里来
结果到哪里去
它属于哪个更大的功能
```

目标不是背代码，而是让用户看到陌生代码时，也能主动找出骨架。

## 6. Python 名字来源必须讲清楚

用户需要分清“哪些词必须这样写”和“哪些名字可以自己起”。

例如：

```text
def       = Python 关键字，规定好的
return    = Python 关键字，规定好的
for / in  = Python 关键字，规定好的
print     = Python 内置函数
len       = Python 内置函数
append    = list 自带方法
card      = 项目自己起的函数名
rank      = 自己起的参数名
suit      = 自己起的参数名
deck      = 自己起的变量名
```

不要把所有 Python 提供的名字都误称为“关键字”。

如果用户再次问“这个能不能换名字”，要直接说明它属于哪一类。

## 7. 变量名要服务于理解

如果两个变量不是同一个变量，只是恰好同名，第一次教学时优先改成不同名字。

例如真实代码：

```python
def create_deck():
    deck = []
    return deck


deck = create_deck()
```

第一次讲作用域时可临时写成：

```python
def create_deck():
    local_deck = []
    return local_deck


received_deck = create_deck()
```

先讲清：

```text
local_deck
↓
return 的值
↓
received_deck
```

真正连接它们的是返回值，不是变量名字。

理解以后再映射回真实项目的常见同名写法。

## 8. PyCharm 颜色和灰色提示

教学时可以利用用户在 PyCharm 中看到的语法高亮帮助识别角色，例如：

```text
关键字
函数名
参数 / 变量
字符串
内置函数
注释
```

但颜色随主题变化，因此颜色只是辅助，真正要说明的是“代码角色”。

同时必须区分：

```text
真正 Python 代码
vs
PyCharm 灰色 Inlay Hints / usages / 类型提示
```

例如 `2 usages`、`rank:`、`suit:`、类型推断提示不是 Python 代码。

## 9. Python + Common Lisp 双语言规则

Common Lisp 是正式学习副线，但不是另一个正式本地工程。

### 角色分工

Python：

- Poker 项目正式代码
- Solver 数据
- 文件处理
- NumPy / Pandas
- Dataset
- PyTorch / JAX
- GPU
- 模型训练与验证

Common Lisp：

- 函数与表达式
- 局部绑定
- 列表处理
- 递归
- 高阶函数
- 树与搜索
- 符号规则
- 宏
- code-as-data
- 需要时用于 CFR / 博弈树概念原型

### Lisp 运行位置

默认：

```text
Python 正式项目 → 用户现有项目 / PyCharm
Lisp 学习实验   → GPT 内教学与代码对照
```

不要默认要求：

```text
C:\PokerGTOAI\lisp\
本地 SBCL
PyCharm Lisp 插件
```

除非用户之后明确要求本地 Lisp 环境。

如果当前 GPT 环境没有真实 Common Lisp 解释器，可以给出标准 Common Lisp 代码和预期结果，但不能把它标记成“已经实际运行验证”。

## 10. Lisp 必须直接对齐当前 Python 项目学习进度

**不要让 Lisp 从零重新追 Python。**

Python 当前学到哪一层，Lisp 直接从同一层开始。

例如 Python 当前是：

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

那么 Lisp 教学必须直接对齐：

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

不要重新花多节课从 `(+ 1 2)`、Hello World 等无关示例开始。

如果当前 Lisp 代码里出现了用户没见过的新语法，就**借助已经会的 Python 逐个解释**。

## 11. 每次 Lisp 教学必须同时给“局部核心 + 完整对齐版”

这是固定规则。

### A. 局部核心

只展示今天真正要理解的最小 Lisp 结构，并和 Python 小段一一对应。

例如：

```python
def create_card(rank, suit):
    return rank + suit
```

```lisp
(defun create-card (rank suit)
  (concatenate 'string rank suit))
```

这部分负责“今天真正学懂”。

### B. 完整对齐版

同一节还要顺手给出**和当前 Python 项目学习进度完整对齐的 Lisp 全代码**。

即使用户当前只详细学习 `defun`，也要让他能看到 `create-card + create-deck + 循环 + 调用 + 输出` 在 Lisp 里的整体位置。

注意：

- 完整版不是要求用户当场理解所有 Lisp 语法。
- 未讲到的部分可以先当整体结构看。
- 每次 Python 主线新增真实功能后，完整 Lisp 对齐版也应同步升级。

一句话原则：

> **局部版负责学懂，完整版负责不迷路。**

## 12. Python ↔ Lisp 对照原则

不要逐字符机械翻译，而要保持下面五件事对齐：

```text
功能
输入
处理
输出
数据流
```

常见对应：

```text
Python def            ↔ Common Lisp defun
参数                  ↔ 参数列表
局部变量              ↔ let
list                  ↔ list / quoted list
for                   ↔ dolist / loop
函数调用              ↔ S-expression 调用
两层循环 Rank × Suit  ↔ 嵌套 dolist / loop
return                ↔ 最后表达式结果（常见情况）
create_deck           ↔ Lisp 版 deck 生成
```

如果 Python 使用第三方库、GPU、PyTorch 等而 Lisp 没有合理的直接教学价值，就不为了形式强行翻译。

## 13. 主动抽查

可以偶尔用 1～2 个短问题检查已经讲过的东西，例如：

```text
这段函数的输入是什么？
return 出去的是什么？
这个名字是谁规定的？
删掉这一行会怎样？
这两个变量是不是同一个变量？
这层 for 每轮发生什么？
同一个功能换成 Lisp 后，输入 / 输出有没有变化？
```

不出陷阱题，不用没讲过的语法测试用户。

用户答错时先给小提示；如果仍卡住，退回最小核心，而不是直接堆完整答案。

## 14. 数学按项目需要出现

```text
百分数        → Range frequency
概率          → Strategy
组合          → 1326 Combos
加权平均      → Range EV
向量          → [Check, B33, B66, B100]
矩阵          → Batch / Range Data
函数          → AI(x) = y
平方 / 误差   → Loss
导数          → Gradient
链式法则      → Backpropagation
概率分布      → Softmax
条件概率      → Range Update
```

不为了“学数学”先刷完整课程，项目需要时补。

## 15. 当前开发方式

默认：

- 项目：`C:\PokerGTOAI`
- Python：`C:\PokerGTOAI\src\main.py`
- IDE：PyCharm
- Python：PyCharm Run
- Lisp：GPT 内同步教学副线
- PowerShell：路径、Git、环境排查

不要假设终端一定在项目目录。

## 16. 学习成果必须变成项目资产

每完成一小步，尽量留下至少一个可追踪成果：

- 新代码
- 新测试
- 新数据样本
- 新模型
- 新实验记录
- 新文档
- 进度状态更新

每完成一个**明确验证**的小步骤，优先更新 `CURRENT_STATE.md`。

课程结构变化时更新 `docs/PYTHON_LISP_COURSE.md`。

教学规则变化时更新本文件。

最终目标不是“上完课程”，而是让 Poker GTO Intelligence 每次都向前一步，同时形成可以跨语言迁移的程序结构能力。