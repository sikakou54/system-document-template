# traceability_scr_api_db

## 1. 概要

画面(SCR)から API・モジュール(MOD)・テーブル(TBL)までの実装連鎖を追跡する。
API は各 SCR の使用API(02_画面設計)、MOD は各 API の実装MOD(03_API設計)、主なTBL は各 MOD の依存TBL(05_モジュール設計)からの転記で構成する。

## 2. 対応表

| SCR ID | API | MOD | 主なTBL |
|---|---|---|---|
| SCR-001 ログイン | API-001 | MOD-001 | TBL-001 |
| SCR-002 会議室検索 | API-002, API-009 | MOD-002, MOD-004 | TBL-002, TBL-003, TBL-004, TBL-005 |
| SCR-003 予約登録 | API-003 | MOD-002, MOD-003 | TBL-002, TBL-003, TBL-001 |
| SCR-004 予約一覧・変更・キャンセル | API-006, API-004, API-005 | MOD-003 | TBL-003, TBL-002 |
| SCR-005 会議室・設備管理 | API-007, API-009, API-013, API-014 | MOD-004 | TBL-002, TBL-004, TBL-005 |
| SCR-006 利用実績 | API-008 | MOD-005 | TBL-002, TBL-003, TBL-006 |
| SCR-007 支払い方法・請求 | API-010, API-012 | MOD-007 | TBL-001, TBL-007, TBL-008, TBL-003 |

- API-011(Stripe Webhook受信)は画面から呼ばれないため本表(SCR起点)には含めない。API-011 も MOD-007 を実装先とする(03_API設計)。

## 3. 更新ルール

| 更新契機 | 更新内容 |
|---|---|
| SCR の新規作成・使用API変更 | 該当 SCR の行を追加／更新し、API を SCR の使用APIから転記する |
| API の実装MOD変更 | 該当行の MOD を API の実装先から転記する |
| MOD の依存TBL変更 | 該当行の主なTBL を MOD の依存TBLから転記する |
| ID廃止 | 行は削除せず、備考に「廃止」と記す |

- 本対応表の更新は関連文書の作成・更新と同一作業内で行う(正本: docs/CLAUDE.md §6・§10-7)。
