# Poker GTO Intelligence — Phase Progress

> **阶段级看板，不是默认恢复入口。** 实时小步骤、当前代码、下一行要写什么统一看 [CURRENT_STATE.md](CURRENT_STATE.md)。

更新时间：2026-08-07

状态：`● 已完成` · `◐ 当前进行` · `○ 未开始`

## Phase 00–19

| Phase | 模块 | 状态 |
|---:|---|:---:|
| 00 | 零基础地基 / 开发环境 | ◐ 收尾 |
| 01 | Python 入门 | ◐ 当前 |
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

当前阶段交界：**Phase 00 收尾 → Phase 01 Python 入门**。

## 四个核心里程碑

| Milestone | 判定标准 | 状态 |
|---|---|:---:|
| M1 数据打开了 | Python → PioSolver → 真实 Combo 的 Strategy / Range / EV | ○ |
| M2 AI 出生 | 未见 Flop + Combo → AI 策略接近 Solver | ○ |
| M3 Range Intelligence | 一次输出整个 Combo Range + 13×13 / Combo 查看 | ○ |
| M4 Fast GTO Engine | State → Strategy + EV → Range 传播 → 下一街 | ○ |

## 更新频率

- 每个小练习 / 小代码完成：更新 `CURRENT_STATE.md`。
- Phase 或里程碑发生变化：更新本文件。
- 完整路线结构变化：更新 `PROJECT_MAP.md`。
