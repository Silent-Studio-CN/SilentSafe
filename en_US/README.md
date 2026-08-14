# SilentSafe

SilentSafe is a system security protection tool for personal devices, produced by **SilentStudio**.

- **Version**: v1.0.0
- **Platform**: Windows

> This repository is for project showcase only and does **not** contain source code.

## Features

- File security scanning (multithreaded + Rust-accelerated)
- Real-time system monitoring (registered as a Windows system service; auto-restarts on failure; protection continues even after the app exits)
- Quarantine management
- Behavior protection (process / registry / network)
- Deep injection detection (ETW-TI)
- Protection fully on by default; the UI shows results only and hides technical details

## Tech Stack

Python + PySide6 + QFluentWidgets + C++ scan engine + Rust acceleration extension

## Architecture

- **UI layer**: Python + PySide6 + QFluentWidgets; multi-page navigation (Home / Security Advice / Scan / Protection / Behavior / Quarantine / Notices / Settings); light/dark theme and accent color; instant zh/en language switching.
- **Scan engine**: C++ (SilentSecurityEngine), multithreaded parallel scanning, streams progress and results as line-delimited JSON (JSONL); single-file / directory / full-disk modes.
- **Acceleration**: Rust (`ss_rust.pyd`, PyO3) batch-parses and aggregates engine JSONL output, roughly 3x faster than line-by-line Python parsing; falls back to pure Python seamlessly when absent.
- **Real-time monitoring**: Windows `ReadDirectoryChangesW` event-driven, recursive on all fixed disks; confirmed signature hits are auto-deleted, heuristic hits are auto-quarantined.
- **Behavior monitoring**: process creation is event-driven via ETW (0 latency, behind `NtCreateProcess`; falls back to polling when unavailable); registry autorun and outbound connections are detected by snapshot diff; events carry PID / parent PID / behavior chain.
- **System service**: the engine is registered as a Windows service (SCM-managed, auto-start on boot) with a failure-restart policy (5s / 10s / 60s); decoupled from the UI process — protection continues after exit, and SCM restarts it if the process is killed.
- **Sandbox**: high-risk executables that fail quarantine are automatically detonated in a sandboxed process, re-judged from the sampled behavior, then quarantined again on a malicious verdict.
- **Signature verification**: offline WinVerifyTrust Authenticode validation + signer extraction (no revocation check, no network); valid Microsoft / Google signatures are fully trusted and skipped, other valid signatures are downgraded with signer info attached.
- **Deep injection detection**: ETW-TI (AutoLogger kernel session, Windows 11).
- **Communication model**: UI and engine are decoupled via JSONL — stdout pipe for scans; in service mode, monitor/behavior events are written to event files and read incrementally by the UI.
- **Quarantine**: files are moved into a quarantine directory and renamed to prevent re-execution; list / restore / delete supported; quarantine and log directories are skipped by the scanner to avoid re-reporting.

---

## Copyright

**Copyright © SilentStudio**

Some publicly available components of this software (e.g., SDK examples, parts of frontend code, or community-contributed modules) may be subject to the GNU Affero General Public License (AGPL) v3.0 and its supplemental terms when specific conditions are met.

The core engines (e.g., SilentSecurityEngine), cloud services (SSDBS), and any parts not explicitly marked as Open Source are protected by copyright laws. Unauthorized reproduction, modification, reverse engineering, or commercial distribution of these parts is strictly prohibited without prior written consent from SilentStudio.

---

## Team

SilentStudio, as the parent organization of SilentCodeTeams, oversees the development and operations of the following sub-teams:

- SilentSafeGroup
- SilentNet.
- SilentCodeTeamsDev.

**Produced by SilentStudio.**
