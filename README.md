# system-document-template

[![Markdown Link Check](https://github.com/sikakou54/system-document-template/actions/workflows/markdown-link-check.yml/badge.svg)](https://github.com/sikakou54/system-document-template/actions/workflows/markdown-link-check.yml)
![Cloudflare](https://img.shields.io/badge/Cloudflare-Workers_Pages_D1-F38020?logo=cloudflare&logoColor=white)
![Stripe](https://img.shields.io/badge/Stripe-metered_billing-635BFF?logo=stripe&logoColor=white)
![Resend](https://img.shields.io/badge/Resend-Email-000000?logo=resend&logoColor=white)
![Docs](https://img.shields.io/badge/docs-119_files-blue)
![Format](https://img.shields.io/badge/format-Markdown-lightgrey?logo=markdown)

要件定義・機能設計ドキュメントの**テンプレート集**。サンプルとして、会議室予約プロダクト **MeetRoom**（Cloudflare / Stripe 従量課金 / Resend 前提）の完全な文書一式を収録する。

## これは何か

| 要素 | 内容 |
|---|---|
| 型（ルール） | ID採番・命名・参照方向・状態・トレーサビリティを定めた文書作成の規約（[docs/CLAUDE.md](docs/CLAUDE.md) / [docs/99_その他/ID採番ルール.md](docs/99_その他/ID採番ルール.md)） |
| 型（テンプレート） | 文書種別ごとの雛形（[docs/99_その他/テンプレート/](docs/99_その他/テンプレート/)） |
| 実例 | 規約に従って書かれた MeetRoom の要件定義・機能設計一式 |

## 入口

- プロダクト概要と推奨読み順 → [docs/README.md](docs/README.md)
- 作業ルール正本 → [docs/CLAUDE.md](docs/CLAUDE.md)
- ID採番・命名の正本 → [docs/99_その他/ID採番ルール.md](docs/99_その他/ID採番ルール.md)

## ディレクトリ構成

| パス | 内容 |
|---|---|
| [docs/01_要件定義/](docs/01_要件定義/) | 業務要件(BR)・機能要件(FR)・共通機能要件(CFR)・ユースケース(UC) |
| [docs/02_機能設計/](docs/02_機能設計/) | 概要・画面(SCR)・API・JOB・モジュール(MOD)・DB(TBL, D1)・クエリ(SQL)・シーケンス(SEQ)・権限(PERM) |
| [docs/03_トレーサビリティ/](docs/03_トレーサビリティ/) | 要件〜設計の対応表 |
| [docs/99_その他/](docs/99_その他/) | ID採番ルール・用語集・テンプレート・レビュー用プロンプト |

## サンプルの技術前提

Cloudflare (Pages / Workers / D1 / KV / Queues / Cron Triggers) ＋ Stripe（有料会議室の従量課金）＋ Resend（メール送信）。
DB は Cloudflare D1（SQLite）。ERR/MSG は中央カタログを持たず各文書にインライン定義する。

## CI

[.github/workflows/markdown-link-check.yml](.github/workflows/markdown-link-check.yml) が push / Pull Request 時にマークダウンのリンク切れを検査する。
