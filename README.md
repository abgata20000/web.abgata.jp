# エイビー 公式サイト

[abgata.jp](https://abgata.jp) - 個人事業「エイビー」の公式ホームページです。

## 技術スタック

- **フレームワーク**: [Astro](https://astro.build/) 5.x (SSG)
- **スタイリング**: CSS 変数 + Astro スコープ付き CSS
- **フォント**: M PLUS Rounded 1c / Noto Sans JP
- **ホスティング**: GitHub Pages

## 開発

```bash
# 依存パッケージのインストール
npm install

# 開発サーバーの起動
npm run dev

# ビルド
npm run build

# ビルドのプレビュー
npm run preview
```

## ディレクトリ構成

```
src/
├── pages/          # ページ (ファイルベースルーティング)
├── layouts/        # 共通レイアウト
├── components/     # コンポーネント
├── styles/         # グローバル CSS
└── assets/         # 画像等 (Astro で最適化)
public/             # 静的ファイル
old/                # 旧サイト (参照用・読み取り専用)
```



