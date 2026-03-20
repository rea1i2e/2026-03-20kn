# Sass/SCSS

---

## クラス名プレフィックス

- **クラス名は用途に応じたプレフィックスを付ける** — 役割が一目でわかり、命名の迷いをなくすため。

| プレフィックス | 用途 | 例 |
|--------------|------|-----|
| `p-` | パーツ（ページ固有コンポーネント） | `.p-header`, `.p-top-mv` |
| `l-` | レイアウト | `.l-header`, `.l-inner` |
| `c-` | 汎用UIコンポーネント | `.c-button`, `.c-heading` |
| `u-` | ユーティリティ | `.u-sp`, `.u-pc` |
| `js-` | JS操作対象（IDに使用） | `#js-drawer` |

---

## BEM記法（フラット記述）

- **ネストは `mq()` 以外では使わない** — ネストが深いと詳細度が上がり、上書きしにくくなるため。
  - 例: Block / Element / Modifier はすべてフラットに並べる

```scss
// ✅
.p-header { background-color: #ccc; }
.p-header.is-show { background-color: #eee; }
.p-header__inner { display: flex; }
.p-header__logo { width: rem(40); }

// ❌ ネストは使わない
.p-header {
  &__inner { display: flex; }
  &__logo { width: rem(40); }
}
```

---

## サイズ指定

- **サイズは `rem()` 関数を使う** — pxの直書きを避け、スケールの一貫性を保つため。
  - 例: `width: rem(40);`, `padding-inline: rem($padding-sp);`

- **`font-size` は `maxrem()` を使う** — 最小10px保証が必要なため。
  - 例: `font-size: maxrem(14);`

---

## メディアクエリ

- **レスポンシブは `mq()` ミックスインを使う** — 直書きを避け、ブレークポイントを一元管理するため。
- **モバイルファーストで書く** — デスクトップ向けスタイルを `mq()` 内に書く。

```scss
.p-header__pc-nav {
  display: none;
  @include mq() { display: block; }
}
```

---

## @use構文

- **`@import` は使わず `@use` を使う** — `@import` は非推奨のため。
  - 例: コンポーネントファイルの先頭に `@use "global" as *;`

---

## 禁止事項

- **SCSSで `id` セレクタを使わない** — 詳細度が高くなりすぎ、上書きが困難になるため。
  - 例外: JSと連携する `#js-...` は HTML側の属性として使うが、SCSSのセレクタには使わない
