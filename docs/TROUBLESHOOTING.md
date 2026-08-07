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

另外，当时 PowerShell 的实际提示符显示当前目录仍为 `System32`，说明还没有切换到 `C:\PokerGTOAI`。

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

`● 原因已确认；等待用户按正确 PowerShell 命令再次验证。`

---

后续真实遇到的问题继续按 `BUG-002 / BUG-003 ...` 追加。
