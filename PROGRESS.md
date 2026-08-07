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
| 输入 / 输出规范 | ● |
| 近期执行计划 | ● |
| 进度看板 | ● |
| Python 环境确认：Python 3.12.10 | ● |
| NVIDIA 驱动 / GPU 确认：RTX 2060 SUPER 8GB | ● |
| 本地 `C:\PokerGTOAI` 项目目录 | ● |
| `src / data / models / tests / logs` 目录 | ● |
| 第一个 Python 程序 | ◐ |

## 环境记录

- Python：3.12.10
- NVIDIA Driver：560.94
- `nvidia-smi` 显示 CUDA Version：12.6（表示当前驱动支持的 CUDA 上限；PyTorch CUDA 可用性后续单独验证）
- GPU：NVIDIA GeForce RTX 2060 SUPER，8GB 显存
- 当前 C 盘剩余空间约 34.7GB：代码项目可继续放在 C 盘，但后续 Solver、训练 Dataset 和大型模型文件不得堆在 C 盘，需要单独规划数据盘。

## 已确认的关键认知

- 输入是一组牌局状态参数，最终都会编码成数字。
- 神经网络是项目真正要训练的核心映射函数。
- 训练阶段通过 Solver 标签不断调整网络内部参数。
- 推理阶段把新状态通过已训练参数做前向矩阵计算，直接输出结果。
- 最底层优先保留 Combo 级 `Policy + EV + Range Weight + Mask`。
- `Range Weight` 表示 Combo 在当前节点的范围权重；`Strategy Frequency` 表示当前节点怎么行动，两者不能混淆。
- 13×13 Range、Combo 表、单牌面频率、牌面类别频率、EV 表都是同一份底层结果的不同展示 / 汇总方式。

## 当前下一步：Sprint 0

1. 创建 `C:\PokerGTOAI\src\main.py`。
2. 写入并运行第一行 Python 代码。
3. 用户能自己解释：`.py` 文件、`print()`、字符串、终端运行分别是什么。
4. 完成 Sprint 0，进入 Sprint 1：用 Python 表示第一张扑克牌。

详细步骤见 [EXECUTION_PLAN.md](EXECUTION_PLAN.md)。

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
