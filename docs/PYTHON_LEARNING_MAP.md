# Python → Poker AI 螺旋式学习小地图

更新时间：2026-08-09

> 这是 Python / Poker AI 的课程级小地图。核心原则不是“学完一个知识点再永久离开”，而是 **旧知识反复复用 + 每课约 15% 新知识 + 同课内部层层递进 + 交互式验证后才升级**。

## 1. 总原则：85% 已会 + 15% 新知识

这里的 85% / 15% 是教学设计目标，不要求机械按字数计算。

每一课默认：

```text
约 85%：来自已经学过、但需要继续自动化的知识
+
约 15%：真正的新概念 / 新操作 / 新结构
```

目的：

```text
旧知识不掉线
↓
新知识只高一小截
↓
每课都能完成
↓
复杂能力通过很多次小升级自然长出来
```

如果上一课暴露明显漏洞：

```text
暂停新增 15%
↓
回补最低层漏洞
↓
交互复测
↓
稳定后再继续 +15%
```

如果连续多课高正确率：可以把新知识提高到约 20%，但默认仍以 15% 为中心。

---

## 2. 同一堂课内部也必须层层递进

每堂课默认使用 5 层：

```text
Level 1 旧知识快速复测
↓
Level 2 同知识变式 / 易混对比
↓
Level 3 本课约 15% 新知识
↓
Level 4 新旧知识混合
↓
Level 5 Poker Boss：放回真实项目代码
```

每层尽量使用交互式点击 / 选择 / 填写。

规则：

- 当前层未通过，不解锁更复杂层。
- 错题按知识类型归因，不只看总分。
- 代码必须尽量语法着色，并辅助说明 token / 符号。
- Boss 不是独立难题，而是把本课 85% 旧知识 + 15% 新知识重新组合。

---

## 3. 掌握状态不再只分“讲过 / 没讲过”

以后知识点区分：

```text
○ 未接触
△ 已见过：知道大概是什么
◐ 能单独做：简单题能处理
● 稳定：混合代码里也能正确识别 / 使用
★ 项目化：能在 Poker AI 真实代码中独立应用
```

**讲过 ≠ 掌握。**

---

# 4. Stage A — Python 数据与结构识字

目标：看到代码就能判断“现在这个东西是什么类型、哪一层、从哪里取出来”。

### A01 变量 + `int` / `str`

85%：变量名、`=`、字符串、整数、`type()`

15% 新知识：`==` 与 `=` 的区别

Boss：比较 Poker position / stack 数据。

### A02 `list` 基础

85%：`int` / `str` / 变量

15%：`[]` 创建 list、元素、`len()`

Boss：`["As", "Ks"]` 表示 Combo。

### A03 嵌套 `list`

85%：单层 list、str

15%：`["132"]` vs `[["132"]]`、最外层 / 当前层

Boss：Range = 多个 Combo。

### A04 `dict` 基础

85%：str / list / 嵌套结构

15%：`{key: value}`、`state["position"]`

Boss：Poker `state`。

### A05 `[]` 的上下文 + list 索引

85%：list / dict / 取值

15%：`cards[0]` / `cards[1]`，索引从 0 开始

Boss：从 Combo 中取第一张 / 第二张牌。

### A06 `in` 与“当前层”

85%：list 层级、索引、str/list 类型

15%：`A in B` = 在 B 当前层找 A

Boss：Combo 是否在 Range。

### A07 `False` vs `TypeError`

85%：类型、`==`、`in`

15%：类型不同不等于一定报错；比较失败 vs 操作不兼容

Boss：诊断 Range 类型错位。

### A08 `.get()` + 默认值

85%：dict 取值、list、in

15%：`dict.get(key, default)` 与缺失 key

Boss：根据 position 取当前 Range。

### A09 布尔条件

85%：`==` / `in` / `.get()`

15%：`True` / `False`、`not in`、`!=`

Boss：合法 / 非法 Combo 判断。

### A10 `if / else`

85%：布尔判断、Range membership

15%：条件分支

Boss：`Play` / `Fold`。

**Stage A 出口标准：**

不运行代码，也能把复杂表达式按以下顺序展开：

```text
先求值
→ 看最外层类型
→ 看当前层直接元素
→ 再判断操作
→ 得到 True / False / Error / value
```

---

# 5. Stage B — 容器操作与循环

目标：不只“看懂数据”，开始批量处理 Poker 数据。

### B01 `append()`

85%：list、索引、Range

15%：list 方法与原地添加

Boss：逐个添加 Combo。

### B02 最小 `for`

85%：list、append、元素

15%：`for item in items`

Boss：逐个读取 Range Combo。

### B03 `for + if`

85%：for、in、if

15%：循环内部条件筛选

Boss：筛选特定 Combo。

### B04 `range()` + 数字索引

85%：for、索引

15%：`range(len(cards))`

Boss：按位置遍历 Deck。

### B05 两层循环

85%：for、range、索引

15%：嵌套循环

Boss：Rank × Suit 生成牌。

### B06 两个索引 `i / j`

85%：两层循环、索引

15%：两个位置变量

Boss：两张牌配对。

### B07 `j = i + 1` 的去重思想

85%：双索引、range

15%：避免自己配自己和反向重复

Boss：4 张牌生成 6 个 Combo。

### B08 完整 52 张 → 1326 Combo

85%：Deck、双索引、append

15%：规模扩大 + `len()` 验证

Boss：生成 1326 Combo。

---

