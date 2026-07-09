# 1. 概要

MeetRoom の REST API の入出力・認証・認可・バリデーション・エラーを定義する。
共通設計(認証・エラー封筒・ページネーション)は API-COM_共通設計.md が正本。エラー定義(ERR-XXX)はカタログを設けず、共通エラー(ERR-001 / ERR-002 / ERR-006)は API-COM_共通設計.md §4.1 共通エラー一覧に、各 API 固有のエラーは各 API 文書 §7 エラーにインライン定義する。

# 2. 一覧

| ID | 名称 | メソッド | パス | 概要 | トレース元 | 主要依存 |
|---|---|---|---|---|---|---|
| API-001 | ログイン | POST | /api/auth/login | メールアドレスとパスワードで本人確認し Bearer JWT を発行する | CFR-001/UC-01 | MOD-001 |
| API-002 | 会議室検索 | GET | /api/rooms | 日時・人数・設備を条件に空き会議室を検索する | FR-001/UC-01, FR-002/UC-01 | MOD-002 |
| API-003 | 予約登録 | POST | /api/reservations | 会議室の予約を登録する。同一会議室・同一時間帯の二重予約は不可 | FR-002/UC-01 | MOD-002, MOD-003 |
| API-004 | 予約変更 | PUT | /api/reservations/{id} | 自分の予約の日時・タイトルを変更する | FR-003/UC-01 | MOD-003 |
| API-005 | 予約キャンセル | POST | /api/reservations/{id}/cancel | 自分の予約をキャンセルする | FR-003/UC-02 | MOD-003 |
| API-006 | 予約一覧取得 | GET | /api/reservations | 自分の予約一覧を取得する | FR-003/UC-01, FR-003/UC-02 | MOD-003 |
| API-007 | 会議室登録・編集 | POST / PUT | /api/rooms, /api/rooms/{id} | 管理者が会議室(利用単価含む)・設備を登録・編集する | FR-005/UC-01 | MOD-004 |
| API-008 | 利用実績取得 | GET | /api/reports/usage | 管理者が会議室ごとの月次利用実績を取得する | FR-006/UC-01 | MOD-005 |
| API-009 | 設備一覧取得 | GET | /api/equipments | 登録済みの設備の一覧を取得する | FR-005/UC-01, FR-001/UC-01 | MOD-004 |
| API-010 | 支払い方法登録セッション作成 | POST | /api/billing/checkout | Stripe Checkout(サブスク)の支払い方法登録セッションを作成し URL を返す | FR-008/UC-01 | MOD-007 |
| API-011 | Stripe Webhook受信 | POST | /api/webhooks/stripe | Stripe イベントを受信し契約・請求状態を更新する | FR-008/UC-01 | MOD-007 |
| API-012 | 利用量・請求取得 | GET | /api/billing/usage | 当月の利用量・請求見込みと請求履歴を取得する | FR-008/UC-02 | MOD-007 |
| API-013 | 設備登録 | POST | /api/equipments | 管理者が設備を新規登録する | FR-005/UC-01 | MOD-004 |
| API-014 | 会議室一覧取得 | GET | /api/admin/rooms | 管理者向けに全会議室(利用停止を含む)を設備一覧付きで取得する | FR-005/UC-01 | MOD-004 |
| API-COM | 共通設計 | - | - | 全 API に共通する認証・エラー封筒・ページネーション等の共通仕様 | - | - |
