<!-- コピーして docs/03_機能設計/11_トレーサビリティ/index.md として使用 -->
<!-- 設計間マッピングは専用対応表を正本とし、個別設計書へ下位成果物・利用元の網羅一覧を重複記載しない -->

# 1. 概要

(機能設計層で追跡するFR/UC→SEQ→各設計の経路と目的を1〜3行で記載)

# 2. 一覧

| ファイル | 対象経路 | 目的 |
|---|---|---|
| [traceability_uc_sequence.md](traceability_uc_sequence.md) | RQ→FR/CFR→UC→SEQ | 機能要件・ユースケースとSEQ、SEQ省略理由を追跡する |
| [traceability_sequence_design.md](traceability_sequence_design.md) | SEQ→SCR/JOB/API/MOD/SQL/MDL/TBL/ERR/MSG | シーケンスから各個別設計への落とし込みを追跡する |

# 3. 更新ルール

- 対応表は `99_その他/テンプレート_トレーサビリティ.md` を用いて作成する。
- 関連するFR/CFR/UC/SEQまたは下位設計の作成・更新と同一作業内で該当行を更新する。
- 記載するIDは実在するか、各index.mdへ状態「未着手」で予約済みのものに限る。
- SEQを省略する場合も、FR/UC→SEQ表に対象と具体的な省略理由を記録する。
