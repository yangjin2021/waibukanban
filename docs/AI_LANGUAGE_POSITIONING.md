# Poker GTO Intelligence — Python AI 学习与工程定位

更新时间：2026-08-08

> 本文件规定 Poker GTO Intelligence 的长期语言与工程定位。
>
> 当前规则已经统一为 **Python 单线**。正式教学、实验、数据处理、模型、算法原型与工程落地全部使用 Python。

## 1. 一句话定位

> **Python = 学习语言 + 原型语言 + AI 语言 + 最终工程语言。**

最终目标：

> **用 Python 做出一个类似 Solver 的 Poker GTO 智能系统。**

## 2. 为什么统一 Python

当前阶段最重要的是建立稳定的代码骨架感，并持续推进真实 Poker AI 项目。

统一 Python 可以减少：

```text
语言切换
语法切换
命名规则切换
运行环境切换
不必要的认知负担
```

把有限注意力集中在：

```text
Poker 逻辑
数据流
算法
数学
AI
工程
```

## 3. 所有 AI 内容默认使用 Python

包括但不限于：

```text
Card / Combo / Range
Poker State / Action
Solver 数据读取与自动化
数据清洗
NumPy / Pandas
Dataset / DataLoader
Tensor
PyTorch
神经网络
Loss / Optimizer
Batch
GPU / CUDA
模型保存 / 加载
评估
实验管理
推理服务
Game Tree
Search
Legal Actions
State → Action → Next State
Regret
CFR / CFR+ / DCFR / MCCFR
部署
```

如果某个概念本身是语言无关的，先用大白话、数学、图或手算建立直觉，然后仍然用 Python 实现。

## 4. AI 学习必须连接 Poker 语义

不要把 AI 课程变成与项目无关的通用教程。

优先建立以下连接：

```text
向量
→ Range / Policy / EV

矩阵
→ Batch / Dataset

概率分布
→ Strategy / Softmax

Mask
→ Legal Actions / Blocker

状态
→ Board / Position / Pot / Stack / Range / Action History

价值
→ EV

Game Tree
→ Poker 决策树

Regret / CFR
→ Solver-like 策略计算与学习

神经网络
→ 从状态近似输出策略 / EV
```

## 5. 当前长期路线

```text
Python 基础与代码骨架感
↓
Card / Deck / Combo
↓
Range
↓
Poker State / Action
↓
Solver 数据接口与数据资产
↓
Dataset
↓
NumPy / PyTorch
↓
第一个可训练 / 可泛化模型
↓
Game Tree / Search / Regret / CFR
↓
模型与算法结合
↓
推理、评估、持续改进
↓
类似 Solver 的 Poker GTO 智能系统
```

这条路线允许根据实际项目验证结果调整，但最终方向不变。

## 6. 学习筛选规则

遇到新知识，先问：

```text
现在需要它吗？
↓
它解决当前项目哪个问题？
↓
它怎样接到最终 Solver-like AI？
```

如果目前用不到，不因为“AI 学习应该完整”而提前堆入课程。

## 7. 教学卡住时怎么办

不换语言。

只在 Python 内增加观察方式：

```text
最小核心 Python
人话伪代码
输入 / 处理 / 输出
真实数据跑一轮
箭头数据流
树 / 层级
盒子 / 表格
压缩 ↔ 展开
正向 ↔ 逆向追踪
同构 Python 小例子
```

## 8. 最终原则

> **所有路最终回到 Python；所有 Python 最终回到 Poker AI；所有 Poker AI 工作最终朝向一个类似 Solver 的智能系统。**
