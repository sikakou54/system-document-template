# 1. 基本情報

| 項目 | 内容 |
|---|---|
| クエリID | SQL-029 |
| クエリ名 | 月次利用実績UPSERT |
| 概要 | 会議室×対象月の利用実績(予約件数・利用時間)を登録または更新する(1組み合わせ1行)。 |
| 用途 | 月次利用実績集計結果の保存(UsageReportService)。 |
| 使用元 | MOD-005 |

# 2. 対象テーブル

| テーブル | 物理名 | 用途 |
|---|---|---|
| TBL-006 | T_USAGE_REPORTS | 保存対象(会議室×月の利用実績 UPSERT) |

# 3. 入力パラメータ

| パラメータ | 論理名 | 型 | 必須 | 説明・制約 |
|---|---|---|---|---|
| :room_id | 会議室ID | INTEGER | Yes | 集計対象の会議室ID |
| :target_month | 対象月 | TEXT | Yes | 'YYYY-MM' 形式 |
| :reservation_count | 予約件数 | INTEGER | Yes | 完了予約の件数 |
| :total_minutes | 利用時間分 | INTEGER | Yes | 利用時間の合計(分) |
| :updated_at | 更新日時 | TEXT | Yes | ISO8601(UTC)。アプリで現在時刻を設定(共通カラム.md) |

# 4. クエリ

会議室×対象月で UPSERT する。UX_USAGE_REPORTS_ROOM_MONTH(ROOM_ID, TARGET_MONTH)により、既存があれば件数・利用時間を更新、無ければ INSERT する。会議室ごとに実行する。

```sql
INSERT INTO T_USAGE_REPORTS (
  ROOM_ID, TARGET_MONTH, RESERVATION_COUNT, TOTAL_MINUTES
) VALUES (
  :room_id, :target_month, :reservation_count, :total_minutes
)
ON CONFLICT (ROOM_ID, TARGET_MONTH) DO UPDATE SET
  RESERVATION_COUNT = excluded.RESERVATION_COUNT,
  TOTAL_MINUTES     = excluded.TOTAL_MINUTES,
  UPDATED_AT        = :updated_at
RETURNING ID, ROOM_ID, TARGET_MONTH;
```

# 5. 出力(列)

| 列名 | 論理名 | 型 | 説明 |
|---|---|---|---|
| ID | 実績ID | INTEGER | 利用実績行の ID |
| ROOM_ID | 会議室ID | INTEGER | 会議室の ID |
| TARGET_MONTH | 対象月 | TEXT | 集計対象の年月('YYYY-MM') |

# 6. 補足(性能・インデックス)

| 項目 | 内容 |
|---|---|
| 利用インデックス | TBL-006/IDX-1(UX_USAGE_REPORTS_ROOM_MONTH: ROOM_ID, TARGET_MONTH) |
| 想定件数 | 対象月に完了予約がある会議室の件数分(1件ずつ UPSERT) |
| 注意点 | 集計値は SQL-002(月次利用実績集計)の結果を渡す。ON CONFLICT の対象は一意インデックス UX_USAGE_REPORTS_ROOM_MONTH。UPDATED_AT はアプリで現在時刻を設定する |
