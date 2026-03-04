---
name: design-guide
description: エイビーHPリニューアルのデザインガイド。カラーパレット、タイポグラフィ、スペーシング、コンポーネントの設計指針とCSS変数定義。デザイン実装、UI/UX設計、スタイリング、レイアウト作業時に参照する。
---

# エイビー HP デザインガイド — Pop & Craft

## デザインコンセプト

### テーマ: 「Pop & Craft」

プログラマーとしての確かな技術力を、**ポップで楽しく、きれいめ**に表現する。
堅苦しいコーポレートサイトではなく、訪れた人が「楽しそうな人が作ってるな」と感じられるサイト。

### キーワード
- **ポップ** — 明るく親しみやすい色使い、遊び心のあるインタラクション
- **クラフト** — コードで丁寧に作り込んだ感触、細部への配慮 (マイクロインタラクション、余白の精度)
- **きれいめ** — 整然としたレイアウト、十分な余白、読みやすいタイポグラフィ
- **楽しい** — 微細なアニメーション、ホバーエフェクト、視覚的なアクセント
- **プロフェッショナル** — 情報が整理されていて信頼感がある

### 旧サイトからの継承と進化
- 旧サイトのロゴ「AB」(赤い幾何学的ブロック体) のアイデンティティを継承
- アクセントカラー赤 `#e61e1e` のエネルギーを活かしつつ、よりモダンな配色へ
- カード型レイアウトのアイデアは継承しつつ、レスポンシブに進化
- 「Create Useful (便利なものを創る)」のコンセプトは引き続き大切にする

---

## 1. ブランドアイデンティティ

### ロゴ
- **形状**: 赤い幾何学ブロック体の「AB」(SVG 変換時は元画像を必ず参照すること)
- **元ファイル**: `old/web.abgata.jp/common/images/logo.gif` (90×43px)
- **新サイト**: SVG に変換してスケーラブルにする (元 GIF を忠実に再現)
- **ロゴカラー**: プライマリレッド `#e61e1e` + ホワイト `#ffffff`
- **最小表示サイズ**: 幅 60px 以上を維持
- **周囲余白**: ロゴ高さの 50% 以上のクリアスペースを確保

### スローガン
- **「Create Useful」** — 便利なものを創る
- ロゴの近くやヒーローセクションで使用

---

## 2. カラーシステム

全てのカラーは CSS 変数で定義し、ハードコードしない。

### CSS 変数定義

```css
:root {
  /* === ブランドカラー === */
  --color-primary: #e61e1e;           /* 旧サイト継承: メインレッド */
  --color-primary-light: #ff4d4d;     /* ホバー・アクセント用 */
  --color-primary-dark: #b81818;      /* ダーク用・フッター */
  --color-primary-bg: #fff0f0;        /* 背景のほのかな赤み */
  --color-primary-bg-hover: #ffe0e0;  /* カードホバー時の背景 */

  /* === セカンダリカラー === */
  --color-secondary: #2d2d2d;         /* 濃いグレー (見出し) */
  --color-secondary-light: #555555;   /* 本文テキスト */

  /* === アクセントカラー (1ページあたり最大2色まで使用) === */
  --color-accent-blue: #3b82f6;       /* リンク・CTAバリエーション */
  --color-accent-green: #22c55e;      /* 成功・完了 */
  --color-accent-yellow: #f59e0b;     /* 注意・ハイライト */
  --color-accent-purple: #8b5cf6;     /* 装飾・バッジ */

  /* === ニュートラル === */
  --color-white: #ffffff;
  --color-gray-50: #fafafa;           /* セクション背景 (交互) */
  --color-gray-100: #f5f5f5;          /* カード背景 */
  --color-gray-200: #e5e5e5;          /* ボーダー */
  --color-gray-300: #d4d4d4;          /* 無効状態 */
  --color-gray-400: #a3a3a3;          /* プレースホルダー */
  --color-gray-500: #737373;          /* 補足テキスト */
  --color-gray-600: #525252;          /* サブテキスト */
  --color-gray-800: #262626;          /* 濃いテキスト */
  --color-gray-900: #171717;          /* 最も濃い */
  --color-black: #111111;

  /* === セマンティックカラー === */
  --color-text-primary: var(--color-gray-800);
  --color-text-secondary: var(--color-gray-600);
  --color-text-muted: var(--color-gray-500);
  --color-text-inverse: var(--color-white);
  --color-bg-page: var(--color-white);
  --color-bg-section: var(--color-gray-50);
  --color-bg-card: var(--color-white);
  --color-border: var(--color-gray-200);
  --color-link: var(--color-primary);
  --color-link-hover: var(--color-primary-dark);

  /* === フォーカス・アクセシビリティ === */
  --color-focus-ring: rgba(230, 30, 30, 0.4);

  /* === z-index スケール === */
  --z-header: 100;
  --z-dropdown: 150;
  --z-modal-backdrop: 200;
  --z-modal: 250;
  --z-toast: 300;
}
```

