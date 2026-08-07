# Poker GTO Intelligence 项目 / 学习路线地图

状态：`● 已完成` · `◐ 当前进行` · `○ 未开始`

> 核心目标：从零基础开始，边学习边研发一个**不需要运行时现场求解、能够快速输出 Combo 级 GTO 策略与 EV 的扑克决策智能**。

## 总路线

```text
基础数字与计算机
  ↓
Python
  ↓
Card Engine
  ↓
Combo Engine（1326）
  ↓
Range Engine
  ↓
Pio / CFR 数据读取
  ↓
GTO Dataset
  ↓
机器学习基础
  ↓
Policy Model
  ↓
Value / EV Model
  ↓
Range Intelligence
  ↓
Flop 泛化
  ↓
River
  ↓
Turn
  ↓
完整多街
  ↓
Solver 验证
  ↓
多 Range / 多 Stack / 多位置
  ↓
高级 AI（按需）
  ↓
CFR 深入理解
  ↓
Fast GTO Engine
```

## 完整阶段表

| 阶段 | 学什么 | 项目产物 | 过关标准 | 状态 |
|---|---|---|---|---|
| 00 零基础地基 | 文件、路径、数字、小数、百分比、最基础代数 | 能看懂项目中的数字和文件 | 理解 `0.35=35%`、路径/文件夹 | ◐ |
| 01 Python 入门 | 变量、字符串、数字、list、if、for、函数 | 第一个 Poker Python 程序 | 能读懂并修改简单 Python | ○ |
| 02 扑克牌表示 | 数据结构、编码思想 | Card / Hand / Board 系统 | Python 能认识 `AsKh`、`Qs8h4c` | ○ |
| 03 Combo 系统 | 组合、枚举、数组 | 1326 Combo Engine | 列出全部 1326 Combo 并处理 blocker | ○ |
| 04 Range 系统 | 百分比、概率、向量、权重 | Combo 级 Range Engine | 每个 Combo 有 0~1 权重 | ○ |
| 05 Solver 数据读取 | 进程、文本协议、文件处理 | Python ↔ PioSolver 数据提取器 | 一棵 `.cfr` 能自动读取 Strategy / Range / EV | ○ |
| 06 数据集工程 | 样本、输入、标签、训练集 | `.cfr → GTO Dataset` | 184 棵可批量转换成训练数据 | ○ |
| 07 第一次机器学习 | 模型、输入、输出、参数 | Poker AI 0.0 | 模型能学习最简单 Solver 数据规律 | ○ |
| 08 神经网络基础 | 神经元、权重、Loss、梯度、反向传播 | Poker AI 0.1 | Flop + Combo → Flop GTO | ○ |
| 09 Policy 模型 | Softmax、概率分布、交叉熵 | Combo → Action Frequency | 输出混合策略而非单一动作 | ○ |
| 10 Value 模型 | EV、期望、回归 | Strategy + EV Model | 每个 Combo 同时预测 Strategy 与 EV | ○ |
| 11 Range 智能 | 条件概率、reach、Range 更新 | Range Propagation Engine | 点 Bet / Call 后 Range 自动变化 | ○ |
| 12 未见牌面泛化 | Train/Val/Test、过拟合 | Poker AI 0.5 | 未见 Flop 仍能逼近 Solver | ○ |
| 13 Turn / River | 状态、历史、序列 | 多街 GTO AI | 能沿行动树继续预测 Turn / River | ○ |
| 14 Solver 级验证 | 策略误差、EV 误差、Best Response、Exploitability | AI vs Solver 测试系统 | 用量化指标证明接近 GTO | ○ |
| 15 多 Range / 多配置 | 条件输入、分布变化 | Range-aware GTO AI | 换 Range 仍能产生对应策略 | ○ |
| 16 多 Stack / 多位置 | 泛化、embedding 等 | Poker AI 1.0 | 100BB/150BB、不同位置可处理 | ○ |
| 17 高级 AI | Attention / Transformer / Residual 等按需学习 | 更强网络 | 只在简单模型确实遇到瓶颈时升级 | ○ |
| 18 博弈论 / CFR 深入 | Nash、Regret、CFR/CFR+/DCFR/MCCFR | 小型 CFR Solver | 能解释老师 Solver 的底层原理 | ○ |
| 19 最终系统 | 工程优化、缓存、GPU、部署 | Fast GTO Engine | 输入局面 → 快速输出完整 Combo Range 策略 | ○ |

## 四个核心里程碑

### Milestone 1 — 数据打开了

`Python → Solver → 读出一个真实 Combo 的 GTO Strategy / Range / EV`

### Milestone 2 — AI 出生

一个训练时没见过的 Flop：`Board + Combo → AI → GTO Strategy`，且预测明显接近 Solver。

### Milestone 3 — Range Intelligence

一次输出整个合法 Combo Range，并提供 13×13 Solver 风格展示；点击格子可展开具体花色 Combo。

### Milestone 4 — Fast GTO Engine

`牌局状态 → Range → AI → 完整 Strategy + EV → 行动 → Range 自动更新 → 下一街`

## 当前起点

当前只做 **Phase 00**：确认 Python / GPU / 本地目录，并写出项目第一行可执行代码。
