# 1. 概要

MeetRoom の機能設計に関わるトレースを一元管理する。

- 要件(UC)を実現する画面・API の対応、画面から API・モジュール・テーブルまでの実装連鎖を追跡する。
- 要件定義に関わるトレース(要求RQ→要件、FR→CFR/NFR、機能×データの CRUD 相関)は 02_要件定義/04_トレーサビリティ/ で管理する。

# 2. 一覧

| ファイル | 対象経路 | 目的 |
|---|---|---|
| [traceability_uc_design.md](traceability_uc_design.md) | UC→SCR/API | 各システムユースケース(UC。各FR/CFR文書内に定義)を実現する画面・API を追跡する(要件→設計) |
| [traceability_scr_api_db.md](traceability_scr_api_db.md) | SCR→API→MOD→TBL | 画面から API・モジュール・テーブルまでの実装連鎖を追跡する |

# 3. 更新ルール

- 各対応表は関連文書(UC/SCR/API/MOD/TBL 等)の作成・更新と同一作業内で該当行を更新する(正本: docs/CLAUDE.md §6・§10-7)。
- 記載する ID はすべて実在するもの(各 index.md／各文書のインライン定義に存在)に限る。採番・廃止の扱いは docs/99_その他/ID採番ルール.md に従う。
