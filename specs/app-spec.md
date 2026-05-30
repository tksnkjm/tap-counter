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

## 熊スプライトアニメーション

### 素材（docs/assets/）
| ファイル | 内容 | サイズ |
|---------|------|--------|
| `bear-sprite.png` | 白熊が茶碗を箸で叩く動作（背景透過） | 1408×768px |
| `chin.png` | 「チン」コミック風テロップ（背景透過） | 1408×768px |

### スプライト構成
| 項目 | 値 |
|------|-----|
| 列数（COLS） | 4 |
| 行数（ROWS） | 2 |
| 総コマ数 | 8 |
| 1コマ原寸 | 352×384px |
| 表示サイズ | clamp(110px, 32vw, 200px) ― 縦横比維持 |

### アニメーション動作
- タップごとに frame 0 から全 8 コマを 1 サイクル再生（JS setTimeout コマ送り方式）
- 連打時は毎回 frame 0 からリスタート
- アイドル時は frame 0（待機ポーズ）を表示

### チンテロップ
- 打撃コマ（`HIT_FRAME = 2`）到達時に `chin.png` を表示
- pop アニメーション：scale 0.5→1.15→1.0 + opacity 0→1→0
- 熊より奥（z-index: 1）に配置

### CONFIG 定数（コード冒頭で調整可能）
| 定数 | デフォルト | 説明 |
|------|-----------|------|
| COLS | 4 | スプライト列数 |
| ROWS | 2 | スプライト行数 |
| TOTAL_FRAMES | 8 | 総コマ数 |
| FRAME_W | 352 | 元画像 1 コマ幅（px） |
| FRAME_H | 384 | 元画像 1 コマ高さ（px） |
| FRAME_MS | 75 | 1 コマ表示時間（ms） |
| HIT_FRAME | 2 | チン発火コマ（0始まり） |
| CHIN_DURATION_MS | 650 | チンフェードアウト時間（ms） |

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