### カラー使用ルール
- **プライマリレッド**: CTA ボタン、ロゴ、重要なアクセント、ナビアクティブ状態
- **セカンダリ (濃いグレー)**: 見出し、本文テキスト
- **アクセントカラー**: 装飾的な要素に限定使用 (1ページあたり最大2色まで)
- **ニュートラル**: 背景、ボーダー、セパレーター
- **コントラスト比**: テキストと背景は WCAG AA (4.5:1) 以上を厳守

### コントラスト比に関する注意
- `--color-primary` (#e61e1e) は白背景でのコントラスト比が **約 4.5:1 (AA 境界値)**
- **14px 以下の小さいテキスト**には `--color-primary` を使用禁止 → `--color-primary-dark` (#b81818, 約 6.5:1) を使うこと
- テキストリンクには**必ず下線 (`text-decoration: underline`) を付与**する (色だけで区別しない)
- ボタンなど大きい要素や太字テキストでの `--color-primary` 使用は問題なし

### ダークモード (将来対応)

```css
@media (prefers-color-scheme: dark) {
  :root {
    --color-primary: #ff4d4d;
    --color-primary-dark: #e61e1e;
    --color-primary-bg: #2a1010;
    --color-text-primary: #e5e5e5;
    --color-text-secondary: #a3a3a3;
    --color-bg-page: #111111;
    --color-bg-section: #1a1a1a;
    --color-bg-card: #1f1f1f;
    --color-border: #333333;
  }
}
```

---

## 3. タイポグラフィ

### フォントファミリー

```css
:root {
  /* 見出し: 丸みのあるポップ体 */
  --font-heading: 'M PLUS Rounded 1c', 'Hiragino Kaku Gothic Pro', sans-serif;

  /* 本文: 読みやすいゴシック */
  --font-body: 'Noto Sans JP', 'Hiragino Kaku Gothic Pro', 'Meiryo', sans-serif;

  /* コード: 等幅 */
  --font-mono: 'JetBrains Mono', 'Source Code Pro', monospace;
}
```

### Google Fonts 読み込み

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=M+PLUS+Rounded+1c:wght@400;500;700;800&family=Noto+Sans+JP:wght@400;500;700&display=swap" rel="stylesheet">
```

### フォントサイズスケール

```css
:root {
  --text-xs: 0.75rem;    /* 12px - 注釈 */
  --text-sm: 0.875rem;   /* 14px - 小さいテキスト */
  --text-base: 1rem;     /* 16px - 本文 */
  --text-lg: 1.125rem;   /* 18px - リード文 */
  --text-xl: 1.25rem;    /* 20px - 小見出し */
  --text-2xl: 1.5rem;    /* 24px - セクション見出し */
  --text-3xl: 1.875rem;  /* 30px - ページ見出し */
  --text-4xl: 2.25rem;   /* 36px - ヒーロー */
  --text-5xl: 3rem;      /* 48px - ヒーロー大 */
}
```

### 行間・文字間

```css
:root {
  --leading-tight: 1.3;    /* 見出し */
  --leading-normal: 1.7;   /* 本文 (日本語は広め) */
  --leading-relaxed: 2.0;  /* 長文・注釈 */

  --tracking-tight: -0.02em;  /* 大見出し */
  --tracking-normal: 0;       /* 通常 */
  --tracking-wide: 0.05em;    /* 小さい文字・英字 */
  --tracking-wider: 0.1em;    /* ナビ・ラベル */
}
```

### 見出しスタイルルール

| 要素 | フォント | ウェイト | サイズ (PC) | サイズ (SP) |
|------|----------|----------|-------------|-------------|
| h1 | M PLUS Rounded 1c | 800 | `--text-4xl` | `--text-3xl` |
| h2 | M PLUS Rounded 1c | 700 | `--text-3xl` | `--text-2xl` |
| h3 | M PLUS Rounded 1c | 700 | `--text-2xl` | `--text-xl` |
| h4 | M PLUS Rounded 1c | 500 | `--text-xl` | `--text-lg` |
| body | Noto Sans JP | 400 | `--text-base` | `--text-base` |
| small | Noto Sans JP | 400 | `--text-sm` | `--text-sm` |

---

## 4. スペーシングシステム

4px ベースの倍数で統一。

```css
:root {
  --space-1: 0.25rem;   /* 4px */
  --space-2: 0.5rem;    /* 8px */
  --space-3: 0.75rem;   /* 12px */
  --space-4: 1rem;      /* 16px */
  --space-5: 1.25rem;   /* 20px */
  --space-6: 1.5rem;    /* 24px */
  --space-8: 2rem;      /* 32px */
  --space-10: 2.5rem;   /* 40px */
  --space-12: 3rem;     /* 48px */
  --space-16: 4rem;     /* 64px */
  --space-20: 5rem;     /* 80px */
  --space-24: 6rem;     /* 96px */
}
```

### 使い分け
- **コンポーネント内部パディング**: `--space-4` 〜 `--space-6`
- **セクション間マージン**: `--space-16` 〜 `--space-24`
- **カード内パディング**: `--space-6` 〜 `--space-8`
- **テキスト間マージン**: `--space-2` 〜 `--space-4`
- **グリッドギャップ**: `--space-6` 〜 `--space-8`

---

## 5. レイアウト

### ブレークポイント

```css
:root {
  --bp-sm: 640px;    /* スマートフォン (横) */
  --bp-md: 768px;    /* タブレット */
  --bp-lg: 1024px;   /* PC */
  --bp-xl: 1280px;   /* 大画面 */
}

/* モバイルファースト: min-width で拡張 */
@media (min-width: 640px)  { /* sm */ }
@media (min-width: 768px)  { /* md */ }
@media (min-width: 1024px) { /* lg */ }
@media (min-width: 1280px) { /* xl */ }
```

### コンテナ

```css
:root {
  --container-max: 1200px;
  --container-padding: var(--space-4);  /* SP: 16px */
}

@media (min-width: 768px) {
  :root {
    --container-padding: var(--space-8);  /* PC: 32px */
  }
}
```

### コンテナ実装

```css
.container {
  width: 100%;
  max-width: var(--container-max);
  margin-inline: auto;
  padding-inline: var(--container-padding);
}
```

### グリッドシステム

```css
/* カード型レイアウト (旧サイトから継承・進化) */
.grid-cards {
  display: grid;
  gap: var(--space-6);
  grid-template-columns: 1fr;                          /* SP: 1列 */
}

@media (min-width: 640px) {
  .grid-cards { grid-template-columns: repeat(2, 1fr); }  /* タブレット: 2列 */
}

@media (min-width: 1024px) {
  .grid-cards { grid-template-columns: repeat(3, 1fr); }  /* PC: 3列 */
}
```

---

## 6. コンポーネントスタイル

### 角丸・シャドウ・トランジション

```css
:root {
  /* 角丸 */
  --radius-sm: 4px;
  --radius-md: 8px;
  --radius-lg: 12px;
  --radius-xl: 16px;
  --radius-full: 9999px;

  /* シャドウ */
  --shadow-sm: 0 1px 2px rgba(0, 0, 0, 0.06);
  --shadow-md: 0 4px 6px rgba(0, 0, 0, 0.07);
  --shadow-lg: 0 10px 25px rgba(0, 0, 0, 0.1);
  --shadow-xl: 0 20px 40px rgba(0, 0, 0, 0.12);
  --shadow-primary: 0 4px 14px rgba(230, 30, 30, 0.3);  /* 赤い光彩 */

  /* トランジション */
  --transition-fast: 150ms ease;
  --transition-base: 250ms ease;
  --transition-slow: 400ms ease;
}
```

### ボタン

```css
/* プライマリボタン */
.btn-primary {
  background: var(--color-primary);
  color: var(--color-text-inverse);
  font-family: var(--font-heading);
  font-weight: 700;
  padding: var(--space-3) var(--space-8);
  border-radius: var(--radius-full);
  border: none;
  cursor: pointer;
  transition: all var(--transition-base);
  box-shadow: var(--shadow-sm);
}

.btn-primary:hover {
  background: var(--color-primary-light);
  box-shadow: var(--shadow-primary);
  transform: translateY(-2px);
}

.btn-primary:active {
  transform: translateY(0);
  box-shadow: var(--shadow-sm);
}

/* セカンダリボタン (アウトライン) */
.btn-secondary {
  background: transparent;
  color: var(--color-primary);
  border: 2px solid var(--color-primary);
  padding: var(--space-3) var(--space-8);
  border-radius: var(--radius-full);
  font-family: var(--font-heading);
  font-weight: 700;
  cursor: pointer;
  transition: all var(--transition-base);
}

.btn-secondary:hover {
  background: var(--color-primary);
  color: var(--color-text-inverse);
}
```

### カード

```css
/* 旧サイトのカードレイアウトを進化 */
.card {
  background: var(--color-bg-card);
  border-radius: var(--radius-lg);
  padding: var(--space-6);
  box-shadow: var(--shadow-md);
  transition: all var(--transition-base);
  border: 1px solid var(--color-border);
}

.card:hover {
  box-shadow: var(--shadow-lg);
  transform: translateY(-4px);
  border-color: var(--color-primary-bg-hover);
}
```

### ナビゲーション

```css
/* 旧サイト: GIF画像ナビ → 新: テキスト+アイコン */
.nav-link {
  font-family: var(--font-heading);
  font-weight: 500;
  font-size: var(--text-sm);
  letter-spacing: var(--tracking-wider);
  color: var(--color-text-primary);
  text-decoration: none;
  padding: var(--space-2) var(--space-4);
  border-radius: var(--radius-md);
  transition: all var(--transition-fast);
}

.nav-link:hover {
  color: var(--color-primary);
  background: var(--color-primary-bg);
}

.nav-link.active {
  color: var(--color-primary);
  font-weight: 700;
}
```

### フォーカスリング (アクセシビリティ必須)

```css
/* キーボードフォーカス表示 */
:focus-visible {
  outline: 3px solid var(--color-focus-ring);
  outline-offset: 2px;
}

/* マウス操作時はフォーカスリングを非表示 */
:focus:not(:focus-visible) {
  outline: none;
}
```

### フォーム要素

```css
/* テキスト入力 */
.input,
.textarea {
  font-family: var(--font-body);
  font-size: var(--text-base);
  padding: var(--space-3) var(--space-4);
  border: 2px solid var(--color-border);
  border-radius: var(--radius-md);
  background: var(--color-bg-card);
  color: var(--color-text-primary);
  transition: border-color var(--transition-fast);
  width: 100%;
}

.input:focus,
.textarea:focus {
  border-color: var(--color-primary);
  outline: 3px solid var(--color-focus-ring);
  outline-offset: 0;
}

.input::placeholder,
.textarea::placeholder {
  color: var(--color-gray-400);
}

.textarea {
  min-height: 120px;
  resize: vertical;
}

/* ラベル */
.label {
  font-family: var(--font-heading);
  font-weight: 500;
  font-size: var(--text-sm);
  color: var(--color-text-secondary);
  margin-bottom: var(--space-1);
  display: block;
}
```

### バッジ・タグ

```css
.badge {
  display: inline-block;
  font-family: var(--font-heading);
  font-size: var(--text-xs);
  font-weight: 700;
  padding: var(--space-1) var(--space-3);
  border-radius: var(--radius-full);
  background: var(--color-primary-bg);
  color: var(--color-primary-dark);
  letter-spacing: var(--tracking-wide);
}
```

### セクション見出し装飾

```css
/* ポップなセクション見出し */
.section-title {
  font-family: var(--font-heading);
  font-weight: 800;
  position: relative;
  display: inline-block;
}

/* 赤いアンダーラインアクセント */
.section-title::after {
  content: '';
  display: block;
  width: 60%;
  height: 4px;
  background: var(--color-primary);
  border-radius: var(--radius-full);
  margin-top: var(--space-2);
}
```

---

## 7. アニメーション・インタラクション

### ホバーエフェクト指針
- カード: `translateY(-4px)` + シャドウ拡大
- ボタン: `translateY(-2px)` + 赤い光彩シャドウ
- リンク: カラー変化 + 背景色変化
- 画像: `scale(1.02)` (コンテナで `overflow: hidden`)

### スクロールアニメーション

```css
/* フェードイン (Intersection Observer と組み合わせ) */
.animate-fade-in {
  opacity: 0;
  transform: translateY(20px);
  transition: opacity var(--transition-slow), transform var(--transition-slow);
}

.animate-fade-in.is-visible {
  opacity: 1;
  transform: translateY(0);
}
```

### アクセシビリティ配慮

```css
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
```

---

## 8. アイコン

### 方針
- 旧サイトの GIF アイコン → **SVG インラインアイコン**に置換
- アイコンライブラリ: [Lucide Icons](https://lucide.dev/) 推奨 (軽量・MIT)
- サイズ: 20px (テキスト内), 24px (UI), 32–48px (フィーチャー)
- カラー: `currentColor` を使い、親要素の色を継承

### サービスアイコンのマッピング (旧→新)

| 旧サイト (GIF) | 新サイト (Lucide等) | 用途 |
|----------------|-------------------|------|
| website_icon.gif | `Monitor` / `Globe` | WEB制作 |
| develop_icon.gif | `Settings` / `Code` | システム開発 |
| tablet_icon.gif | `Smartphone` | アプリ開発 |
| manage_icon.gif | `RefreshCw` / `Shield` | サイト運営 |

---

## 9. 画像・メディア

### 画像ルール
- **フォーマット**: WebP 優先、JPEG フォールバック (PNG は透過が必要な場合のみ)
- **遅延読み込み**: `loading="lazy"` を全画像に付与 (ファーストビュー除く)
- **アスペクト比**: `aspect-ratio` で CLS を防止
- **レスポンシブ**: `srcset` / `sizes` で適切なサイズを配信

### 旧サイトアセット再利用
- `logo.gif` → SVG 再作成 (スケーラブル化)
- `bg.jpg` (テクスチャ) → 不要 (モダンなフラットデザインに移行)
- `footer_illust.gif` → CSS/SVG で再現 or 新規イラスト
- サービスアイコン → SVG アイコンに置換

---

## 10. フッター

### 旧サイトからの進化
- 旧: 赤背景 + GIF イラスト + 白テキスト
- 新: ダーク背景 (`--color-gray-900`) + 赤いアクセントライン

```css
.footer {
  background: var(--color-gray-900);
  color: var(--color-gray-400);
  padding: var(--space-16) 0 var(--space-8);
  border-top: 3px solid var(--color-primary);
}

.footer a {
  color: var(--color-gray-300);
  transition: color var(--transition-fast);
}

.footer a:hover {
  color: var(--color-primary-light);
}
```

---

## AI アシスタント向け指示

このスキルが参照された場合:

1. **CSS 変数を必ず使う** — カラー・フォント・スペーシングは全て `var(--xxx)` で指定
2. **ハードコード禁止** — `#e61e1e` や `16px` などの直値は `:root` 定義以外で使わない
3. **モバイルファースト** — 基本スタイルは SP 向け、`min-width` メディアクエリで PC 拡張
4. **旧サイトの赤を大切に** — `--color-primary: #e61e1e` をブランドの核として扱う
5. **ポップだが散らかさない** — アニメーションは subtle に、アクセントカラーは1ページ最大2色
6. **`prefers-reduced-motion`** — アニメーション実装時は必ず配慮する
7. **フォント** — 見出しは `M PLUS Rounded 1c`、本文は `Noto Sans JP` を徹底
8. **コントラスト比** — WCAG AA (4.5:1) 厳守。`--color-primary` は14px以下のテキストに使用禁止、代わりに `--color-primary-dark` を使う
9. **フォーカスリング** — インタラクティブ要素には `:focus-visible` スタイルを必ず実装
10. **リンクのアクセシビリティ** — テキストリンクには下線を付与し、色だけで区別しない
11. **グラデーション禁止** — `linear-gradient` / `radial-gradient` は使用しない。安っぽく AI 生成感が出るため。背景色は単色 (CSS変数) で指定すること
