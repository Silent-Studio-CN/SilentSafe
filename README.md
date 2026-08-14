# SilentSafe

SilentSafe 是一款面向个人设备的系统安全防护软件，由 **SilentStudio** 出品。

- **版本**：v1.0.0
- **平台**：Windows

> 本仓库仅用于项目展示，**不包含源代码**。

<details>
<summary>🌐 Supported Languages</summary>

- `https://github.com/Silent-Studio-CN/SilentSafe/tree/main/en_US`  · English (US)
- `https://github.com/Silent-Studio-CN/SilentSafe/tree/main/ja-JP`  · 日本語 (日本)
- `https://github.com/Silent-Studio-CN/SilentSafe/tree/main/ru-RU`  · Русский (Россия)
- `https://github.com/Silent-Studio-CN/SilentSafe/tree/main/es-ES`  · Español (España)
- `https://github.com/Silent-Studio-CN/SilentSafe/tree/main/fr-FR`  · Français (France)
- `https://github.com/Silent-Studio-CN/SilentSafe/tree/main/lzh`  · 文言文

</details>

## 功能特点

- 文件安全扫描（多线程并行 + Rust 加速扩展）
- 实时系统监控（注册为 Windows 系统服务，失败自动重启，退出软件防护继续运行）
- 文件隔离管理
- 行为防护（进程 / 注册表 / 网络）
- 深度注入检测（ETW-TI）
- 防护默认全开，界面只展示处理结果，隐藏技术细节

## 技术栈

Python + PySide6 + QFluentWidgets + C++ 扫描引擎 + Rust 加速扩展

## 技术架构

- **UI 层**：Python + PySide6 + QFluentWidgets，多页面导航（主页 / 安全建议 / 扫描 / 实时防护 / 行为防护 / 隔离区 / 通知 / 设置），支持亮暗主题与主题色、中英双语即时切换。
- **扫描引擎**：C++（SilentSecurityEngine），多线程并行扫描，以逐行 JSON（JSONL）流式输出进度与结果；单文件/目录/全盘多模式。
- **加速扩展**：Rust（`ss_rust.pyd`，PyO3），对引擎 JSONL 输出做批量解析与聚合，相对 Python 逐行解析约 3 倍提速；缺失时自动回退纯 Python 解析，语义一致。
- **实时监控**：Windows `ReadDirectoryChangesW` 事件驱动，所有固定磁盘递归监听；命中内置签名库的确认威胁自动删除，启发式命中自动隔离。
- **行为监控**：进程创建用 ETW 事件驱动（0 延迟，对应 `NtCreateProcess`，不可用时自动回退轮询）；注册表自启动与出站网络连接用快照差异检测；事件携带 PID / 父进程 / 行为链。
- **系统服务**：引擎注册为 Windows 服务（SCM 管理，开机自启），配置失败自动重启策略（5s / 10s / 60s）；防护与 UI 进程解耦，退出软件后防护继续运行，进程被结束后由 SCM 自动拉起。
- **沙箱**：对隔离失败的高危可执行文件自动送入沙箱进程引爆分析，按采样行为事件二次判定并再次尝试隔离。
- **签名验证**：WinVerifyTrust 离线 Authenticode 校验 + 签名者提取（不查吊销、不联网）；微软 / 谷歌有效签名完全信任跳过启发式，其余有效签名降级提示并附签名者信息。
- **深度注入检测**：ETW-TI（AutoLogger 内核会话，Windows 11），消费注入事件并展示拦截战果。
- **通信模型**：UI 与引擎通过 JSONL 解耦——扫描用 stdout 管道，服务模式下监控/行为事件写入事件文件供 UI 增量轮询。
- **隔离区**：文件移入隔离目录并重命名防再执行，支持列表 / 恢复 / 删除；隔离区与日志目录被扫描器主动跳过，避免二次误报。

---

## Copyright / 版权声明

**Copyright © SilentStudio**

本软件（指代 SilentStudio 旗下相关产品及项目）的部分公开组件（如 SDK 示例、部分前端代码或社区贡献模块）在满足特定条件时，可能适用 GNU Affero General Public License (AGPL) v3.0 及其补充条款。

对于核心引擎（如 SilentSecurityEngine）、云端服务（SSDBS）及未明确标注为开放源代码的部分，均依据《中华人民共和国著作权法》及相关国际公约予以保护。未经 SilentStudio 书面授权，严禁对该部分进行复制、修改、反向工程或商业性分发。

Some publicly available components of this software (e.g., SDK examples, parts of frontend code, or community-contributed modules) may be subject to the GNU Affero General Public License (AGPL) v3.0 and its supplemental terms when specific conditions are met.

The core engines (e.g., SilentSecurityEngine), cloud services (SSDBS), and any parts not explicitly marked as Open Source are protected by copyright laws. Unauthorized reproduction, modification, reverse engineering, or commercial distribution of these parts is strictly prohibited without prior written consent from SilentStudio.

---

## 出品团队

SilentStudio 是 SilentCodeTeams 的上级组织，统筹管理以下子团队的开发与运营：

- SilentSafeGroup
- SilentNet.
- SilentCodeTeamsDev.

**Produced by SilentStudio.**
