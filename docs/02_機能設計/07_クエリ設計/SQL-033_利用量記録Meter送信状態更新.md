# 1. 基本情報

| 項目 | 内容 |
|---|---|
| クエリID | SQL-033 |
| クエリ名 | 利用量記録Meter送信状態更新 |
| 概要 | 利用量記録1件の Stripe Meter Event ID・計上ステータスを更新する。 |
| 用途 | Stripe Meter Event 送信後の状態更新(送信済 / 失敗)。 |
| 使用元 | MOD-007 |

# 2. 対象テーブル

| テーブル | 物理名 | 用途 |
|---|---|---|
| TBL-007 | T_USAGE_RECORDS | 更新対象(送信状態・Meter Event ID の UPDATE) |

# 3. 入力パラメータ

| パラメータ | 論理名 | 型 | 必須 | 説明・制約 |
|---|---|---|---|---|
| :id | 利用量記録ID | INTEGER | Yes | 更新対象の利用量記録 ID |
| :stripe_meter_event_id | Stripe Meter Event ID | TEXT | No | 送信成功時に記録。失敗時は NULL |
| :status | 計上ステータス | INTEGER | Yes | 2=送信済 / 3=失敗(TBL-007/ENM-1) |
| :updated_at | 更新日時 | TEXT | Yes | ISO8601(UTC)。アプリで現在時刻を設定(共通カラム.md) |

# 4. クエリ

有効(DELETED_AT IS NULL)な利用量記録の STRIPE_METER_EVENT_ID・STATUS を更新する。

```sql
UPDATE T_USAGE_RECORDS
SET STRIPE_METER_EVENT_ID = :stripe_meter_event_id,
    STATUS                = :status,                 -- 2=送信済 / 3=失敗(TBL-007/ENM-1)
    UPDATED_AT            = :updated_at
WHERE ID = :id
  AND DELETED_AT IS NULL
RETURNING ID, STATUS, STRIPE_METER_EVENT_ID;
```

# 5. 出力(列)

| 列名 | 論理名 | 型 | 説明 |
|---|---|---|---|
| ID | 利用量記録ID | INTEGER | 利用量記録の ID |
| STATUS | 計上ステータス | INTEGER | 更新後の計上ステータス(TBL-007/ENM-1) |
| STRIPE_METER_EVENT_ID | Stripe Meter Event ID | TEXT | 送信成功時の Meter Event ID(失敗時 NULL) |

# 6. 補足(性能・インデックス)

| 項目 | 内容 |
|---|---|
| 利用インデックス | 主キー(ID)による一意更新 |
| 想定件数 | 最大1件 |
| 注意点 | 送信成功時は STRIPE_METER_EVENT_ID を設定し STATUS=2、失敗時は STATUS=3(記録は残し JOB で再送対象)。UPDATED_AT はアプリで現在時刻を設定する |
