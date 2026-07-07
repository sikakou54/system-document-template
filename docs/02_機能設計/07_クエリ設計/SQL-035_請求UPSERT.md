# 1. 基本情報

| 項目 | 内容 |
|---|---|
| クエリID | SQL-035 |
| クエリ名 | 請求UPSERT |
| 概要 | Stripe請求IDで請求を登録または状態更新する(1請求1行・冪等)。 |
| 用途 | Webhook(invoice.paid / payment_failed)による請求状態の反映(BillingService)。 |
| 使用元 | MOD-007 |

# 2. 対象テーブル

| テーブル | 物理名 | 用途 |
|---|---|---|
| TBL-008 | T_INVOICES | 保存対象(請求の UPSERT) |

# 3. 入力パラメータ

| パラメータ | 論理名 | 型 | 必須 | 説明・制約 |
|---|---|---|---|---|
| :user_id | ユーザーID | INTEGER | Yes | 請求対象の利用者ID(新規時に設定) |
| :stripe_invoice_id | Stripe請求ID | TEXT | Yes | Stripe の invoice ID。UX_INVOICES_STRIPE で一意 |
| :billing_period | 請求対象月 | TEXT | Yes | 'YYYY-MM' 形式(新規時に設定) |
| :amount | 請求金額 | INTEGER | Yes | 円(新規時に設定) |
| :status | 請求ステータス | INTEGER | Yes | DEF-001/CODE-007 |
| :updated_at | 更新日時 | TEXT | Yes | ISO8601(UTC)。アプリで現在時刻を設定(共通カラム.md) |

# 4. クエリ

Stripe請求ID(STRIPE_INVOICE_ID)で UPSERT する。UX_INVOICES_STRIPE により、既存があれば STATUS を更新、無ければ利用者・請求対象月・金額とともに INSERT する。冪等に処理する。

```sql
INSERT INTO T_INVOICES (
  USER_ID, STRIPE_INVOICE_ID, BILLING_PERIOD, AMOUNT, STATUS
) VALUES (
  :user_id, :stripe_invoice_id, :billing_period, :amount, :status   -- STATUS: DEF-001/CODE-007
)
ON CONFLICT (STRIPE_INVOICE_ID) DO UPDATE SET
  STATUS     = excluded.STATUS,
  UPDATED_AT = :updated_at
RETURNING ID, STRIPE_INVOICE_ID, STATUS;
```

# 5. 出力(列)

| 列名 | 論理名 | 型 | 説明 |
|---|---|---|---|
| ID | 請求ID | INTEGER | 請求行の ID |
| STRIPE_INVOICE_ID | Stripe請求ID | TEXT | Stripe の invoice ID |
| STATUS | 請求ステータス | INTEGER | 反映後の請求ステータス(DEF-001/CODE-007) |

# 6. 補足(性能・インデックス)

| 項目 | 内容 |
|---|---|
| 利用インデックス | TBL-008/IDX-1(UX_INVOICES_STRIPE: STRIPE_INVOICE_ID) |
| 想定件数 | 最大1件(1請求1行) |
| 注意点 | ON CONFLICT の対象は一意インデックス UX_INVOICES_STRIPE。Webhook 再送でも同じ結果に収束する(冪等)。区分値は DEF-001/CODE-007。UPDATED_AT はアプリで現在時刻を設定する |
