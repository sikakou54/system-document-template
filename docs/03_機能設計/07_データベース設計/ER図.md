# 1. 概要

MeetRoom の全テーブル間のリレーションを示す。

- 各テーブルのカラム定義の正本は 07_データベース設計/ 配下の各 TBL 文書(共通カラムは 共通カラム.md)であり、本図には主要カラムのみ記載する。
- 型は Cloudflare D1(SQLite)方針(INTEGER / TEXT)。

# 2. ER図

```mermaid
erDiagram
    M_USERS ||--o{ T_RESERVATIONS : "予約する"
    M_ROOMS ||--o{ T_RESERVATIONS : "予約対象"
    M_ROOMS ||--o{ M_ROOM_EQUIPMENTS : "設備を持つ"
    M_EQUIPMENTS ||--o{ M_ROOM_EQUIPMENTS : "設置される"
    M_ROOMS ||--o{ T_USAGE_REPORTS : "実績集計対象"
    M_USERS ||--o{ T_USAGE_RECORDS : "利用量計上対象"
    M_ROOMS ||--o{ T_USAGE_RECORDS : "利用対象"
    T_RESERVATIONS ||--o| T_USAGE_RECORDS : "利用量記録"
    M_USERS ||--o{ T_INVOICES : "請求先"

    M_USERS {
        integer ID PK
        text NAME
        text EMAIL UK
        text PASSWORD_HASH
        integer ROLE
        text STRIPE_CUSTOMER_ID
        text STRIPE_SUBSCRIPTION_ID
        integer BILLING_STATUS
    }
    M_ROOMS {
        integer ID PK
        text NAME
        integer CAPACITY
        text LOCATION
        integer HOURLY_RATE
        integer STATUS
    }
    T_RESERVATIONS {
        integer ID PK
        integer ROOM_ID FK
        integer USER_ID FK
        text TITLE
        text START_AT
        text END_AT
        integer STATUS
        integer REMIND_STATUS
    }
    M_EQUIPMENTS {
        integer ID PK
        text NAME
    }
    M_ROOM_EQUIPMENTS {
        integer ID PK
        integer ROOM_ID FK
        integer EQUIPMENT_ID FK
    }
    T_USAGE_REPORTS {
        integer ID PK
        integer ROOM_ID FK
        text TARGET_MONTH
        integer RESERVATION_COUNT
        integer TOTAL_MINUTES
    }
    T_USAGE_RECORDS {
        integer ID PK
        integer RESERVATION_ID FK
        integer USER_ID FK
        integer ROOM_ID FK
        integer USAGE_MINUTES
        integer UNIT_PRICE
        integer AMOUNT
        text STRIPE_METER_EVENT_ID
        integer STATUS
    }
    T_INVOICES {
        integer ID PK
        integer USER_ID FK
        text STRIPE_INVOICE_ID UK
        text BILLING_PERIOD
        integer AMOUNT
        integer STATUS
    }
```

# 3. リレーション一覧

| 親 | 子 | 関係 | 説明 |
|---|---|---|---|
| M_USERS(TBL-001) | T_RESERVATIONS(TBL-003) | 1 : N | ユーザーは複数の予約を持つ(T_RESERVATIONS.USER_ID) |
| M_ROOMS(TBL-002) | T_RESERVATIONS(TBL-003) | 1 : N | 会議室は複数の予約を持つ(T_RESERVATIONS.ROOM_ID) |
| M_ROOMS(TBL-002) | M_ROOM_EQUIPMENTS(TBL-005) | 1 : N | 会議室と設備の中間テーブル(M_ROOM_EQUIPMENTS.ROOM_ID) |
| M_EQUIPMENTS(TBL-004) | M_ROOM_EQUIPMENTS(TBL-005) | 1 : N | 設備と会議室の中間テーブル(M_ROOM_EQUIPMENTS.EQUIPMENT_ID) |
| M_ROOMS(TBL-002) | T_USAGE_REPORTS(TBL-006) | 1 : N | 会議室×月の利用実績集計(T_USAGE_REPORTS.ROOM_ID) |
| M_USERS(TBL-001) | T_USAGE_RECORDS(TBL-007) | 1 : N | ユーザーは複数の利用量記録を持つ(T_USAGE_RECORDS.USER_ID) |
| M_ROOMS(TBL-002) | T_USAGE_RECORDS(TBL-007) | 1 : N | 会議室は複数の利用量記録を持つ(T_USAGE_RECORDS.ROOM_ID) |
| T_RESERVATIONS(TBL-003) | T_USAGE_RECORDS(TBL-007) | 1 : 0..1 | 完了予約ごとに利用量記録を1件計上(T_USAGE_RECORDS.RESERVATION_ID、UNIQUE) |
| M_USERS(TBL-001) | T_INVOICES(TBL-008) | 1 : N | ユーザーは複数の請求を持つ(T_INVOICES.USER_ID) |
