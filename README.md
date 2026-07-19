# 統合設計書テンプレート

[![Markdown Link Check](https://github.com/sikakou54/system-document-template/actions/workflows/markdown-link-check.yml/badge.svg)](https://github.com/sikakou54/system-document-template/actions/workflows/markdown-link-check.yml)
![Format](https://img.shields.io/badge/format-Markdown-lightgrey?logo=markdown)

要求定義から詳細設計（画面・データベース・API・JOB・モジュール・クエリ）までを、0〜12章の一貫した構成で作成するためのテンプレートと記入例を収録する。

本リポジトリのメイン文書は、0〜12章を設計種別ごとの文書に分けた分割版（テンプレートと記入例）である。

## メイン文書

| ディレクトリ | 役割 | 入口 |
|---|---|---|
| [テンプレート/](テンプレート/) | **テンプレートの正本**。0〜12章を設計種別ごとに分割したテンプレート。新規システムの設計書はこのディレクトリをコピーして作成する | [テンプレート/README.md](テンプレート/README.md) |
| [社員名簿管理システム/](社員名簿管理システム/) | テンプレートに従って詳細化した記入例。Cloudflare Workers＋D1（SQLite互換）を採用し、11画面のHTML/PNGモックアップを含む | [社員名簿管理システム/README.md](社員名簿管理システム/README.md) |

## 設計範囲

| No | セクション | 主な内容 |
|---:|---|---|
| 0 | はじめに | 目的、前提、設計確定範囲 |
| 1 | 要求定義 | 背景、目的、業務要求、非機能要求、制約、対象範囲 |
| 2 | 機能要件 | 機能一覧、想定される全ユースケースと網羅表（機能要求・認可を含む）、基本・代替・例外フローのシーケンス図、データモデル、共通コード |
| 3 | 画面設計 | HTML/PNGモックアップ、項目、イベント、状態、遷移、メッセージ |
| 4 | データベース設計 | SQLite/D1のテーブル、制約、索引、トリガー、原子実行 |
| 5 | API設計 | 入出力、バリデーション、処理フロー、処理詳細、エラー |
| 6 | JOB設計 | Cron、Queues、処理フロー、処理詳細、再配信、監視 |
| 7 | モジュール設計 | 責務、公開IF、処理フロー、処理詳細、データアクセス境界 |
| 8 | クエリ設計 | データアクセスモジュールが実行するSQL、bind、結果、性能、排他 |
| 9 | トレーサビリティ | 要求から画面、API、モジュール、JOB、SQL、DBへの対応 |
| 10 | レビューチェックリスト | 詳細設計とアーキテクチャ境界の確認観点 |
| 11 | 詳細設計への引継ぎ | 実装・環境・性能・試験で確定する事項 |
| 12 | 設計の落とし込み関係 | オンライン／バッチからモジュール、SQL、DBへの経路 |

## 使い方

1. [テンプレート/](テンプレート/) を新しいシステム名のディレクトリへコピーする。
2. 各章直前の定義ルールコメントを確認し、0章から順に記入する。
3. 具体的な記載粒度は [社員名簿管理システム/](社員名簿管理システム/) を参照する。

## アーキテクチャ前提

- バックエンドはCloudflare Workers Paid、データベースはCloudflare D1（SQLite互換）、非同期処理はCloudflare Queuesを前提とする。
- D1 Binding、Prepared Statement、SQLを扱うのはデータアクセスモジュールだけとする。
- APIやJOBからデータベースへ直接アクセスしない。
- API、JOB、モジュールは番号付きの「処理フロー」と、それに対応する「処理詳細」で定義する。

## CI

[.github/workflows/markdown-link-check.yml](.github/workflows/markdown-link-check.yml) が、ルートREADMEとCLAUDE.md、テンプレート、社員名簿管理システムのMarkdownリンク切れを検査する。
