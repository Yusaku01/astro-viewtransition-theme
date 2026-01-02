# astro-viewtransition-theme

Astro theme toggle components with view transitions support.
Seamless dark/light mode switching for your Astro project.

---

Astroプロジェクト向けのテーマトグルコンポーネント。
View Transitions対応でシームレスなダーク/ライトモード切り替えを実現します。

## Features / 特徴

- **Zero flash** - No FOUC (Flash of Unstyled Content) with inline initialization
- **View Transitions ready** - Full support for Astro view transitions
- **Persistent** - Theme preference saved to localStorage
- **System aware** - Detects OS dark/light mode preference
- **Multi-toggle sync** - Multiple toggle buttons stay synchronized
- **Customizable** - Style via CSS variables
- **Accessible** - ARIA attributes and screen reader support
- **TypeScript** - Astro component types supported

---

- **フラッシュなし** - インライン初期化によりFOUC（スタイル未適用のフラッシュ）を防止
- **View Transitions対応** - AstroのView Transitionsを完全サポート
- **永続化** - テーマ設定をlocalStorageに保存
- **システム連携** - OSのダーク/ライトモード設定を自動検出
- **複数トグル同期** - ページ内の複数のトグルボタンが同期
- **カスタマイズ可能** - CSS変数でスタイリング
- **アクセシブル** - ARIA属性とスクリーンリーダー対応
- **TypeScript** - Astroの型サポートに対応

## Installation / インストール

```sh
npm install astro-viewtransition-theme
```

```sh
yarn add astro-viewtransition-theme
```

```sh
pnpm add astro-viewtransition-theme
```

## Quick Start / クイックスタート

```astro
---
import ThemeInit from 'astro-viewtransition-theme/ThemeInit';
import ThemeToggle from 'astro-viewtransition-theme/ThemeToggle';
---

<html lang="en">
  <head>
    <ThemeInit />
  </head>
  <body>
    <ThemeToggle />
  </body>
</html>
```

## Components / コンポーネント

### ThemeInit

Inline script that applies the theme immediately before the page renders, preventing any flash.

**Must be placed in `<head>`.**

How it works:
1. Checks localStorage for saved theme
2. Falls back to system preference (`prefers-color-scheme`)
3. Applies theme to `<html>` element

---

ページがレンダリングされる前にテーマを即座に適用するインラインスクリプト。フラッシュを防ぎます。

**必ず `<head>` 内に配置してください。**

動作の流れ：
1. localStorageに保存されたテーマを確認
2. なければシステム設定（`prefers-color-scheme`）にフォールバック
3. テーマを `<html>` 要素に適用

### ThemeToggle

Main component that handles theme switching logic and view transition events.

- Provides default `ThemeButton` if no slot content
- Accepts custom button via default slot
- Listens for `astro:before-swap` and `astro:page-load` events
- Syncs multiple toggle buttons on the same page

---

テーマ切り替えロジックとView Transitionイベントを処理するメインコンポーネント。

- スロットがなければデフォルトの `ThemeButton` を表示
- デフォルトスロットでカスタムボタンを受け付け
- `astro:before-swap` と `astro:page-load` イベントを監視
- ページ内の複数のトグルボタンを同期

### ThemeButton

Default styled toggle button with sun/moon icons and smooth animations.

- Accessible: `aria-label`, `aria-pressed`
- Animated thumb and icon transitions
- Fully customizable via CSS variables

---

Sun/Moonアイコンとスムーズなアニメーション付きのデフォルトスタイルトグルボタン。

- アクセシブル: `aria-label`, `aria-pressed` 対応
- つまみとアイコンのアニメーション
- CSS変数で完全にカスタマイズ可能

## Usage Examples / 使用例

### Basic Usage / 基本的な使い方

Minimal setup with default button:

デフォルトボタンでの最小構成：

```astro
---
import ThemeInit from 'astro-viewtransition-theme/ThemeInit';
import ThemeToggle from 'astro-viewtransition-theme/ThemeToggle';
---

<html lang="en">
  <head>
    <ThemeInit />
  </head>
  <body>
    <ThemeToggle />
  </body>
</html>
```

### With Explicit ThemeButton / ThemeButtonを明示的に使用

```astro
---
import ThemeInit from 'astro-viewtransition-theme/ThemeInit';
import ThemeToggle from 'astro-viewtransition-theme/ThemeToggle';
import ThemeButton from 'astro-viewtransition-theme/ThemeButton';
---

<html lang="en">
  <head>
    <ThemeInit />
  </head>
  <body>
    <ThemeToggle>
      <ThemeButton />
    </ThemeToggle>
  </body>
</html>
```

### Full Layout with View Transitions / View Transitions付きの完全なレイアウト

