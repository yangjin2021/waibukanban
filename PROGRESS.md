# Poker GTO Intelligence Progress

更新时间：2026-08-07

状态说明：`● 已完成` · `◐ 当前进行` · `○ 未开始`

## 总进度矩阵

| Phase | 模块 | 状态 |
|---:|---|:---:|
| 00 | 零基础地基 / 开发环境 | ◐ |
| 01 | Python 入门 | ○ |
| 02 | 扑克牌表示 | ○ |
| 03 | Combo Engine（1326） | ○ |
| 04 | Range Engine | ○ |
| 05 | Solver 数据读取 | ○ |
| 06 | GTO Dataset | ○ |
| 07 | 第一次机器学习 | ○ |
| 08 | 神经网络基础 / PokerAI 0.1 | ○ |
| 09 | Policy Model | ○ |
| 10 | Value / EV Model | ○ |
| 11 | Range Intelligence | ○ |
| 12 | 未见牌面泛化 | ○ |
| 13 | Turn / River 多街 | ○ |
| 14 | Solver 级验证 | ○ |
| 15 | 多 Range / 多配置 | ○ |
| 16 | 多 Stack / 多位置 | ○ |
| 17 | 高级 AI（按需） | ○ |
| 18 | 博弈论 / CFR 深入 | ○ |
| 19 | Fast GTO Engine | ○ |

```text
总路线：◐ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○
```

## 当前：Phase 00 — 零基础地基 / 开发环境

| 当前任务 | 状态 |
|---|:---:|
| GitHub 仓库建立 | ● |
| 项目总路线文档 | ● |
| 技术宪法 | ● |
| 学习方法文档 | ● |
| 模型 / 数据策略文档 | ● |
| 进度看板 | ● |
| Python 环境确认 | ◐ |
| NVIDIA GPU 环境确认 | ◐ |
| 本地 `PokerGTOAI` 项目目录 | ○ |
| `src / data / models / tests / logs` 目录 | ○ |
| 第一个 Python 程序 | ○ |

## 当前下一步

1. 在 Windows CMD 执行 `python --version`。
2. 执行 `nvidia-smi`。
3. 创建本地 `C:\PokerGTOAI` 项目目录及子目录。
4. 创建并运行第一段项目代码。
5. 开始 Phase 01：围绕扑克牌表示学习 Python 变量、字符串与列表。

## 四个大里程碑

| Milestone | 判定标准 | 状态 |
|---|---|:---:|
| M1 数据打开了 | Python → PioSolver → 读出一个真实 Combo 的 Strategy / Range / EV | ○ |
| M2 AI 出生 | 未见 Flop + Combo → AI 策略明显接近 Solver | ○ |
| M3 Range Intelligence | 一次输出整个 Combo Range，并能 13×13 / Combo 级查看 | ○ |
| M4 Fast GTO Engine | 状态 → Strategy + EV → Range 传播 → 下一街 | ○ |

## 进度更新规则

每完成一个真正可验证的步骤：

1. 更新本文件状态；
2. 提交对应代码 / 文档；
3. 必要时补充学习日志或实验结果；
4. 不因为“看过/听懂了”就标记完成，必须以能运行、能解释或能验证为准。
