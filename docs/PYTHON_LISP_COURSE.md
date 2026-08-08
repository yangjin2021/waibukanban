# Python + Common Lisp 双语言课程路线

更新时间：2026-08-08

## 1. 总原则

Poker GTO Intelligence 的**正式工程主线继续使用 Python**；新增 **Common Lisp（SBCL）学习副线**。

目标不是把 Python 项目机械翻译成 Lisp，而是：

```text
Python：负责真正落地项目、数据处理、Solver、NumPy / PyTorch / AI
Common Lisp：负责训练函数、表达式、递归、组合、符号处理和“代码即数据”的思维

同一个 Poker 问题
    ↓
先看最小核心
    ↓
Python 实现
    ↓
Common Lisp 对照
    ↓
比较两种语言的结构
    ↓
把更清晰的逻辑带回 Python 正式项目
```

## 2. 项目目录规划

正式 Python 代码保留：

```text
C:\PokerGTOAI\src\main.py
```

Common Lisp 学习代码计划新增：

```text
C:\PokerGTOAI\lisp\main.lisp
```

推荐运行环境：

- IDE：PyCharm（继续作为统一编辑器）
- Python：PyCharm Run
- Common Lisp：SBCL；初期可直接从 PyCharm Terminal 运行
- Lisp IDE 插件：可选，不作为课程开始的前置条件

在 SBCL 尚未实际安装 / 验证前，不把 Lisp 环境写成“已完成”。

## 3. 当前课程结构

### Track P — Python 主线

当前目标：完成 Card Engine 第一版，并继续进入 Poker 表示、Combo、Range、Solver 数据和 AI。

| P 课次 | 内容 | 状态 |
|---:|---|:---:|
| P01 | 变量 / 字符串 / print | ● |
| P02 | 字符串索引：Rank / Suit | ● |
| P03 | list | ● |
| P04 | for | ● |
| P05 | 两层 for：Rank × Suit | ● |
| P06 | deck / append / len / set | ● |
| P07 | def / 参数 / return | ● |
| P08 | `card(rank, suit)` 最小函数 | ● |
| P09 | `create_deck()`：函数内部建立 deck | ● |
| P10 | `create_deck()`：两层循环生成 52 张 | ● 已有 PyCharm 验证记录 |
| P11 | **函数组合：`create_deck()` 调用 `create_card()`** | ◐ 当前 Python 知识点 |
| P12 | Card Engine 第一版整理 | ○ |
| P13 | 条件判断 / Card 合法性检查 | ○ |
| P14 | dict / 更结构化 Card 表示 | ○ |

### Track L — Common Lisp 副线

Lisp 不从无关的 Hello World 独立重学，而是尽量复用已经理解的 Poker 概念。

| L 课次 | 内容 | 对应 Python |
|---:|---|---|
| L00 | 安装并验证 SBCL；在 PyCharm 中运行 `.lisp` | 开发环境 |
| L01 | S-expression / 表达式：谁包着谁 | Python 调用 / 缩进结构 |
| L02 | 值、字符串、列表 | Python string / list |
| L03 | `defun`：定义 `card` | Python `def card(...)` |
| L04 | Lisp 函数的输入与返回值 | Python 参数 / `return` |
| L05 | `let`：局部绑定 | Python 局部变量 |
| L06 | `dolist` / `loop`：遍历 suits | Python `for` |
| L07 | 嵌套遍历：Rank × Suit | Python 两层 `for` |
| L08 | Lisp 版最小 Deck | Python `create_deck()` |
| L09 | 递归版 Deck / 列表处理 | Python 循环视角对照 |
| L10 | 高阶函数 / map 思维 | Python 映射与数据加工 |
| L11 | 宏与 code-as-data 入门 | Python AST / 装饰器概念的远期对照 |

## 4. 双轨同步方式

不是一节 Python、一节 Lisp 永远机械交替。

默认节奏：

```text
Python 学到一个稳定概念
↓
需要时用 Lisp 重看同一个骨架
↓
比较两种表达
↓
回到 Python 项目继续前进
```

### 当前同步点

Python 已经理解：

```python
def card(rank, suit):
    return rank + suit
```

所以 Lisp 的第一段正式课程会围绕“同一个 card 功能”展开，而不是重新讲变量是什么。

注意：Common Lisp 的字符串拼接语法与 Python 不同，因此对照时保持**功能语义相同**，不要求字符级一一对应。

## 5. 教学格式

每次默认：

1. 只显示当前小地图。
2. **真正可运行的代码放最上面**，不把大量中文注释塞进代码。
3. 如果代码看不懂，先压缩到不能再压的最小核心。
4. 代码下面再解释：
   - 功能名字
   - 输入
   - 处理
   - 输出
   - 执行顺序 / 数据流
5. 再需要时补 PyCharm 颜色 / 灰色提示解释。
6. 双语言课时，再增加 Python ↔ Lisp 对照；不要一次引入多个 Lisp 新概念。
7. 用户理解后才补下一层，最后回到完整 Poker 项目代码。

## 6. Python 与 Lisp 的角色边界

### Python 必须保持主线的部分

后续以下模块默认使用 Python：

- 文件与数据清洗
- NumPy / Pandas
- PioSolver 或其他 Solver 数据接口
- 大规模 Dataset
- PyTorch / JAX
- GPU 训练
- Policy / Value Model
- 模型评估与实验

### Lisp 特别适合辅助的部分

- 函数与表达式结构
- 递归
- 树与搜索
- 状态变换
- 符号规则
- DSL
- 宏
- code-as-data
- CFR / 博弈树算法的概念原型（按需要）

如果 Lisp 写法在某一课反而增加认知负担，就暂时跳过 Lisp，对应概念继续用 Python 学。

## 7. 近期课程顺序

从现在开始：

```text
1. L00：在现有 PokerGTOAI 项目中建立 lisp/ 并验证 SBCL
2. L01：用最小 Lisp 表达式理解 S-expression
3. L03/L04：把已经熟悉的 card(rank, suit) 改写成 Common Lisp
4. 回 Python P11：create_deck 调用 create_card
5. Python / Lisp 各做一个最小 Deck
6. 对比 for / dolist、局部变量、返回值
7. 整理 Python Card Engine 第一版
8. 进入 Poker Card 表示与 Combo Engine
```

## 8. 判断是否真正学会

不以“背语法”为主，优先看能否：

```text
看到代码
→ 找出功能名字 / 输入 / 处理 / 输出
→ 预测数据怎么流
→ 用另一门语言表达同一个逻辑
→ 回到 Python 项目正确使用
```

最终目标不是成为“会两套语法的人”，而是形成可以跨语言迁移的程序结构能力。