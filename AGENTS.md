# AGENTS.md — ワイガヤJリーグ

このファイルは AI コーディングエージェント（OpenAI Codex / ChatGPT Codex、Claude Code など）向けの共通ガイドです。
Codex はリポジトリ直下の `AGENTS.md` を、Claude Code は `CLAUDE.md`（ここから本ファイルを読み込み）を自動で参照します。
ルールを変えるときは **このファイルだけ** を更新してください。

## プロジェクト概要

- ゴルフ仲間のリーグ戦の成績・メダル・組み合わせ・大会案内を管理する、スマホ向けの単一ページアプリ。
- 公開 URL: https://qkkf48309-commits.github.io/waigaya-league/ （GitHub Pages、`main` ブランチ直下を配信）
- ビルド工程・パッケージ管理なし。HTML / CSS / JavaScript はすべて `index.html` 1 ファイルにインライン。

## ファイル構成

| ファイル | 役割 |
| --- | --- |
| `index.html` | 本体（公開されるアプリ）。変更は基本的にここだけ |
| `waigaya_league.html`, `index.html.html` | 旧バージョンの残骸（同一内容）。特に指示がない限り編集しない |
| `bgm.mp3`, `3274-1.mp3` | BGM・効果音 |
| `notice_header.png` | 大会案内のヘッダー画像 |

## データと外部サービス

- データは Firebase Realtime Database（REST API を `fetch` で呼び出し）と `localStorage` に保存。
- スコアカード読み取りに OCR.space API を使用。
- データ構造（保存キーや JSON の形）を変えるときは、既存データを読めるよう後方互換を保つこと。

## 作業ルール

- UI 文言・コミットメッセージは **日本語** で書く（既存の履歴に合わせる）。
- 外部ライブラリや CDN を新たに追加しない。素の JavaScript で書く。
- iPhone Safari での表示（`viewport-fit=cover`、セーフエリア、タップ操作）を壊さない。
- 既存のコードスタイル（CSS 変数 `--primary` など、関数の書き方）に合わせる。
- 大きな機能追加の前に、変更方針を PR の説明に書く。

## 動作確認

テストやビルドはありません。ローカルで確認する場合:

```sh
python3 -m http.server 8000
# ブラウザで http://localhost:8000/ を開く（スマホ幅で確認）
```

JavaScript の構文エラーがないか、ブラウザのコンソールで確認してから PR を出してください。

## Codex と Claude Code の併用

- どちらのエージェントも作業ブランチを切って PR を出し、`main` へ直接 push しない。
- 片方が作った PR をもう片方にレビューさせてもよい（例: Codex が実装 → Claude Code がレビュー）。
- 同じ箇所を同時に編集すると衝突しやすいので、1 つの作業は 1 つのエージェントに任せる。