# 6. Stage C — 函数与数据流

目标：把已经会的 Poker 操作封装成可复用模块。

### C01 `def` + 参数

85%：变量、字符串、处理表达式

15%：函数边界与输入参数

Boss：`create_card(rank, suit)`。

### C02 `return`

85%：函数、变量

15%：函数输出与调用方接收

Boss：Card 返回给 Deck。

### C03 函数调用函数

85%：def / 参数 / return

15%：调用链

Boss：`create_deck()` 调 `create_card()`。

### C04 list 作为函数输入输出

85%：函数 + list

15%：容器跨函数流动

Boss：`create_combo(card1, card2)`。

### C05 dict 作为 State 输入

85%：函数 + dict + `.get()`

15%：结构化状态传入函数

Boss：`decide_action(state, ranges)`。

### C06 作用域

85%：函数内外变量

15%：局部名字与外部名字

Boss：函数内 / 外 `deck`。

### C07 输入验证与错误诊断

85%：type、len、if

15%：主动检查数据结构

Boss：拒绝错误 Combo / Range 形状。

---

# 7. Stage D — Poker 数据模型

目标：形成稳定的 Card / Combo / Range / State / Action 结构。

### D01 Card 数据

85%：str / index / function

15%：rank / suit 拆解

### D02 Combo 数据

85%：list / Card

15%：固定两张牌结构

### D03 Range 数据

85%：嵌套 list / Combo

15%：Range membership 与数量

### D04 Position → Range 映射

85%：dict / `.get()`

15%：多 position 映射

### D05 State 数据

85%：dict + str/list/int

15%：position / combo / stack / pot 混合类型

### D06 Action 数据

85%：if / str / dict

15%：Fold / Call / Raise 等合法动作集合

### D07 Preflop 最小 Decision Engine

85%：Range + State + if

15%：把多个字段组合成一次决策

### D08 多 Position Decision Engine

85%：decision engine

15%：BTN / CO / BB 不同 Range

### D09 数据结构一致性

85%：所有旧结构

15%：统一 Combo / Range schema

### D10 Poker 数据模型 Boss

从牌 → Combo → Range → State → Action 完整追踪，不运行代码预测结果。

---

# 8. Stage E — 工程化 Python

目标：从“学习代码”进入真正项目代码。

### E01 `import` / 模块
### E02 文件拆分
### E03 JSON 基础
### E04 保存 / 读取 Range 与 State
### E05 `assert` 最小测试
### E06 函数测试
### E07 错误信息 / traceback 阅读
### E08 类型提示基础
### E09 `dataclass`（在 dict 模型稳定之后再引入）
### E10 Poker Engine v1 工程化 Boss

每课仍保持 85% 已知项目代码 + 15% 新工程概念。

---

# 9. Stage F — Dataset 与数值计算

只有 Python / Poker 数据结构稳定后进入。

### F01 数据行：feature / label
### F02 list of records
### F03 NumPy array
### F04 `shape` / `dtype`
### F05 数组索引
### F06 向量化计算
### F07 Poker feature vector
### F08 Range frequency vector
### F09 Dataset 切分
### F10 Solver 样本 → Dataset Boss

---

# 10. Stage G — PyTorch / 神经网络

### G01 Tensor
### G02 shape / batch
### G03 `nn.Module`
### G04 `forward`
### G05 输入 x → 输出 y
### G06 loss
### G07 optimizer
### G08 training loop
### G09 validation
### G10 Poker Policy Model Boss

原则：每次只把上一课已经理解的数据流升级约 15%，不突然跳到完整训练框架。

---

# 11. Stage H — Solver-like AI

### H01 Policy / EV 输出
### H02 Combo-level prediction
### H03 Range-level aggregation
### H04 Solver `.cfr` 数据解析入口
### H05 Teacher → Dataset
### H06 Model prediction vs Solver target
### H07 Game Tree 最小结构
### H08 Regret / CFR 最小代码直觉
### H09 Search / Decision integration
### H10 Solver-like Poker GTO Intelligence Boss

---

# 12. 当前用户所在位置（2026-08-09）

已经见过很多 Stage B / C 内容，但最近交互测试说明 Stage A 的某些基础在“混合结构”里还没有完全自动化，因此**不按章节倒退重学，而是采用螺旋回补**。

当前重点：

```text
A03 嵌套 list              ◐
A04 dict                   ◐
A05 [] 上下文 / 索引       ◐
A06 in 当前层              ◐
A07 False vs TypeError     ◐
A08 .get()                 ◐
A09 布尔条件               下一小步
A10 if / else              已见过，待混合稳定
```

同时保留已经学过的：

```text
for / 两层 for / append / len / set
def / 参数 / return
create_card / create_deck / create_combo
```

这些不废弃，而是继续作为后续课的 85% 熟悉材料反复出现。

---

# 13. 每课自动调速规则

```text
100% / 连续全对
→ 下一课正常 +15%，Boss 稍复杂

80%～99%
→ 下一课仍 +15%，但把错题主题混入旧知识区

60%～79%
→ 新知识降到约 5%～10%，先补最弱层

<60%
→ 暂停新增，进入 Diagnose → Backfill → Re-test
```

重点不是追求快，而是确保每一层能支撑下一层。

---

# 14. 一句话课程架构

> **课程不是一条“学完就丢”的直线，而是一条不断复用旧代码、每次只扩张约 15%、课内再分层递进、最后回到 Poker Boss 的螺旋路线。**
