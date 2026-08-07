# Poker GTO Intelligence

这是一个以项目式学习方式，从零开始研发 **快速德州扑克 GTO 决策智能** 的长期项目。

## 最终目标

训练一个不需要在使用时现场运行 CFR/Solver 的模型：

```text
牌局状态
+ Board
+ Stack / Pot / Position
+ IP Range（Combo级）
+ OOP Range（Combo级）
+ Action History
+ Legal Actions / Bet Sizes
        ↓
   GTO Neural Model
        ↓
Combo级 Policy + EV
        ↓
13×13 Range 表 / Combo明细 / API
```

目标是让模型在推理阶段快速输出接近 Solver 的 GTO 策略，而不是每次重新求解。

## 当前已有资源

- 184 个已结算 PioSolver Full CFR 方案
- 统一求解精度约 1%
- 当前主数据域：150BB、BTN vs BB、SRP
- 已有范围表与方案总览
- 训练数据将优先从 `.cfr` 中提取 Combo 级 Range / Strategy / EV

## 当前硬件

- CPU：Intel Core i5-12490F
- RAM：32 GB
- GPU：NVIDIA GeForce RTX 2060 SUPER 8 GB
- SSD：WD_BLACK SN750 SE 1 TB

开发策略：**Small → Correct → Scale**。先用小模型与少量树跑通完整链路，再逐步扩大数据、模型和牌局配置。

## 项目设计原则

1. **内部始终保持 Combo 级精度**：以 1326 个起手 Combo 为统一空间，并使用 blocker mask。
2. **模型支持批量输出整个 Range**：一次推理输出 `Combo × Action` 策略矩阵。
3. **Range 是输入，不永久写死在模型里**。
4. **Stack / Position / Pot / Action History / Bet Size 都逐步设计成条件输入**。
5. **模型输出至少包含 Policy + EV**。
6. **统一 API**：AI 大脑与 13×13 Range UI、训练工具、未来其他项目解耦。
7. **新 Solver 数据优先用于继续训练同一个模型**，同时通过 replay 防止灾难性遗忘。
8. **最终准确性必须由 Solver 验证**，不能只凭“看起来像”。

## 项目文件

- [PROJECT_MAP.md](PROJECT_MAP.md)：长期项目 / 学习路线地图
- [PROGRESS.md](PROGRESS.md)：当前进度看板

## 进度标记

- `●` 已完成
- `◐` 当前进行
- `○` 未开始

当前正在进行：**Phase 00 — 开发环境与项目骨架**。
