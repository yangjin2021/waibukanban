# Poker GTO Intelligence — Troubleshooting Log

本文件记录开发过程中真实遇到的 Bug、原因和解决方法。目的不是只“修掉”，而是把排错经验沉淀成项目资产。

## BUG-001 — PowerShell 中把 CMD 提示符当成命令一起输入

**日期：** 2026-08-07  
**环境：** PowerShell 7.6.4 / Windows

### 现象

在 PowerShell 中输入：

```text
C:\PokerGTOAI>python src\main.py
```

得到错误：

```text
C:\PokerGTOAI>python: The term 'C:\PokerGTOAI>python' is not recognized ...
```

### 原因

`C:\PokerGTOAI>` 是 CMD 的提示符，用来显示“当前目录”，不是用户要输入的命令内容。

PowerShell 会把整段 `C:\PokerGTOAI>python` 当成一个命令名称，因此找不到。

### 正确做法

先切换目录：

```powershell
cd C:\PokerGTOAI
```

然后运行：

```powershell
python .\src\main.py
```

也可以在任何目录直接运行完整路径：

```powershell
python C:\PokerGTOAI\src\main.py
```

### 学到的知识

- Terminal 的“提示符”与“命令”是两回事。
- CMD 常见提示符：`C:\PokerGTOAI>`。
- PowerShell 提示符可能经过主题美化，显示更多图标、目录、Git 状态等。
- 教程中的提示符不应复制进命令本身。
- 运行相对路径前要确认当前工作目录。

### 状态

`● 已验证解决：PowerShell 中执行 python .\src\main.py 成功输出 As。`

---

## BUG-002 — 在 PowerShell 中直接输入 Python 代码 `print(card)`

**日期：** 2026-08-07  
**环境：** PowerShell 7.6.4 / Windows

### 现象

在普通 PowerShell 提示符中直接输入：

```text
print(card)
```

PowerShell 报错：

```text
card: The term 'card' is not recognized as a name of a cmdlet, function, script file, or executable program.
```

### 原因

当前窗口正在运行的是 **PowerShell 语言**，不是 Python 解释器。

`print(card)` 是 Python 代码。PowerShell 会按照自己的语法解释这一行，因此把 `card` 当成 PowerShell 中要执行 / 解析的名称，而不是 Python 变量。

另外，`card` 变量只存在于运行 `main.py` 的那次 Python 进程里；Python 程序结束后，它不会自动变成 PowerShell 变量。

### 正确做法 A — 推荐：把 Python 代码写进 `.py` 文件

编辑：

```powershell
notepad .\src\main.py
```

文件内容：

```python
card = "As"
print(card)
```

然后：

```powershell
python .\src\main.py
```

### 正确做法 B — 以后会学：先进入 Python 交互解释器

```powershell
python
```

看到 Python 的 `>>>` 提示符后，才可以逐行输入 Python：

```python
card = "As"
print(card)
```

退出可使用：

```python
exit()
```

当前项目教学优先采用 `.py` 文件方式，避免混淆 PowerShell 和 Python 两种语言。

### 学到的知识

- PowerShell 和 Python 是两种不同的语言 / 解释环境。
- Terminal 是“容器 / 入口”，里面当前是谁在解释命令很重要。
- `.py` 文件中的变量不会自动成为 PowerShell 变量。
- 看到 PowerShell 提示符时输入的是 PowerShell 命令；看到 Python `>>>` 时输入的才是 Python 代码。

### 状态

`● 原因已确认；项目本身正常，python .\src\main.py 已成功运行。`

---

## BUG-003 — 打开了错误的文件路径 / `src` 拼写错误

**日期：** 2026-08-07  
**环境：** PowerShell 7.6.4 / Windows

### 现象

用户依次输入过：

```powershell
notepad main.py
notepad scr main.py
```

### 原因

项目真正的 Python 文件位于：

```text
C:\PokerGTOAI\src\main.py
```

因此：

- `notepad main.py` 指向的是项目根目录的 `C:\PokerGTOAI\main.py`，不是已有的 `src\main.py`；如果不存在，记事本可能提示创建一个新的错误位置文件。
- `scr` 是拼写错误，正确目录名是 `src`（source 的缩写）。
- `notepad scr main.py` 中还有空格，可能会被当成多个独立参数 / 文件名，而不是 `src\main.py` 这条路径。

### 正确做法

在 `C:\PokerGTOAI` 下：

```powershell
notepad .\src\main.py
```

其中：

- `.` = 当前目录
- `\` = 进入下一层路径
- `src` = source code 目录
- `main.py` = Python 文件

### 学到的知识

- 文件名相同但路径不同，就是不同文件。
- `C:\PokerGTOAI\main.py` 和 `C:\PokerGTOAI\src\main.py` 不是同一个文件。
- 编程中路径和拼写必须准确。

### 状态

`● 原因已确认；后续统一使用 notepad .\src\main.py。`

---

## NOTE-001 — PowerShell 提示符显示 `CONFIG NOT FOUND`

目前这条文字来自 PowerShell 提示符 / 主题配置的可能性较高。它没有阻止 `python .\src\main.py` 成功执行，因此目前不属于 PokerGTOAI 的 Python 故障。

在后续如果它影响终端使用，再单独排查 PowerShell Profile / Prompt Theme 配置。

---

后续真实遇到的问题继续按 `BUG-004 / BUG-005 ...` 追加。
