# SilentSafe

SilentSafe は **SilentStudio** が手がける、個人向けのシステムセキュリティ保護ソフトウェアです。

- **バージョン**: v1.0.0
- **プラットフォーム**: Windows

> 本リポジトリはプロジェクト紹介のみを目的としており、**ソースコードは含まれません**。

## 機能

- ファイル安全スキャン（マルチスレッド並列 + Rust 高速化拡張）
- リアルタイムシステム監視（Windows システムサービスとして登録、失敗時自動再起動、ソフト終了後も保護継続）
- 隔離管理
- 挙動保護（プロセス / レジストリ / ネットワーク）
- 深い注入検出（ETW-TI）
- カスペルスキー風 UX：保護はデフォルトで全オン、結果のみ表示、技術的詳細は非表示

## 技術スタック

Python + PySide6 + QFluentWidgets + C++ スキャンエンジン + Rust 高速化拡張

---

## 著作権表示

**Copyright © SilentStudio**

本ソフトウェア（SilentStudio 傘下の関連製品・プロジェクト）の一部の公開コンポーネント（例：SDK サンプル、一部のフロントエンドコード、コミュニティ提供モジュール）は、特定の条件を満たす場合、GNU Affero General Public License (AGPL) v3.0 およびその補足条項が適用される場合があります。

コアエンジン（例：SilentSecurityEngine）、クラウドサービス（SSDBS）、およびオープンソースと明示されていない部分は、著作権法により保護されています。SilentStudio の書面による事前の同意なしに、これらの部分の複製、改変、リバースエンジニアリング、商用配布は固く禁じられています。

---

## チーム

SilentStudio は SilentCodeTeams の上位組織として、以下のサブチームの開発・運営を統括しています：

- SilentSafeGroup
- SilentNet.
- SilentCodeTeamsDev.

**Produced by SilentStudio.**
