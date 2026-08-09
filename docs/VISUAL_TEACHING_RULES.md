# 视觉化 Python 教学规则

更新时间：2026-08-09

## 核心原则

以后 HTML / 交互式 Python 课程不只使用“代码 + 文字 + 题目”，还要在合适的位置加入真正的图形层。

> 图不是装饰，而是代码执行结构的另一种表示。

所有图都必须能够回指到具体 Python 代码中的变量、容器、函数、循环、条件或数据流，不能画成脱离代码的抽象概念图。

## 默认加入的图形类型

### 1. 数据结构图

适用于：`str`、`list`、嵌套 list、dict、Combo、Range、State。

例如：

```text
Range
├─ Combo
│  ├─ Card
│  └─ Card
└─ Combo
   ├─ Card
   └─ Card
```

重点表现：最外层、当前层、直接元素、嵌套关系。

### 2. 数据流箭头图

适用于：赋值、dict 取值、`.get()`、函数参数、`return`、State → Range → Action。

例如：

```text
state["position"]
↓
"CO"
↓
ranges.get("CO", [])
↓
allowed_range
↓
filter_playable(...)
↓
result
```

### 3. 循环逐轮图

适用于：`for`、两层 `for`、Range 遍历、Deck / Combo 生成。

图中应显示：

- 第 1 轮变量接到什么值
- 第 2 轮变量接到什么值
- 条件判断结果
- 是否执行 `append()`
- 如何进入下一轮

### 4. 条件分支图

适用于：`if / else`、`in`、`not in`、合法 / 非法 Combo、Play / Fold。

例如：

```text
combo in allowed_range ?
        ↓
   True     False
    ↓         ↓
 append     skip
```

### 5. 函数骨架图

适用于所有新函数。

默认对应四个骨架问题：

```text
输入
↓
函数名字
↓
处理
↓
return 输出
```

同时标记调用方是谁、结果由谁接住。

### 6. Poker 系统图

随着项目推进，逐渐使用：

```text
Card
↓
Combo
↓
Range
↓
State
↓
Decision Function
↓
Action
```

后续再扩展到：

```text
Solver Data
↓
Dataset
↓
Tensor / Batch
↓
Model
↓
Policy / EV
↓
Decision
```

## HTML 课程实现要求

如果课程使用 HTML：

- 优先用 SVG / HTML / CSS 绘制结构图和流程图。
- 图应清晰、响应式，并与代码放在相邻位置。
- 同一个变量在代码与图里名称保持一致。
- 箭头方向必须与真实数据流 / 执行方向一致。
- 图中的颜色只辅助分组，不替代 token / 类型解释。
- 不为了“好看”增加与当前知识无关的复杂动画。
- 可以加入轻量交互，例如点击某一轮循环、切换 position、查看不同 Range 的数据流。

## 与交互题的关系

图形层和交互题是并列辅助，不互相充当门锁。

默认结构可以是：

```text
代码
↓
图
↓
解释
↓
小题
↓
继续下一段代码
```

题目用于测量理解；图用于建立结构直觉。即使题目答错，课程内容也不默认锁住。

## 最终目标

逐步让用户具备三种互相转换的能力：

```text
看到 Python 代码
↔
脑中形成结构 / 数据流图
↔
看到图能重新写回 Python
```

这项能力最终服务于 Poker GTO AI 中越来越复杂的 Dataset、Model、Game Tree、CFR 与推理流程。
