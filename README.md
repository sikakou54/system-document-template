# system-document-template

[![Markdown Link Check](https://github.com/sikakou54/system-document-template/actions/workflows/markdown-link-check.yml/badge.svg)](https://github.com/sikakou54/system-document-template/actions/workflows/markdown-link-check.yml)
![Format](https://img.shields.io/badge/format-Markdown-lightgrey?logo=markdown)

要件定義・機能設計ドキュメントを、ID採番・トレーサビリティ・レビュー観点まで含めて標準化するための**ドキュメントテンプレート・リポジトリ**。
再利用できる**テンプレート一式**(template/)と、それに従って書かれた**完成サンプル**(docs/ = 会議室予約プロダクト MeetRoom)を収録する。

## 構成

| ディレクトリ | 役割 | 入口 |
|---|---|---|
| [template/](template/) | 新規プロジェクトへコピーして使う**テンプレート集**(文書種別ごとの雛形・運用ルール・採番ルール・プロンプト)。テンプレートの正本 | [template/README.md](template/README.md) |
| [docs/](docs/) | テンプレートに従って書いた**サンプル**(MeetRoom の要件定義・機能設計一式)。記入例 | [docs/README.md](docs/README.md) |

## 使い方

| 目的 | 手順 |
|---|---|
| テンプレートで新規プロジェクトを始める | [template/](template/) 一式を新規プロジェクトの docs/ としてコピーし、各テンプレートを埋める(詳細は [template/README.md](template/README.md)) |
| 記入例(完成形)を確認する | [docs/](docs/) の MeetRoom サンプルを読む([docs/README.md](docs/README.md)) |
| リポジトリの運用ルールを知る | [CLAUDE.md](CLAUDE.md) |

## README / CLAUDE の階層

| 階層 | README.md | CLAUDE.md |
|---|---|---|
| ルート(本リポジトリ) | リポジトリの概要(本ファイル) | リポジトリの運用ルール([CLAUDE.md](CLAUDE.md)) |
| [docs/](docs/) | サンプルプロジェクト(MeetRoom)の概要 | プロジェクトの運用ルール ※ |
| [template/](template/) | プロジェクト概要の雛形(docs/README.md のテンプレート) | プロジェクトの運用ルール ※ |

※ docs/ と template/ の CLAUDE.md は同一内容(プロジェクト運用ルールの正本)。

## サンプル(MeetRoom)の技術前提

Cloudflare (Pages / Workers / D1 / KV / Queues / Cron Triggers) ＋ Stripe(有料会議室の従量課金) ＋ Resend(メール送信)。DB は Cloudflare D1(SQLite)。詳細は [docs/README.md](docs/README.md)。

## CI

[.github/workflows/markdown-link-check.yml](.github/workflows/markdown-link-check.yml) が push / Pull Request 時にマークダウンのリンク切れを検査する。
