# Poker GTO Intelligence

这是一个从零开始、以项目式学习方式研发 **快速德州扑克 GTO 决策智能** 的长期项目。

## 最终目标

```text
牌局状态
+ Board / Stack / Pot / Position
+ IP / OOP Combo Range
+ Action History / Legal Actions
        ↓
   GTO Neural Model
        ↓
Combo级 Policy + EV + Range 信息
        ↓
13×13 Range / Combo明细 / 频率分析 / API
```

训练阶段使用 PioSolver `.cfr` 作为老师；最终使用阶段主要运行训练好的神经网络，不要求现场重新 CFR 求解。

## 最重要的两个入口

### 1. [CURRENT_STATE.md](CURRENT_STATE.md) — 默认恢复入口

用户说“查看当前进度 / 继续项目 / 教我下一阶段”时，优先只读取这个文件。

它固定包含：

1. **大地图进度**
2. **小地图进度**
3. **相关代码**
4. **简单学习总结**

### 2. [REFERENCE_INDEX.md](REFERENCE_INDEX.md) — 参数 / 字段索引

当聊天需要本机配置、Solver 参数、模型输入输出字段、路径、Bug、技术原则等具体信息时，先看这个索引，再只读取对应详细文档。

原则：**当前状态轻量加载，详细参数按需查询。**

## 当前项目核心理解

```text
输入参数 x
   ↓
训练好的神经网络 AI(x)
   ↓
输出参数 y
```

真正训练的是神经网络内部参数。底层坚持 Combo 级精度；13×13、Combo 表、牌面频率表、EV 表等只是同一份底层输出的不同展示。

## 当前资源摘要

- 184 个 PioSolver Full CFR 方案
- 求解精度约 1%
- 当前主要数据域：150BB、BTN vs BB、SRP
- CPU：Intel Core i5-12490F
- RAM：32 GB
- GPU：RTX 2060 SUPER 8GB
- SSD：WD_BLACK SN750 SE 1TB

具体值和后续变化不要依赖本摘要，按需从 `REFERENCE_INDEX.md` 跳到对应 Source of Truth。

## 信息架构

```text
README.md
├─ CURRENT_STATE.md       ← 默认：当前进度 / 代码 / 学习总结
├─ REFERENCE_INDEX.md     ← 按需：参数 / 字段去哪里查
│
├─ PROJECT_MAP.md         ← 完整 Phase 00–19 大路线
├─ PROGRESS.md            ← 详细阶段级进度
├─ EXECUTION_PLAN.md      ← 详细 Sprint 计划
├─ ENVIRONMENT.md         ← 本机 / Python / CUDA / 路径
│
└─ docs/
   ├─ CONTINUITY_PROTOCOL.md
   ├─ INPUT_OUTPUT_SPEC.md
   ├─ MODEL_AND_DATA_STRATEGY.md
   ├─ TECHNICAL_CONSTITUTION.md
   ├─ LEARNING_METHOD.md
   └─ TROUBLESHOOTING.md
```

## 文档职责

| 文件 | 职责 |
|---|---|
| `CURRENT_STATE.md` | **实时学习状态，默认只读这个** |
| `REFERENCE_INDEX.md` | 参数 / 字段 / 文档路由 |
| `PROJECT_MAP.md` | 完整长期路线 |
| `PROGRESS.md` | 详细阶段看板 |
| `EXECUTION_PLAN.md` | Sprint 详细计划 |
| `ENVIRONMENT.md` | 本机环境与路径事实来源 |
| `docs/INPUT_OUTPUT_SPEC.md` | Poker State / Model Output / API 字段 |
| `docs/MODEL_AND_DATA_STRATEGY.md` | Solver 数据、训练 / 推理策略 |
| `docs/TECHNICAL_CONSTITUTION.md` | 不轻易改变的架构原则 |
| `docs/LEARNING_METHOD.md` | 教学方法 |
| `docs/TROUBLESHOOTING.md` | Bug / 排错历史 |
| `docs/CONTINUITY_PROTOCOL.md` | 跨聊天 / 换模型恢复规则 |

## 更新原则

- 每完成一个可验证小步骤：优先更新 `CURRENT_STATE.md`。
- 环境、Bug、模型、接口等发生变化：只更新对应领域文档。
- 新增参数 / 字段类别：登记到 `REFERENCE_INDEX.md`。
- `PROGRESS.md` / `EXECUTION_PLAN.md` 主要在 Phase、Sprint 或计划明显变化时更新。
- 不把密码、Token、私钥、设备 ID 等敏感信息写入仓库。

开发策略：**Small → Correct → Scale**。
