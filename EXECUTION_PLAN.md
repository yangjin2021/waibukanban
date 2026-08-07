# Poker GTO Intelligence — Sprint Plan

> **Sprint 级计划，不是默认恢复入口。** 当前正在写哪行代码、最后验证到哪里，请看 [CURRENT_STATE.md](CURRENT_STATE.md)。

状态：`● 已完成` · `◐ 当前进行` · `○ 未开始`

## Sprint 0 — 环境与第一段代码

目标：本地电脑能够稳定运行 PokerAI 项目代码。

主要任务：Python / NVIDIA 环境确认、项目目录、`src/main.py`、终端运行链路。

状态：**◐ 收尾**

过关标准：能从任意新 CMD / PowerShell 回到项目，能区分终端命令和 Python 代码，并能运行 `.py` 文件。

---

## Sprint 1 — 用 Python 表示一张牌

目标：围绕扑克牌学习变量、字符串和最基础的数据表示。

主要任务：

- `card = "As"`
- 字符串
- Rank / Suit
- 生成 52 张牌
- 验证无重复且数量为 52

状态：**◐ 当前**

过关标准：程序能生成并打印完整 52 张牌，并能解释一张牌如何由 Rank + Suit 表示。

---

## Sprint 2 — Combo Engine

目标：建立 AI 的最小扑克手牌单位。

主要任务：

- 两张牌 Combo 表示
- 枚举全部 1326 Combo
- 理解 AA / AKs / AKo 对应 6 / 4 / 12 Combo
- Board blocker
- 自动测试

状态：**○**

过关标准：Python 自动生成 1326 Combo，并正确排除与 Board 冲突的 Combo。

---

## Sprint 3 — Range Engine

目标：让每个 Combo 拥有 0~1 权重，并能沿动作传播。

主要任务：

- Range Weight
- 加权 Combo 数量
- Blocker + Range
- Action Frequency
- Range Propagation

状态：**○**

过关标准：能清楚区分 `Range Weight` 与 `Strategy Frequency`，并实现 `weight × action_probability`。

---

## Sprint 4 — 打开第一棵 Solver

目标：到达 Milestone 1 的最小版本。

```text
Python
  ↓
PioSolver / UPI
  ↓
加载 1 棵 .cfr
  ↓
真实节点
  ↓
Range / Strategy / EV
```

状态：**○**

先 1 棵验证，再逐步扩到 5 → 20 → 50 → 184。

过关标准：Python 能打印真实 Combo 的 Solver Range Weight、动作频率与 EV。

---

## 第一阶段开发纪律

1. 每次只增加一个真正需要的新概念。
2. 每一步必须有可验证产物。
3. 不提前堆高级网络结构。
4. 不一次处理全部 Solver 数据。
5. 不把大型 `.cfr`、Dataset、模型权重提交 GitHub。
6. 实时细节更新 `CURRENT_STATE.md`；Sprint 结构变化才更新本文件。
