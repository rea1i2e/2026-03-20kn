# JavaScript

---

## モジュール構成

- **ES6モジュール形式（`import`/`export`）を使う** — グローバル汚染を防ぎ、依存関係を明示するため。
- **モジュールファイルはアンダースコア始まりで命名する** — エントリーポイントと区別するため。
  - 例: `_drawer.js`, `_slider.js`

```javascript
// index.js（エントリーポイント）
import './_drawer.js';
import './_slider.js';
```

---

## 要素の存在確認（早期return）

- **対象要素がない場合は早期returnする** — 不要な処理を防ぎ、エラーを回避するため。
  - 例: `const el = document.getElementById('js-top-mv'); if (!el) return;`

```javascript
// ✅
const el = document.getElementById('js-top-mv');
if (!el) return;
new Splide(el, { type: 'fade' }).mount();

// ❌
if (el) { new Splide(el, { type: 'fade' }).mount(); }
```

---

## セレクタ運用

- **JSで操作する要素は `js-` 接頭辞または `data-*` 属性で管理する** — スタイル用クラスとJS用セレクタを分離するため。
  - 例（ID）: `id="js-drawer"`, `id="js-header"`
  - 例（data属性）: `data-fadein`
  - 例外: 既存実装が別の方針を取っている場合は既存に合わせる

---

## アクセシビリティ

- **インタラクティブ要素の状態変化時は `aria-*` 属性を更新する** — スクリーンリーダーに状態を伝えるため。
  - 例: ドロワー開閉時に `aria-expanded` / `aria-hidden` を切り替える

```javascript
menuButton.setAttribute('aria-expanded', isOpen ? 'true' : 'false');
drawer.setAttribute('aria-hidden', isOpen ? 'false' : 'true');
```

---

## アニメーション（GSAP）

- **ScrollTrigger を使う場合は `gsap.registerPlugin(ScrollTrigger)` を明示する** — プラグインの登録漏れを防ぐため。
- **デバイス分岐は `matchMedia()` ベースで行う** — CSSブレークポイントと一致させるため。
