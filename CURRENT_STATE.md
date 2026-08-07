# Poker GTO Intelligence — Current State

> **默认恢复入口。** 当用户说“查看当前进度 / 继续项目 / 教我下一阶段”时，优先只读取本文件。除非问题需要更详细参数，否则不要默认加载整个仓库。

更新时间：2026-08-07

状态：`● 已完成` · `◐ 当前进行` · `○ 未开始`

## 1. 大地图进度

| Phase | 模块 | 状态 |
|---:|---|:---:|
| 00 | 零基础地基 / 开发环境 | ◐ 收尾 |
| 01 | Python 入门 | ◐ 当前 |
| 02 | 扑克牌表示 | ○ |
| 03 | Combo Engine（1326） | ○ |
| 04 | Range Engine | ○ |
| 05 | Solver 数据读取 | ○ |
| 06 | GTO Dataset | ○ |
| 07 | 第一次机器学习 | ○ |
| 08 | 神经网络 / PokerAI 0.1 | ○ |
| 09 | Policy Model | ○ |
| 10 | Value / EV Model | ○ |
| 11 | Range Intelligence | ○ |
| 12 | 未见 Flop 泛化 | ○ |
| 13 | Turn / River 多街 | ○ |
| 14 | Solver 级验证 | ○ |
| 15 | 多 Range / 多配置 | ○ |
| 16 | 多 Stack / 多位置 | ○ |
| 17 | 高级 AI（按需） | ○ |
| 18 | CFR / 博弈论深入 | ○ |
| 19 | Fast GTO Engine | ○ |

当前交界：**Phase 00 收尾 → Phase 01 Python 入门**。

## 2. 小地图进度

| 当前任务 | 状态 |
|---|:---:|
| Python / GPU / 本地项目目录建立 | ● |
| `src/main.py` 创建并运行 | ● |
| `card = "As"` 并成功输出 `As` | ● |
| 区分 Terminal / PowerShell / CMD 与 Python 代码 | ◐ |
| 理解变量、赋值 `=`、字符串、`print()` | ◐ |
| 自己把 `As` 改成 `Kh` 并验证 | ○ 下一步 |
| 拆解 `Rank / Suit` | ○ |
| 生成 52 张牌 Deck | ○ |

当前 Sprint 过关标准：能从任意新终端回到项目，能读懂并修改最简单 Python，并最终生成/打印 52 张牌。

## 3. 相关代码

### 最后一次已验证代码

文件：`C:\PokerGTOAI\src\main.py`

```python
card = "As"
print(card)
```

已验证输出：`As`

### 下一步目标代码（尚未验证）

```python
card = "Kh"
print(card)
print("card")
```

| 操作 | 命令 |
|---|---|
| CMD 回项目 | `cd /d C:\PokerGTOAI` |
| PowerShell 回项目 | `cd C:\PokerGTOAI` |
| 打开文件 | `notepad .\src\main.py` |
| 运行 | `python .\src\main.py` |
| 目标输出 | `Kh` / `card` |

> 注意：“最后已验证代码”与“下一步目标代码”必须分开，不能把尚未由用户运行确认的代码写成已完成。

## 4. 简单学习总结

目前已经学到 / 正在巩固：

- Terminal 是运行命令的入口；CMD / PowerShell 与 Python 是不同解释环境。
- Python 代码优先写进 `.py` 文件，再用 `python 文件.py` 执行。
- `card = "As"`：把字符串 `"As"` 赋给变量 `card`。
- `print(card)`：读取变量内容；`print("card")`：直接打印文字 `card`。
- 相对路径依赖当前目录；新开终端时先回到 `C:\PokerGTOAI`。
- 路径和拼写必须准确：项目代码在 `src\main.py`，不是根目录的 `main.py`。

下一知识点：**用 `Kh` 拆出 `K = Rank`、`h = Suit`，开始真正的 Card Engine。**

## 更新规则

每完成一个可验证的小步骤，优先更新本文件。只有涉及详细阶段规划、环境、Bug、模型或技术规范时，再同步更新对应详细文档。
