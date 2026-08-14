# 静安（SilentSafe）

静安者，**SilentStudio** 所製，护个人机之安防软件也。

- **版本**：v1.0.0
- **平台**：Windows

> 此仓祗为示览，**不载源码**。

## 功能

- 档检：多线程并行，兼 Rust 提速
- 实时监：注册为 Windows 系统服务，败则自起；退软而不辍护
- 隔离之治
- 行止之护（进程 / 注册表 / 网络）
- 深探注入（ETW-TI）
- 防护默认全开，界面祗示结果，藏其技术之细

## 技术栈

Python + PySide6 + QFluentWidgets + C++ 检引擎 + Rust 提速扩

## 技术架构

- 界面层：Python + PySide6 + QFluentWidgets，多页导航（主页 / 安全建议 / 扫描 / 实时防护 / 行为防护 / 隔离区 / 通知 / 设置），明暗主题与主色，中英即时切换。
- 检引擎：C++（SilentSecurityEngine），多线程并行，逐行 JSON（JSONL）流式输出进度与结果；单档 / 目录 / 全盘诸模式。
- 提速扩：Rust（`ss_rust.pyd`，PyO3），批量解析聚合引擎之 JSONL，较 Python 逐行约三倍速；阙则自动回退纯 Python，语义无异。
- 实时监：Windows `ReadDirectoryChangesW` 事件驱动，递归监听诸固定盘；确认之威胁自动删除，启发命中自动隔离。
- 行为护：进程创建以 ETW 事件驱动（零延迟，对应 `NtCreateProcess`，阙则回退轮询）；注册表自启与出站连接以快照差异检测；事件携 PID / 父 PID / 行为链。
- 系统服务：引擎注册为 Windows 服务（SCM 管理，开机自启），失败自动重启（5s / 10s / 60s）；防护与界面解耦，退软不辍护，进程被终则 SCM 自动拉起。
- 沙箱：隔离失败之高危可执行文件自动入沙箱进程引爆分析，依所采行为二次判定，若判恶意则复试隔离。
- 签名验证：WinVerifyTrust 离线 Authenticode 校验并提取签名者（不查吊销、不联网）；微软 / 谷歌有效签名完全信任跳过，其余有效签名降级示以签名者。
- 深探注入：ETW-TI（AutoLogger 内核会话，Windows 11）。
- 通信模型：界面与引擎以 JSONL 解耦——扫描用 stdout 管道，服务模式下监控 / 行为事件写事件文件，供界面增量轮询。
- 隔离区：文件移入隔离目录并更名防再行，支持列表 / 恢复 / 删除；隔离区与日志目录为扫描器所略，免二次误报。

---

## 版权声明

**Copyright © SilentStudio**

凡本软件（SilentStudio 旗下诸产品及项目）之若干公开组件，若合特定之条件，或适 GNU Affero General Public License (AGPL) v3.0 与其补充条款。

至若核心引擎（如 SilentSecurityEngine）、云端诸服务（SSDBS）及凡未明标为开源者，皆依《中华人民共和国著作权法》及诸国际公约所护。非经 SilentStudio 书面之许，严禁复制、篡改、反工程及商用分发。

---

## 团队

SilentStudio 为 SilentCodeTeams 之上级组织，统辖下列诸子队之开发与运营：

- SilentSafeGroup
- SilentNet.
- SilentCodeTeamsDev.

**Produced by SilentStudio.**
