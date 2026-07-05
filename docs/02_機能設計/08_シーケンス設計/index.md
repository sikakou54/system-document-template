## 1. 概要

MeetRoom のシーケンス設計(SEQ)を定義する。複数要素(画面・API・モジュール・ジョブ・テーブル・外部サービス)の時系列連携を管理する。各シーケンスの詳細は SEQ-XXX_シーケンス名.md に記載する。

## 2. 一覧

| ID | 名称 | 概要 | 契機 | 関連要素 |
|---|---|---|---|---|
| SEQ-001 | 会議室予約登録シーケンス | 会議室前提判定・有料契約確認・重複判定を経て会議室予約を確定する連携 | 利用者操作 | SCR-003, API-003, MOD-002, MOD-003, TBL-001, TBL-002, TBL-003 |
| SEQ-002 | 予約リマインド通知シーケンス | Cron→Queue→通知サービス→Resend で予約者へリマインド送信する連携 | 定期(Cron) | JOB-001, MOD-006, TBL-003, Cloudflare Cron Trigger, Cloudflare Queue, Resend |
| SEQ-003 | 利用量の従量課金計上シーケンス | 完了予約の利用量を Stripe Meter Event に計上し月次請求を反映する連携 | 定期(Cron)／Webhook | JOB-002, MOD-007, API-011, TBL-002, TBL-003, TBL-007, TBL-008, Stripe |
| SEQ-004 | 支払い方法登録シーケンス | Stripe Checkout で支払い方法を登録し課金契約を有効化する連携 | 利用者操作／Webhook | SCR-007, API-010, API-011, MOD-007, TBL-001, Stripe |
