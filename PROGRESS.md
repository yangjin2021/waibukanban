# Poker GTO Intelligence Progress

更新时间：2026-08-07

状态说明：`● 已完成` · `◐ 当前进行` · `○ 未开始`

## 总进度矩阵

| Phase | 模块 | 状态 |
|---:|---|:---:|
| 00 | 零基础地基 / 开发环境 | ◐ |
| 01 | Python 入门 | ◐ |
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
总路线：◐ ◐ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○ ○
```

## 当前交界：Phase 00 收尾 + Phase 01 Python 入门启动

| 当前任务 | 状态 |
|---|:---:|
| GitHub 仓库 / 路线 / 技术文档 | ● |
| Python 环境确认：Python 3.12.10 | ● |
| NVIDIA 驱动 / GPU 确认：RTX 2060 SUPER 8GB | ● |
| 本地 `C:\PokerGTOAI` 项目目录与基础子目录 | ● |
| 创建并运行 `src\main.py` | ● |
| PowerShell 正确运行 `python .\src\main.py` | ● |
| 第一张牌变量 `card = "As"` 并输出 `As` | ● |
| 区分 PowerShell 命令与 Python 代码 | ◐ |
| 理解变量 / 字符串 / `print()` | ◐ |
| Rank / Suit | ○ |
| 52 张牌 Deck | ○ |

## 环境记录

- Python：3.12.10
- PowerShell：7.6.4
- NVIDIA Driver：560.94
- `nvidia-smi` 显示 CUDA Version：12.6（驱动能力信息；PyTorch CUDA 可用性后续单独验证）
- GPU：NVIDIA GeForce RTX 2060 SUPER，8GB 显存
- 本地项目目录：`C:\PokerGTOAI`
- 已建立目录：`src / data / models / tests / logs`
- 第一段程序：`C:\PokerGTOAI\src\main.py`
- 已验证 PowerShell 命令：`python .\src\main.py`
- 当前已验证输出：`As`
- 当前 C 盘剩余空间约 34.7GB：代码项目可继续放在 C 盘，但后续 Solver、训练 Dataset 和大型模型文件不得堆在 C 盘，需要单独规划数据盘。

## 当前已记录排错

- BUG-001：把 CMD 提示符一起复制到 PowerShell — 已解决。
- BUG-002：把 Python 代码 `print(card)` 直接输入 PowerShell — 原因已确认。
- BUG-003：`main.py` 路径 / `src` 拼写错误 — 原因已确认。
- `CONFIG NOT FOUND`：目前记录为 PowerShell 提示符配置备注，不影响 Python 项目执行。

详见 `docs/TROUBLESHOOTING.md`。

## 当前下一步

1. 巩固：PowerShell 负责启动程序，Python 负责执行 `.py` 文件里的代码。
2. 理解 `card = "As"` 中变量、赋值与字符串。
3. 自己把 `As` 改成 `Kh` 并成功运行。
4. 开始拆解 `Kh`：`K = Rank`、`h = Suit`。
5. 逐步进入 52 张牌 Deck。

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
