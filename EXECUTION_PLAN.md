# Poker GTO Intelligence — 近期执行计划

本文件只管理“接下来实际做什么”，避免长期路线太大导致迷路。

状态：`● 已完成` · `◐ 当前进行` · `○ 未开始`

## Sprint 0 — 环境与第一段代码

目标：让本地电脑真正能够运行 PokerAI 项目代码。

| 任务 | 产物 | 状态 |
|---|---|:---:|
| 确认 Python | `python --version` 正常 | ◐ |
| 确认 NVIDIA 驱动 | `nvidia-smi` 正常 | ◐ |
| 创建项目根目录 | `C:\PokerGTOAI` | ○ |
| 创建基础目录 | `src/data/models/tests/logs` | ○ |
| 创建第一段代码 | `src/main.py` | ○ |
| 成功运行 | 终端显示项目启动文本 | ○ |

过关标准：用户能自己说明“Python 文件是什么、终端怎么运行它”。

---

## Sprint 1 — 用 Python 表示一张牌

目标：不脱离项目地学习变量、字符串、列表。

| 任务 | 产物 | 状态 |
|---|---|:---:|
| 变量 | `card = "As"` | ○ |
| 字符串 | 理解 `"As"` 是文本数据 | ○ |
| Rank / Suit | 从 `As` 中表示 A 与 s | ○ |
| 52 张牌 | 生成完整 Deck | ○ |
| 基础验证 | 没有重复牌，共 52 张 | ○ |

过关标准：程序能生成并打印 52 张扑克牌。

---

## Sprint 2 — Combo Engine

目标：建立 AI 最终的最小扑克单位。

| 任务 | 产物 | 状态 |
|---|---|:---:|
| 两张牌组合 | Hand / Combo 表示 | ○ |
| 枚举所有 Combo | 1326 个 Combo | ○ |
| AA / AKs / AKo 理解 | 6 / 4 / 12 Combo | ○ |
| Board blocker | 删除与公共牌冲突的 Combo | ○ |
| 自动测试 | 确认数量与 blocker 正确 | ○ |

过关标准：能解释为什么总共有 1326 Combo，并让 Python 自动生成。

---

## Sprint 3 — Range Engine

目标：让每个 Combo 拥有 0~1 权重。

| 任务 | 产物 | 状态 |
|---|---|:---:|
| Range Weight | `combo -> weight` | ○ |
| Range 总量 | 加权 Combo 统计 | ○ |
| Blocker + Range | Board 后自动更新合法范围 | ○ |
| 动作概率 | `combo -> action frequency` | ○ |
| Range Propagation | `weight × action_probability` | ○ |

过关标准：能够区分 `Range Weight` 和 `Strategy Frequency`。

---

## Sprint 4 — 打开第一棵 Solver

目标：到达第一个大里程碑 M1 的最小版本。

步骤：

```text
Python
  ↓
启动 PioSolver
  ↓
发送 UPI 命令
  ↓
读取一个 .cfr
  ↓
取得一个真实节点
  ↓
取得 Range / Strategy / EV
```

先只处理 1 棵 `.cfr`，成功后再扩到 5 → 10 → 184。

过关标准：Python 能打印一个真实 Combo 的 Solver Range Weight、动作频率与 EV。

---

## 第一阶段开发纪律

1. 每次只增加一个真正需要的新概念。
2. 每一步必须有可运行产物。
3. 不提前学习与当前任务无关的高级网络结构。
4. 不一次处理全部 184 棵树。
5. 不把大型 `.cfr` 复制进项目仓库。
6. GitHub 不提交 Solver 大文件、训练数据或大型模型权重。
7. 代码、路线、进度与关键实验结论提交 GitHub。
