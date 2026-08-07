# Poker GTO Intelligence — Reference Index

> **按需查询索引。** 正常“查看进度 / 继续教学”不需要读取本文件；当聊天需要某个环境参数、Solver 参数、模型字段、API 字段、Bug 记录或技术原则时，先看本索引，再只读取对应源文件。

## 1. 默认加载策略

```text
查看当前进度 / 继续教学
        ↓
只读 CURRENT_STATE.md
        ↓
输出：1 大地图  2 小地图  3 相关代码  4 简单学习总结
```

只有出现具体信息需求时：

```text
需要某个参数 / 字段
        ↓
REFERENCE_INDEX.md
        ↓
找到对应 Source of Truth
        ↓
只读取那个文件
```

不要为了一个参数默认加载所有文档。

## 2. 文档路由

| 用户需要的信息 | 优先读取 | 主要内容 |
|---|---|---|
| 当前进度 / 下一课 / 当前代码 | `CURRENT_STATE.md` | 大地图、小地图、代码、学习总结 |
| 完整 Phase 00–19 路线 | `PROJECT_MAP.md` | 长期路线、里程碑、阶段过关标准 |
| 更详细进度历史 / 阶段看板 | `PROGRESS.md` | 详细完成状态、阶段级进度 |
| Sprint 详细任务 | `EXECUTION_PLAN.md` | Sprint 0–4 的详细计划 |
| 本机配置 / 软件版本 / 路径 | `ENVIRONMENT.md` | CPU、RAM、GPU、Python、Driver、CUDA、项目/数据路径 |
| Solver 数据资产 / 第一代模型配置 | `docs/MODEL_AND_DATA_STRATEGY.md` | 184 树、1%、150BB、BTN vs BB、SRP、蒸馏路线 |
| 神经网络输入 / 输出 / API 字段 | `docs/INPUT_OUTPUT_SPEC.md` | State 字段、Policy、EV、Range Weight、Mask、UI/API |
| 长期架构原则 | `docs/TECHNICAL_CONSTITUTION.md` | 1326 Combo、Range 输入、Action-aware、验证、持续学习 |
| 教学方法 | `docs/LEARNING_METHOD.md` | 零基础项目式教学顺序 |
| 跨聊天 / 换模型恢复规则 | `docs/CONTINUITY_PROTOCOL.md` | 默认加载、输出格式、更新规则 |
| 已遇到 Bug / 排错 | `docs/TROUBLESHOOTING.md` | BUG-001…、终端/路径问题等 |
| 项目总体介绍 | `README.md` | 最终目标与文档入口 |

## 3. 常用参数 / 字段索引

这里主要保存“字段名 → 去哪里查”，避免同一数值在多个文件重复维护。

### Environment / Path

| Key / 字段 | Source |
|---|---|
| `env.cpu` | `ENVIRONMENT.md` |
| `env.ram` | `ENVIRONMENT.md` |
| `env.gpu` | `ENVIRONMENT.md` |
| `env.vram` | `ENVIRONMENT.md` |
| `env.ssd` | `ENVIRONMENT.md` |
| `env.python_version` | `ENVIRONMENT.md` |
| `env.powershell_version` | `ENVIRONMENT.md` |
| `env.nvidia_driver` | `ENVIRONMENT.md` |
| `env.nvidia_smi_cuda` | `ENVIRONMENT.md` |
| `env.pytorch_version` | `ENVIRONMENT.md` |
| `env.torch_cuda_available` | `ENVIRONMENT.md` |
| `path.project_root` | `ENVIRONMENT.md` |
| `path.main_py` | `CURRENT_STATE.md` / `ENVIRONMENT.md` |
| `path.piosolver_exe` | `ENVIRONMENT.md` |
| `path.cfr_root` | `ENVIRONMENT.md` |
| `path.dataset_root` | `ENVIRONMENT.md` |
| `path.checkpoint_root` | `ENVIRONMENT.md` |

### Solver / Dataset / Training

| Key / 字段 | Source |
|---|---|
| `solver.tree_count` | `docs/MODEL_AND_DATA_STRATEGY.md` |
| `solver.solve_precision` | `docs/MODEL_AND_DATA_STRATEGY.md` |
| `solver.base_stack` | `docs/MODEL_AND_DATA_STRATEGY.md` |
| `solver.base_matchup` | `docs/MODEL_AND_DATA_STRATEGY.md` |
| `solver.base_pot_type` | `docs/MODEL_AND_DATA_STRATEGY.md` |
| `model.v0_1_input` | `docs/MODEL_AND_DATA_STRATEGY.md` |
| `model.v0_1_output` | `docs/MODEL_AND_DATA_STRATEGY.md` |
| `training.pipeline` | `docs/MODEL_AND_DATA_STRATEGY.md` |
| `training.continual_learning` | `docs/MODEL_AND_DATA_STRATEGY.md` / `docs/TECHNICAL_CONSTITUTION.md` |
| `training.validation_principles` | `docs/TECHNICAL_CONSTITUTION.md` |

### Poker State 输入字段

这些字段的正式定义统一查 `docs/INPUT_OUTPUT_SPEC.md`：

- `street`
- `board`
- `acting_player`
- `position`
- `effective_stack`
- `pot`
- `ip_range[1326]`
- `oop_range[1326]`
- `action_history`
- `legal_actions`
- `bet_raise_size`
- `valid_blocker_mask[1326]`

### Model 输出字段

统一查 `docs/INPUT_OUTPUT_SPEC.md`：

- `policy[1326, legal_actions]`
- `action_ev[1326, legal_actions]`
- `range_weight[1326]`
- `valid_mask[1326]`
- `overall_action_frequency`
- UI 聚合：13×13 / Combo detail / Board frequency / EV view

### 核心语义

| 概念 | Source |
|---|---|
| `Range Weight` 是什么 | `docs/INPUT_OUTPUT_SPEC.md` |
| `Strategy Frequency` 是什么 | `docs/INPUT_OUTPUT_SPEC.md` |
| `Range Propagation` | `docs/INPUT_OUTPUT_SPEC.md` / `docs/MODEL_AND_DATA_STRATEGY.md` |
| 1326 Combo 固定槽位 / blocker mask | `docs/TECHNICAL_CONSTITUTION.md` |
| 169 格负责看、Combo 负责算 | `docs/INPUT_OUTPUT_SPEC.md` |
| 运行时不用 Solver / CFR | `docs/TECHNICAL_CONSTITUTION.md` |

## 4. 更新原则

- **实时学习状态**：只在 `CURRENT_STATE.md` 维护为首要事实来源。
- **某类参数的真实值**：只在对应领域 Source of Truth 中维护，索引尽量不复制值。
- `PROGRESS.md` / `EXECUTION_PLAN.md` 作为更详细的阶段 / Sprint 文档，可在阶段或计划变化时更新，不要求每个小步骤都读取。
- 出现新的参数类别时，先确定唯一 Source of Truth，再把字段名登记到本索引。
- 不在仓库中记录密码、Token、私钥、产品 ID、设备 ID 等敏感凭据。
