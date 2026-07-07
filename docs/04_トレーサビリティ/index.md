# 04_トレーサビリティ index

# 1. 概要

MeetRoom の要求〜要件〜設計のトレース経路を対応表で一元管理する。
リンクの正本は各文書のトレース欄・依存欄であり、本ディレクトリの各対応表は各文書の基本情報の転記で構成する(独自情報を書かない。docs/CLAUDE.md §6)。
上流→下流／下流→上流の追跡は各対応表のフィルタで行う。

# 2. 対応表一覧

| ファイル | 対象経路 | 目的 |
|---|---|---|
| traceability_rq_br_fr.md | RQ→BR→FR/CFR/NFR | 要求が業務要件を経て実現要件へ落ちているかを追跡する |
| traceability_br_fr_uc.md | BR→FR/CFR/NFR→UC | 業務要件が機能要件・共通機能要件・非機能要件・ユースケースへ落ちているかを追跡する |
| traceability_uc_design.md | UC→SCR/API | 各ユースケースを実現する画面・API を追跡する |
| traceability_fr_nfr.md | FR→CFR/NFR | 機能要件に適用される共通機能要件(CFR)・非機能要件(NFR)を追跡する |
| traceability_scr_api_db.md | SCR→API→MOD→TBL | 画面から API・モジュール・テーブルまでの実装連鎖を追跡する |

# 3. 更新ルール

- 各対応表は関連文書(要件・設計)の作成・更新と同一作業内で行を更新する(正本: docs/CLAUDE.md §6・§10-7)。
- 記載するIDはすべて実在するもの(各index.md／各文書のインライン定義に存在)に限る。採番・廃止の扱いは docs/99_その他/ID採番ルール に従う。
