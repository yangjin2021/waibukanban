# Poker GTO Intelligence — 教学与项目连续性协议

本文档用于保证本项目在不同聊天页面、不同会话、不同模型之间仍能连续推进。

## 1. GitHub 是项目事实来源

当用户说“继续项目”“教我下一阶段”“从当前进度继续”等表达时，助手应优先读取仓库中的：

- `PROJECT_MAP.md`：大地图 / 长期阶段
- `PROGRESS.md`：当前真实进度
- `EXECUTION_PLAN.md`：当前小地图 / Sprint
- `ENVIRONMENT.md`：本机与软件环境
- `docs/TROUBLESHOOTING.md`：已遇到的 Bug 与解决记录
- 必要时读取技术规范和学习方法文档

不得仅凭聊天记忆猜测当前进度。

## 2. 每次继续教学的固定开场

只要用户要求继续教学或进入下一阶段，回答开头必须先给出：

### 大地图

显示当前处于 Phase 几，以及前后关键阶段，例如：

```text
Phase 00 环境 ●/◐
→ Phase 01 Python
→ Phase 02 Card
→ Phase 03 Combo
→ Phase 04 Range
→ ...
```

### 小地图

显示当前 Sprint 和当前任务，例如：

```text
Sprint 1 — 用 Python 表示一张牌
● 环境已验证
● 第一段程序已运行
◐ card = "As"
○ Rank / Suit
○ 52 张牌
```

随后再开始本次课程。

## 3. 跨页面 / 跨会话 / 换模型规则

如果用户换了聊天页面、开启新会话或换了模型，只要仍在继续本项目：

1. 先读上述 GitHub 状态文件；
2. 明确告诉用户“已从 GitHub 恢复到哪个阶段 / Sprint / 当前任务”；
3. 从该任务继续，不要求用户重新复述已经记录的项目事实；
4. 如果 GitHub 与用户当前提供的新事实冲突，以用户最新可验证事实为准，并更新 GitHub。

## 4. 进度更新规则

只有真正可验证完成的任务才能从 `◐ / ○` 改为 `●`。

可验证包括：

- 命令成功执行；
- 程序成功运行；
- 用户提交输出结果；
- 测试通过；
- 用户能够完成对应小练习；
- 数据 / 模型 / Solver 结果被真实读取或验证。

仅仅“看过解释”不算完成。

## 5. Bug / 排错记录规则

开发过程中遇到的真实问题应记录到：

`docs/TROUBLESHOOTING.md`

按 `BUG-001 / BUG-002 / ...` 编号，至少记录：

- 日期
- 环境
- 现象
- 原因
- 解决方法
- 验证状态
- 从中学到的知识

问题解决后更新状态，不删除旧记录。

## 6. 环境变化规则

Python、PyTorch、CUDA、Driver、GPU、RAM、磁盘、Solver 路径、Dataset 路径、模型路径等变化，应同步更新 `ENVIRONMENT.md`。

## 7. 教学风格连续性

本项目坚持：

`项目问题 → 大白话 → 最少数学 → 小段 Python → 用户亲手运行 → 验证 → 更新进度`

不因为换聊天页面或换模型而突然跳到高级内容。

## 8. 每课结束

如果本次完成了可验证步骤：

1. 更新 `PROGRESS.md`；
2. 更新 `EXECUTION_PLAN.md`；
3. 必要时更新 `ENVIRONMENT.md` / `TROUBLESHOOTING.md`；
4. 下一次继续时从最新 GitHub 状态恢复。

本文件是项目的 **连续性规则事实来源（Continuity Source of Truth）**。
