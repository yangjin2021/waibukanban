# 项目式学习方法

本项目不是先学完整数学、完整 Python、完整 AI 再开始开发，而是始终围绕 Poker GTO Intelligence 的下一步功能学习。

## 每次继续项目时

默认读取：

`CURRENT_STATE.md`

教学展示规则：

1. 默认只显示 **小地图表格**。
2. 用户要求完整规划时，再显示大地图。
3. 先看当前已验证进度，再进入下一小课。

## 固定教学循环

每个知识点按以下顺序：

1. **先看到项目问题**：当前功能为什么需要这个知识。
2. **大白话解释**：先理解直觉，不先堆公式。
3. **只补当前最少数学**：不做无关扩展。
4. **手算一个例子**：确认概念不是只会背。
5. **学习一点 Python**：只学马上要用的语法。
6. **亲手写几行代码**：不一次给几百行工程代码。
7. **加入 Poker AI 项目**：知识立刻变成功能。
8. **做一个小练习**：检查是否真正掌握。
9. **复盘错误 / 疑问**。
10. **进入下一个功能**。

## Python 教学代码格式

以后提供代码时：

- 伪代码逻辑和正式 Python 代码放在同一个代码块。
- 使用 `# 中文注释` 描述“人话逻辑”。
- 注释用于学习，不通过 `print()` 输出。
- 保持程序实际运行结果干净。
- 重点解释：为什么这样写、不这样写会怎样。

示例：

```python
# 对每一个点数，都执行下面的事情
for rank in ranks:

    # 当前点数，再和所有花色组合
    for suit in suits:

        # 拼成一张牌
        card = rank + suit
```

## 当前开发方式

默认使用：

- IDE：PyCharm
- 运行方式：PyCharm Run
- PowerShell：用于路径、Git、环境排查

不要假设用户仍然在上一次终端目录。

常用恢复：

- CMD：`cd /d C:\PokerGTOAI`
- PowerShell：`cd C:\PokerGTOAI`

## 数学按项目需要出现

```text
百分数        → Range frequency
概率          → Strategy
组合          → 1326 Combos
加权平均      → Range EV
向量          → [Check, B33, B66, B100]
矩阵          → Batch / Range Data
函数          → AI(x) = y
平方 / 误差   → Loss
导数          → Gradient
链式法则      → Backpropagation
概率分布      → Softmax
条件概率      → Range Update
```

不单独刷完整大学数学课程；遇到项目需要时补齐。

## Python 也围绕扑克学

例如：

- 变量：`pot = 6`、`stack = 147`
- list：`actions = ["check", "b33", "b66", "b100"]`
- for：遍历 hero range 中的 Combo
- dict：保存每个 Action 的频率和 EV
- 文件 / 进程：控制 PioSolver、读取 `.cfr` 输出

## 暂时不提前学习的内容

除非项目真的遇到需求，否则不优先系统学习：

- CNN / ResNet
- 图像识别
- NLP / LLM
- 语音
- 生成式图像
- 大型 Transformer

## CFR 的学习位置

CFR 不放在项目最前面。

先利用现有 Solver 作为教师数据，完成第一个能泛化的神经模型后，再学习：

`博弈论 → Nash → Regret → Regret Matching → CFR → CFR+ / DCFR / MCCFR`

## 学习成果必须变成项目资产

每次课程至少留下一个可追踪成果之一：

- 新代码
- 新测试
- 新数据样本
- 新模型
- 新实验记录
- 新文档
- 进度状态更新

每完成一个可验证的小步骤，优先更新 `CURRENT_STATE.md`；只有领域信息变化时，再更新对应详细文档。

目标不是“上完课程”，而是让 Poker GTO Intelligence 每次都向前一步。