```astro
---
// src/layouts/Layout.astro
import { ClientRouter } from 'astro:transitions';
import ThemeInit from 'astro-viewtransition-theme/ThemeInit';
import ThemeToggle from 'astro-viewtransition-theme/ThemeToggle';
---

<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <ThemeInit />
    <ClientRouter />
  </head>
  <body>
    <header>
      <nav>
        <ThemeToggle />
      </nav>
    </header>
    <main>
      <slot />
    </main>
  </body>
</html>
```

### Custom Slot Content / カスタムスロットコンテンツ

Use your own button element with `data-theme-toggle` attribute:

`data-theme-toggle` 属性を持つ独自のボタン要素を使用：

```astro
---
import ThemeInit from 'astro-viewtransition-theme/ThemeInit';
import ThemeToggle from 'astro-viewtransition-theme/ThemeToggle';
---

<ThemeInit />
<ThemeToggle>
  <button data-theme-toggle aria-label="Toggle theme">
    Toggle
  </button>
</ThemeToggle>

<style>
  button {
    padding: 0.5rem 1rem;
    border-radius: 0.25rem;
    cursor: pointer;
  }
</style>
```

## Styling / スタイリング

### CSS Variables / CSS変数

Override these variables to customize the toggle button:

これらの変数をオーバーライドしてトグルボタンをカスタマイズ：

```css
/* Light theme (default) / ライトテーマ（デフォルト） */
:root {
  --toggle-track: #1f2632;   /* Track background / トラック背景 */
  --toggle-thumb: #f6f7f9;   /* Thumb color / つまみの色 */
  --toggle-icon: #7b8494;    /* Icon color / アイコンの色 */
  --accent: #1b6c8c;         /* Focus ring / フォーカスリング */
}

/* Dark theme / ダークテーマ */
html[data-theme='dark'] {
  --toggle-track: #2a3342;
  --toggle-thumb: #f2f4f7;
  --toggle-icon: #6f798c;
}
```

### Size Variables / サイズ変数

```css
:root {
  --toggle-width: 76px;       /* Total width / 全体の幅 */
  --toggle-height: 36px;      /* Total height / 全体の高さ */
  --toggle-padding: 4px;      /* Inner padding / 内側の余白 */
  --toggle-thumb-size: 28px;  /* Thumb diameter / つまみの直径 */
}
```

### Customization Example / カスタマイズ例

```css
/* Custom purple theme / カスタム紫テーマ */
:root {
  --toggle-track: #4c1d95;
  --toggle-thumb: #f3e8ff;
  --toggle-icon: #a78bfa;
  --accent: #7c3aed;
}

html[data-theme='dark'] {
  --toggle-track: #581c87;
  --toggle-thumb: #faf5ff;
  --toggle-icon: #c4b5fd;
}

/* Larger toggle / 大きいトグル */
:root {
  --toggle-width: 100px;
  --toggle-height: 48px;
  --toggle-thumb-size: 40px;
}
```

## How It Works / 仕組み

### Theme Storage / テーマの保存

- **localStorage key**: `theme`
- **Valid values**: `'dark'` | `'light'`

テーマは `localStorage` の `theme` キーに保存されます。

### HTML Attributes / HTML属性

The theme is applied via attributes on the `<html>` element:

テーマは `<html>` 要素の属性で適用されます：

| Attribute | Value | Description |
|-----------|-------|-------------|
| `data-theme` | `'dark'` \| `'light'` | Current theme / 現在のテーマ |
| `style.colorScheme` | `'dark'` \| `'light'` | Browser color scheme / ブラウザのカラースキーム |

### CSS Selectors / CSSセレクター

Use these selectors in your styles:

スタイルでこれらのセレクターを使用：

```css
/* Dark mode styles / ダークモードのスタイル */
html[data-theme='dark'] {
  --bg-color: #0f172a;
  --text-color: #f1f5f9;
}

/* Light mode styles / ライトモードのスタイル */
html[data-theme='light'] {
  --bg-color: #ffffff;
  --text-color: #0f172a;
}
```

### View Transitions Integration / View Transitionsとの連携

The library handles Astro view transition events automatically:

ライブラリはAstroのView Transitionイベントを自動で処理します：

| Event | Action |
|-------|--------|
| `astro:before-swap` | Applies theme to new document before swap / スワップ前に新しいドキュメントにテーマを適用 |
| `astro:page-load` | Syncs toggle button states after load / ロード後にトグルボタンの状態を同期 |

## TypeScript

Import components via subpath:

型サポート付きでコンポーネントをインポート：

```typescript
import ThemeInit from 'astro-viewtransition-theme/ThemeInit';
import ThemeToggle from 'astro-viewtransition-theme/ThemeToggle';
import ThemeButton from 'astro-viewtransition-theme/ThemeButton';
```

## License / ライセンス

MIT
