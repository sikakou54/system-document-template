# 1. 概要

シーケンス設計から画面・JOB・API・モジュール・クエリ・データモデル・テーブル・エラー・メッセージへの対応を一元管理する。
個別設計書には直接使用する根拠・依存IDだけを記載し、下位成果物や利用元の網羅一覧は本表を正本とする。

# 2. 対応表

| SEQ ID | SCR | JOB | API | MOD | SQL | MDL | TBL | ERR | MSG | 権限・外部IF反映先 | 状態 |
|---|---|---|---|---|---|---|---|---|---|---|---|
| SEQ-001 | SCR-003, SCR-007 | - | API-003 | MOD-002, MOD-003, MOD-007 | SQL-004, SQL-008, SQL-009, SQL-022, SQL-025 | MDL-001, MDL-002, MDL-003 | TBL-001, TBL-002, TBL-003 | ERR-003, ERR-004, ERR-006, ERR-007, ERR-008, ERR-010 | MSG-001, MSG-003, MSG-005, MSG-006, MSG-014, MSG-016 | CFR-001, CFR-002／外部IFなし | 確定 |
| SEQ-002 | - | JOB-001 | - | MOD-006 | SQL-004, SQL-024, SQL-028 | MDL-001, MDL-003 | TBL-001, TBL-003 | - | - | システム実行権限／概要設計のResend連携・MOD-006 | 確定 |
| SEQ-003 | - | JOB-002 | API-011 | MOD-007 | SQL-004, SQL-021, SQL-031, SQL-032, SQL-033, SQL-035 | MDL-001, MDL-002, MDL-003, MDL-006, MDL-007 | TBL-001, TBL-002, TBL-003, TBL-007, TBL-008 | ERR-009 | - | Stripe署名検証／概要設計のStripe連携・API-011・MOD-007 | 確定 |
| SEQ-004 | SCR-007 | - | API-010, API-011, API-012 | MOD-007 | SQL-004, SQL-005, SQL-006, SQL-007 | MDL-001 | TBL-001 | ERR-009 | MSG-013, MSG-029, MSG-030 | CFR-001, CFR-002／概要設計のStripe連携・API-010・API-011・MOD-007 | 確定 |
| SEQ-005 | SCR-001 | - | API-001 | MOD-001, MOD-008 | SQL-003 | MDL-001 | TBL-001 | ERR-001, ERR-006 | MSG-004, MSG-027, MSG-028 | CFR-001／外部IFなし | 確定 |
| SEQ-006 | SCR-002 | - | API-002, API-009 | MOD-002, MOD-004 | SQL-001, SQL-013, SQL-016 | MDL-002, MDL-003, MDL-004, MDL-008 | TBL-002, TBL-003, TBL-004, TBL-005 | ERR-001, ERR-006 | MSG-007, MSG-008, MSG-009, MSG-015 | CFR-002, CFR-005／外部IFなし | 確定 |
| SEQ-007 | SCR-004 | - | API-004, API-006 | MOD-003 | SQL-009, SQL-020, SQL-022, SQL-023, SQL-026 | MDL-002, MDL-003 | TBL-002, TBL-003 | ERR-001, ERR-003, ERR-004, ERR-005, ERR-006 | MSG-017, MSG-018, MSG-032, MSG-033, MSG-034, MSG-035 | CFR-002／外部IFなし | 確定 |
| SEQ-008 | SCR-004 | - | API-005 | MOD-003 | SQL-020, SQL-027 | MDL-002, MDL-003 | TBL-002, TBL-003 | ERR-001, ERR-005 | MSG-002, MSG-017, MSG-019 | CFR-002／外部IFなし | 確定 |
| SEQ-009 | SCR-005 | - | API-007, API-009, API-013, API-014 | MOD-004 | SQL-008, SQL-010, SQL-011, SQL-012, SQL-014, SQL-015, SQL-016, SQL-017, SQL-018, SQL-019, SQL-037 | MDL-002, MDL-004, MDL-008 | TBL-002, TBL-004, TBL-005 | ERR-001, ERR-002, ERR-006, ERR-007, ERR-011 | MSG-010, MSG-011, MSG-020, MSG-021, MSG-022, MSG-023, MSG-024 | CFR-002／外部IFなし | 確定 |
| SEQ-010 | SCR-006 | JOB-003 | API-008 | MOD-005 | SQL-030 | MDL-002, MDL-005 | TBL-002, TBL-006 | ERR-001, ERR-002, ERR-006 | MSG-025, MSG-026 | CFR-002／外部IFなし | 確定 |
| SEQ-011 | SCR-007 | - | API-012 | MOD-007 | SQL-034, SQL-036 | MDL-006, MDL-007 | TBL-007, TBL-008 | ERR-001, ERR-006 | - | CFR-002／外部IFなし | 確定 |

# 3. 更新ルール

| 更新契機 | 更新内容 |
|---|---|
| SEQの作成・変更 | 参加者、データ参照更新、ERR/MSG、権限・外部IFの落とし込み先を更新する |
| 下位設計IDの予約 | 該当列へ予約IDを追加し、状態を「未着手」にする |
| 下位設計の作成・変更 | SEQとの責務・順序・CRUDを照合し、該当列と状態を更新する |
| ID廃止 | IDを削除せず、備考または状態に「廃止」を記録する |

- 本表はSEQ→各設計対応の正本であり、関連文書の作成・更新と同一作業内で更新する。
