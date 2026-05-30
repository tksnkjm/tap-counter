# Tap Counter — ハーネスエンジニアリング資料

## リポジトリ・開発環境
| 項目 | 内容 |
|------|------|
| リポジトリ | https://github.com/tksnkjm/tap-counter |
| ローカルパス | `C:\Home\10_Develope\tap-counter` |
| ブランチ戦略 | `main` 一本運用（直接コミット） |
| 認証 | GitHub CLI（`gh auth login`）、keyring 保存済み |

## デプロイフロー
```
ローカル編集
  └─ git commit & push → main ブランチ
        └─ GitHub Pages が docs/ を自動配信
              └─ https://tksnkjm.github.io/tap-counter/
```

手動 CI/CD 不要。`docs/` 配下の変更が push されれば数分で反映される。

## ディレクトリルール
| パス | 配信 | 用途 |
|------|------|------|
| `docs/` | ✅ GitHub Pages | アプリ本体（index.html） |
| `specs/` | ❌ 配信対象外 | 仕様書・ハーネス資料（本ファイル） |
| `CLAUDE.md` | ❌ 配信対象外 | Claude への指示 |

## Claude 運用ルール
- `docs/` 配下を編集したら `specs/app-spec.md` との整合性を確認する
- 仕様変更が発生した場合は `specs/app-spec.md` を先に更新してからコードを修正する
- ハーネス構成（パス・デプロイ方法・ツール設定等）が変わった場合は本ファイルを更新する
- コミットメッセージは英語、末尾に `Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>` を付与する

## 過去の主な変更履歴
| 日付 | 内容 |
|------|------|
| 2026-05-30 | リポジトリ作成、GitHub CLI 認証設定 |
| 2026-05-30 | タップカウンター初期実装（docs/index.html） |
| 2026-05-30 | index.html をルートから docs/ に移動（GitHub Pages を /docs に変更） |
| 2026-05-30 | specs/ ディレクトリ作成、CLAUDE.md 追加 |
