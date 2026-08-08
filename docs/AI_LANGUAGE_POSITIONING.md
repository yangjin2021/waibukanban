# Python + Common Lisp — AI 学习与工程定位

更新时间：2026-08-08

> 本文件规定 Python 与 Common Lisp 在 Poker GTO Intelligence / AI 学习中的长期角色分工。
>
> 目标不是平均学习两门语言，而是让它们各自承担最有价值的任务。

## 1. 一句话定位

```text
Python = 把 AI 真正做出来
Common Lisp = 帮助把 AI 的结构想清楚
```

更准确地说：

```text
Python
→ 正式工程主语言
→ 数据、模型、训练、GPU、测试、部署

Common Lisp
→ GPT 内思维实验室
→ 函数、组合、递归、树、状态、规则、搜索、符号、code-as-data
```

不采用 50/50 的双主语言路线。

## 2. 熟练度目标

```text
Python：★★★★★
目标 = 能独立开发真实 Poker AI 工程

Common Lisp：★★★
目标 = 能读、能写小型原型、能用来思考程序与 AI 结构
```

Lisp 当前不要求达到大型生产工程熟练度；如果未来用户主动产生更强兴趣，再单独加深。

## 3. AI 教学自动偏向规则

以后遇到 AI 新知识，先判断它属于哪一类，再决定主要使用哪种语言。

### A. 默认偏 Python 的内容

```text
数据读取 / 清洗
Solver 数据
NumPy / Pandas
Dataset / DataLoader
Tensor
PyTorch / JAX
神经网络训练
Loss
Backpropagation 的工程实现
Optimizer
Batch
GPU / CUDA
模型保存 / 加载
评估
实验管理
推理服务
部署
```

这些内容：

> **Python 是正式教学与实现主角。**

Lisp 如果没有明显结构教学价值，不为了“双语言”形式强行翻译。

### B. 默认适合 Lisp 辅助思考的内容

```text
函数组合
纯函数 / 状态变换
递归
树
Game Tree
Search
Legal Actions
State → Action → Next State
规则系统
符号表示
知识表示
DSL
宏
code-as-data
CFR / 博弈树的结构原型
程序生成 / 规则生成
```

这些内容可以先问：

```text
这个智能过程的结构是什么？
状态是什么？
输入 / 输出是什么？
动作如何产生新状态？
它是不是一棵树？
能不能写成几个可组合函数？
规则能不能作为数据？
```

必要时用 Lisp / S-expression 把结构显露出来，再回 Python 工程化。

### C. 数学 / AI 原理

例如：

```text
概率
EV
向量 / 矩阵
Softmax
Loss
Gradient
Backpropagation
Policy / Value
```

默认顺序：

```text
先讲语言无关的数学 / 数据流
↓
再用 Python 做真实实现
↓
只有当 Lisp 能明显帮助理解“函数组合 / 递归 / 树 / 状态”时才加入 Lisp
```

不要让语言语法遮住数学本身。

## 4. 混合型 AI 问题的标准流程

如果一个 AI 模块同时包含“结构设计 + 工程实现”，优先：

```text
① 先定义问题
↓
② 用人话 / 图 / 必要时 Lisp 看清结构
↓
③ 明确输入 / 状态 / 动作 / 输出 / 数据流
↓
④ Python 写正式实现
↓
⑤ NumPy / PyTorch / GPU 等工程化
↓
⑥ 测试与验证
```

例如 Poker 决策 AI：

```text
Lisp / 结构视角：
state
→ legal-actions
→ evaluate
→ choose-action
→ next-state

Python / 工程视角：
数据结构
→ Dataset
→ Model
→ Tensor
→ Policy / Value
→ GPU
→ 验证
```

核心原则：

> **Lisp 可以参与设计蓝图，但 Python 负责正式施工。**

## 5. Python 与 Lisp 不是 OOP vs FP 的简单对应

不要误写成：

```text
Python = 面向对象
Lisp = 函数式
```

两者都是多范式语言。

课程中更有用的视角是：

```text
面向对象：这个世界里有哪些“东西”？它们拥有什么状态和行为？

函数式：数据从哪里来？经过哪些函数变换？最后变成什么？
```

Python 可以同时使用 OOP 与函数式思想；Common Lisp 也有对象系统 CLOS。

在 Poker AI 中可以自然组合：

```text
OOP / 对象视角
→ Game / Player / Environment / Config

函数式 / 数据流视角
→ state → encode → evaluate → policy → action
```

## 6. 防止课程偏离的规则

### 不做

- 不把 Python 和 Lisp 按 50/50 时间平均分配。
- 不为了保持双语言形式，把 PyTorch / CUDA 机械翻译成 Lisp。
- 不让 Lisp 语法学习阻塞 Python 正式项目。
- 不把 Lisp 变成第二套需要同步维护的 Poker 工程。
- 不因为 Python 生态强，就放弃 Lisp 对结构思维的训练价值。

### 要做

- Python 主线始终推进真实 Poker AI。
- Lisp 只在能明显提高结构理解时介入。
- Lisp 原型 / 思考最终要能回映到 Python 的模块、函数、数据流或架构。
- AI 课程每进入一个新模块，先判断“这是工程问题还是结构问题”。

## 7. AI 教学决策树

```text
遇到新的 AI 知识
│
├── 数据 / 模型 / 训练 / GPU / 部署？
│       └── Python 主讲
│
├── 状态 / 树 / 搜索 / 规则 / 递归 / 符号？
│       └── Lisp 辅助思考 + Python 落地
│
├── 数学原理？
│       └── 先语言无关解释 + Python 实现
│
└── 两者混合？
        └── Lisp/图 看结构 → Python 工程化
```

## 8. 对 Poker GTO Intelligence 的长期分工

### Python 主线

```text
Card / Combo / Range Engine
Solver 数据
Dataset
Feature / Encoding
NumPy / Pandas
PyTorch / JAX
Policy Model
Value / EV Model
训练
验证
GPU
部署 / 工具化
```

### Lisp 思维实验室

```text
函数组合
状态变换
Game Tree
Action Tree
递归
搜索
规则
符号表示
CFR 结构理解
DSL
code-as-data
AI 架构草图
```

## 9. 最终目标

最终不是：

> 会两套语法。

而是形成两种互补能力：

```text
Python 问：
“这个 AI 怎么真正实现？”

Lisp 问：
“这个 AI 的结构到底是什么，为什么这样设计？”
```

最终工作流：

```text
想清楚
↓
设计结构
↓
Python 实现
↓
数据 / 模型 / GPU
↓
验证
↓
继续迭代
```

> **Python 是主战语言；Common Lisp 是程序设计健身房和 AI 架构草稿纸。**
