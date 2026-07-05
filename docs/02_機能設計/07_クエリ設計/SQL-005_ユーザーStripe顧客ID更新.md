# 1. 基本情報

| 項目 | 内容 |
|---|---|
| クエリID | SQL-005 |
| クエリ名 | ユーザーStripe顧客ID更新 |
| 概要 | 指定ユーザーの Stripe顧客ID(STRIPE_CUSTOMER_ID)を設定する。 |
| 用途 | 支払い方法登録(Checkout)時の Stripe Customer 保存。 |
| 使用元 | MOD-007 |

# 2. 対象テーブル

| テーブル | 物理名 | 用途 |
|---|---|---|
| TBL-001 | M_USERS | 更新対象(Stripe顧客IDの保存) |

# 3. 入力パラメータ

| パラメータ | 論理名 | 型 | 必須 | 説明・制約 |
|---|---|---|---|---|
| :id | ユーザーID | INTEGER | Yes | 更新対象ユーザーの ID |
| :stripe_customer_id | Stripe顧客ID | TEXT | Yes | Stripe で生成した Customer ID |
| :updated_at | 更新日時 | TEXT | Yes | ISO8601(UTC)。アプリで現在時刻を設定(共通カラム.md) |

# 4. クエリ

有効(DELETED_AT IS NULL)なユーザーの STRIPE_CUSTOMER_ID を設定する。更新後の識別値を返す。

```sql
UPDATE M_USERS
SET STRIPE_CUSTOMER_ID = :stripe_customer_id,
    UPDATED_AT         = :updated_at
WHERE ID = :id
  AND DELETED_AT IS NULL
RETURNING ID, STRIPE_CUSTOMER_ID;
```

# 5. 出力(列)

| 列名 | 論理名 | 型 | 説明 |
|---|---|---|---|
| ID | ユーザーID | INTEGER | 更新したユーザーの ID |
| STRIPE_CUSTOMER_ID | Stripe顧客ID | TEXT | 設定した Stripe顧客ID |

# 6. 補足(性能・インデックス)

| 項目 | 内容 |
|---|---|
| 利用インデックス | 主キー(ID)による一意更新 |
| 想定件数 | 最大1件 |
| 注意点 | UPDATED_AT はアプリで現在時刻を設定する(共通カラム.md)。Stripe 顧客未作成のユーザーに対してのみ呼び出す |
