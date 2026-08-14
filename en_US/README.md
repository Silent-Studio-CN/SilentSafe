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
- Kaspersky-style UX: protection fully on by default, results only, technical details hidden

## Tech Stack

Python + PySide6 + QFluentWidgets + C++ scan engine + Rust acceleration extension

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
