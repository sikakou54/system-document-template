# 1. 概要

MeetRoom のデータベース設計を定義する。DB基盤は Cloudflare D1(SQLite)。テーブル一覧のほか、ER図は ER図.md、Enum(列挙値)は各テーブル文書の §5 で定義、共通カラムは 共通カラム.md、命名規則は 命名規則.md を参照。各テーブルの詳細は TBL-XXX_テーブル名.md に記載する。

# 2. 一覧

| ID | 名称 | 物理名 | 概要 |
|---|---|---|---|
| TBL-001 | ユーザーマスタ | M_USERS | ログインユーザー(従量課金の契約情報を含む) |
| TBL-002 | 会議室マスタ | M_ROOMS | 予約対象の会議室(利用単価を含む) |
| TBL-003 | 予約トランザクション | T_RESERVATIONS | 会議室の予約 |
| TBL-004 | 設備マスタ | M_EQUIPMENTS | プロジェクター等の設備マスタ |
| TBL-005 | 会議室設備マスタ | M_ROOM_EQUIPMENTS | 会議室と設備の中間テーブル |
| TBL-006 | 会議室利用実績トランザクション | T_USAGE_REPORTS | 会議室×月の利用実績集計 |
| TBL-007 | 利用量記録トランザクション | T_USAGE_RECORDS | 従量課金の利用量記録(Stripe Meter Event) |
| TBL-008 | 請求トランザクション | T_INVOICES | 月次請求(Stripe Invoice) |
