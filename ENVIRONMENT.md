# Poker GTO Intelligence — Environment

本文档集中记录当前本机研发环境。用途：安装依赖、排查训练问题、迁移电脑、验证 PyTorch/CUDA、规划数据路径。

> 安全规则：不在仓库中保存 Windows 产品 ID、设备 ID、密码、Token、私钥等敏感标识或凭据。

## 1. 当前硬件

| 项目 | 当前配置 | 状态 |
|---|---|:---:|
| CPU | Intel Core i5-12490F（12th Gen） | ● |
| RAM | 32 GB | ● |
| GPU | NVIDIA GeForce RTX 2060 SUPER | ● |
| GPU 显存 | 8 GB | ● |
| SSD | WD_BLACK SN750 SE 1 TB | ● |
| 系统 | Windows 64-bit / x64 | ● |

## 2. 当前软件 / GPU 环境

| 项目 | 当前值 | 状态 |
|---|---|:---:|
| Python | 3.12.10 | ● |
| PowerShell | 7.6.4 | ● |
| NVIDIA Driver | 560.94 | ● |
| `nvidia-smi` CUDA Version | 12.6 | ● |
| PyTorch | 尚未安装 / 尚未验证 | ○ |
| `torch.cuda.is_available()` | 尚未验证 | ○ |
| PyTorch 实际使用的 CUDA Runtime | 尚未验证 | ○ |

说明：`nvidia-smi` 显示的 CUDA 12.6 代表当前 NVIDIA 驱动能够支持的 CUDA 能力上限之一，不等同于“PyTorch 已经成功使用 CUDA”。PyTorch 安装后需要单独验证。

## 3. 当前项目路径

```text
C:\PokerGTOAI
├─ src
├─ data
├─ models
├─ tests
└─ logs
```

已验证：

```text
C:\PokerGTOAI\src\main.py
```

运行命令：

```text
python src\main.py
```

已验证输出：

```text
Poker GTO Intelligence Start
```

### CMD 与 PowerShell 提示符规则

命令示例中的 `C:\PokerGTOAI>` 只是 CMD 显示的“当前位置提示符”，**不是命令的一部分**。

正确：

```text
python src\main.py
```

错误：

```text
C:\PokerGTOAI>python src\main.py
```

在 PowerShell 中，如果当前不在项目目录，先执行：

```powershell
Set-Location C:\PokerGTOAI
```

或简写：

```powershell
cd C:\PokerGTOAI
```

再执行：

```powershell
python .\src\main.py
```

PowerShell 提示符可能由主题美化工具显示成多段内容；提示符文字本身都不要复制到命令中。

## 4. 存储状态与规则

最近一次确认：C 盘可用空间约 **34.7 GB**。

因此：

- `C:\PokerGTOAI`：只放代码、轻量配置、日志、小型测试数据。
- 大型 `.cfr` Solver 文件：保留在原位置，不复制到项目目录。
- 大型训练 Dataset：未来规划到容量更大的数据盘。
- 大型模型 checkpoint：未来规划到数据盘 / 模型盘。
- GitHub：只提交代码、文档、小型配置和关键实验结论；不提交 Solver 大文件、训练数据、大模型权重。

## 5. Solver / 数据路径登记

以下路径目前尚未确认，后续首次使用时再填写：

| 项目 | 路径 | 状态 |
|---|---|:---:|
| PioSolver 可执行文件 | `TODO` | ○ |
| 184 棵 `.cfr` 根目录 | `TODO` | ○ |
| 原始范围表目录 | `TODO` | ○ |
| 提取后的 Dataset 根目录 | `TODO` | ○ |
| 模型 checkpoint 根目录 | `TODO` | ○ |

## 6. 当前硬件开发策略

采用：**Small → Correct → Scale**。

- 先用小模型、少量树、较小 batch 跑通完整链路。
- RTX 2060 SUPER 8GB 足够完成 Python / Card / Combo / Range / Solver 数据提取和第一代小型神经网络实验。
- 后续只有在实验证明“模型继续增大能显著提高 Solver 拟合/泛化，但 8GB 显存成为明确瓶颈”时，才考虑 GPU 升级。
- 数据读取必须流式 / 分批，不把全部 Solver / Dataset 一次加载进 RAM 或 VRAM。

## 7. 环境变更规则

以下任何一项发生变化，都更新本文件：

- Python 版本
- PowerShell / Terminal 环境
- PyTorch 版本
- CUDA / NVIDIA Driver
- GPU / RAM / SSD
- Solver 路径
- Dataset 路径
- 模型保存路径
- 关键依赖包版本

本文件是项目的 **环境事实来源（Environment Source of Truth）**。
