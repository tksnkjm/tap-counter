# CLAUDE.md — tap-counter プロジェクト指示

## プロジェクト概要
シンプルなタップカウンター Web アプリ。`docs/index.html` が唯一の成果物。  
詳細は `specs/app-spec.md` を参照。

## ディレクトリ構成
```
docs/       ← GitHub Pages 配信対象（触っていい）
specs/      ← 仕様・ハーネス資料（配信対象外）
CLAUDE.md   ← 本ファイル
```

## コード変更時の必須チェック

`docs/` 配下のファイルを編集・作成した場合、**必ず以下を確認・更新すること**。

### 1. `specs/app-spec.md` との整合性確認
- 変更した機能・仕様が `app-spec.md` の記述と一致しているか確認する
- 新機能追加・仕様変更があれば `app-spec.md` を更新する
- localStorage キー追加・変更があればキー一覧テーブルを更新する

### 2. `specs/harness.md` の更新
- デプロイ構成・ディレクトリルール・ツール設定に変更があれば更新する
- 主な変更は「過去の主な変更履歴」テーブルに追記する

## 仕様変更の順序
1. `specs/app-spec.md` を先に更新する
2. その後 `docs/index.html` を修正する
3. 両方をまとめて 1 コミットにする

## コミットルール
- メッセージは英語
- 末尾に必ず付与：`Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>`
- PowerShell の here-string（`@'...'@`）でメッセージを渡す

## 技術制約
- `docs/index.html` は HTML / CSS / JS 単一ファイル
- 外部ライブラリ・CDN 禁止
- `specs/` や `CLAUDE.md` は GitHub Pages に含まれないこと（`docs/` 外に置く）
