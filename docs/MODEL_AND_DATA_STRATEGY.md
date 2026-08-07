# 模型与数据策略

## 1. 当前数据资产

当前项目拥有：

- 184 个 PioSolver Full CFR 方案
- 求解精度约 1%
- 当前主要配置：150BB、BTN vs BB、SRP
- 已有范围表 / 方案总览

重要理解：**184 不是 184 条样本，而是 184 棵可展开的完整 postflop 解算树。**

每棵树内部可以产生大量：

- Board state
- Node / Action history
- IP / OOP Range
- Combo-level Strategy
- Combo-level EV
- Reach / frequency 等训练信息

## 2. 第一条主路线：Solver Distillation

现阶段已经有 Solver 作为老师，因此不先从零重造 CFR Solver。

主链路：

```text
184 Full Solver Trees
        ↓
Solver Extractor
        ↓
GTO Dataset
        ↓
Supervised Neural Training
        ↓
Fast GTO Model
```

使用阶段：

```text
Poker State
    ↓
Forward Pass / Inference
    ↓
Combo Strategy + EV
```

不进行现场 CFR 迭代。

## 3. 训练与推理分离

### Training

- 较重
- 使用 GPU
- 反复比较预测与 Solver target
- 通过 loss / backpropagation 修改模型参数

### Inference

- 较轻
- 参数已固定
- 只做一次或少量前向计算
- 目标是快速批量输出整个 Range

最终产品主要执行 inference。

## 4. 第一代模型故意限制问题空间

第一代先固定：

- 150BB
- BTN vs BB
- SRP
- 固定 preflop ranges
- 固定 flop tree
- BB check 后 BTN decision

第一代输入可先简化为：

`Flop + Hero Combo`

输出：

`Check / B33 / B66 / B100 + EV`

目的：先证明模型能对未见 Flop 泛化，而不是一开始追求万能德州扑克。

## 5. 从单 Combo 到整个 Range

长期模型接口一次接受一个完整局面，并批量输出：

```text
1326 Combo slots × Legal Actions
```

对 blocked Combo 使用 mask，不删除固定槽位，从而让 Preflop / Flop / Turn / River 接口一致。

## 6. Range 展示层

内部：Combo-level。

外部：可汇总成 13×13 Range 表。

用户点击 `AKo` 等格子时，可以展开：

- AsKh
- AsKd
- AsKc
- ...

并查看各花色 Combo 的 Strategy / EV / Range weight。

## 7. Range Propagation

当当前 Combo 权重为 `r(c)`，模型给某行动 `a` 的概率为 `π(a|c)`，行动发生后该 Combo 的未归一化新权重为：

`r'(c) = r(c) × π(a|c)`

再对所有合法 Combo 归一化，得到该行动后的新 Range。

这使 Range 能随 Bet / Call / Raise / Check 自动流动。

## 8. 多配置持续扩展

未来新增：

- 100BB / 50BB / 200BB
- CO vs BB / SB vs BB
- 3Bet Pot
- 不同 Range
- 不同 Bet Tree

优先继续训练同一个条件模型，而不是每个配置创建独立模型。

正确流程：

```text
Old Model
+ New Solver Data
+ Representative Old Data (Replay)
        ↓
Continue Training
        ↓
New Model Version
```

参数量不要求随 Solver 数量线性增长；只有模型容量不足时才扩大网络。

## 9. 泛化纪律

模型可以尝试对未见状态插值 / 泛化，例如训练过 50 / 100 / 150BB 后预测 125BB。

但是：**没有 Solver 验证的预测不能直接宣称为准确 GTO。**

## 10. 当前硬件策略

当前：RTX 2060 SUPER 8GB、32GB RAM、1TB SSD。

原则：

- 流式读取 Dataset
- 小 Batch
- 必要时 FP16 / gradient accumulation
- 不把所有数据一次装入 RAM / VRAM
- 不复制数百 GB `.cfr` 到项目目录
- 优先控制中间 Dataset / cache 占用

模型升级按实验结果决定，不提前追求大模型。
