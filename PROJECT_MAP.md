# Poker GTO Intelligence 项目路线地图

状态：

- ● 已完成
- ◐ 当前进行
- ○ 未开始

---

# 总路线

```
基础计算机
    ↓
Python
    ↓
Card Engine
    ↓
Combo Engine
    ↓
Range Engine
    ↓
Solver 数据读取
    ↓
GTO Dataset
    ↓
机器学习基础
    ↓
Policy Network
    ↓
EV Network
    ↓
Range Intelligence
    ↓
多街模型
    ↓
Fast GTO Engine
```

---

# Phase 00 开发环境与项目骨架

目标：建立研发环境，理解程序运行方式。

产物：

- GitHub项目
- Python环境
- 项目目录
- 第一个运行程序

状态：◐

---

# Phase 01 Python基础

学习：

- 变量
- 数据类型
- 条件判断
- 循环
- 函数
- 文件读取

产物：能够自己编写简单扑克程序。

状态：○

---

# Phase 02 Card Engine

目标：让电脑认识扑克。

产物：

- 52张牌表示
- 花色/点数系统
- Board表示

状态：○

---

# Phase 03 Combo Engine

目标：建立德州扑克数学基础。

产物：

- 1326 Combo生成
- Blocker处理
- Combo权重

状态：○

---

# Phase 04 Range Engine

目标：建立Combo级Range系统。

产物：

- Range矩阵
- Combo权重
- Range更新

状态：○

---

# Phase 05 Solver数据工程

目标：把184棵Solver变成AI教材。

产物：

- Python控制Solver
- CFR数据提取
- Strategy/EV/Range Dataset

状态：○

---

# Phase 06 GTO Dataset

目标：生成神经网络训练数据。

数据结构：

```
Input:
Board
Combo
Range
Stack
Pot
History

Target:
Strategy
EV
```

状态：○

---

# Phase 07-10 AI核心

目标：训练第一个Poker AI。

包含：

- 神经网络基础
- Policy预测
- Softmax混合策略
- EV预测

状态：○

---

# Phase 11-14 高级能力

目标：接近真实GTO智能。

包含：

- Range Intelligence
- Flop/Turn/River
- 新配置泛化
- Solver验证

状态：○

---

# Phase 15 Fast GTO Engine

最终产品：

输入牌局状态。

输出：

- Combo Strategy
- EV
- Range
- 13×13展示
- API接口

状态：○
