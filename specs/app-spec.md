# Tap Counter — アプリケーション仕様書

## 概要
画面をタップするたびにカウントが +1 されるシンプルな Web アプリ。  
スマホのブラウザで開いて即プレイできることがゴール。インストール・フレームワーク不要。

## 配信
| 項目 | 内容 |
|------|------|
| リポジトリ | https://github.com/tksnkjm/tap-counter |
| 公開 URL | https://tksnkjm.github.io/tap-counter/ |
| 配信ブランチ | `main` / `/docs` |
| 成果物 | `docs/index.html`（HTML / CSS / JS 単一ファイル） |

## ファイル構成
```
tap-counter/
├── docs/           # GitHub Pages 配信対象
│   └── index.html  # アプリ本体（HTML+CSS+JS 単一ファイル）
├── specs/          # 配信対象外：仕様・ハーネス資料
│   ├── app-spec.md     # 本ファイル
│   └── harness.md      # ハーネスエンジニアリング資料
└── CLAUDE.md       # Claude への指示
```

## 必須機能

### カウンター
- 画面全体がタップ領域。どこを押しても **カウント +1**
- 画面中央に現在のカウントを **特大の数字** で表示
- `localStorage` にカウントを保存し、再アクセス時も記録を保持

### リセット
- 「RESET」ボタンでカウントを 0 に戻す
- 誤操作しにくい位置（画面下部中央）・サイズに配置

## 演出・体験

### アニメーション
- タップごとに数字がポップ（scale 1.18 → バウンス）する
- タップした位置に紫のグラデーション波紋（リップル）エフェクトを表示
- 背景アクセントカラーがタップごとに変化（hue ローテーション）

### スマホ最適化
| 設定 | 値 |
|------|----|
| `user-scalable` | `no` |
| `touch-action` | `manipulation` |
| `-webkit-tap-highlight-color` | `transparent` |
| `user-select` | `none` |
| `overscroll-behavior` | `none` |

### フィードバック
- バイブレーション：`navigator.vibrate(12ms)`
- マイルストーン祝福アニメ：10 / 50 / 100 / 500 / 1000 / 5000 / 10000 回

## 発展機能

### ⚡ スピードモード
- 10 秒間の連打数を測定
- 自己ベストを `localStorage`（キー：`tap-speed-best`）に保存
- 計測終了後 3 秒間結果を表示し、通常モードに戻る

### 🏆 ベスト記録
- 通常モードの最大カウントを `localStorage`（キー：`tap-best`）に保存
- 左上に常時表示

## localStorage キー一覧
| キー | 型 | 内容 |
|------|----|------|
| `tap-count` | number | 現在のカウント |
| `tap-best` | number | 通常モードの自己ベスト |
| `tap-speed-best` | number | スピードモードの自己ベスト（10秒間） |

## 対応環境
- iOS Safari（最新）
- Android Chrome（最新）
- デスクトップ Chrome / Firefox / Edge（動作確認用）
- 外部ライブラリ・CDN なし
