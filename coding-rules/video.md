# 動画の実装

動画を HTML / PHP で記述するときのルール。圧縮・フォーマット選定は [asset-compression/compression-video.md](../asset-compression/compression-video.md) を参照。

---

## 属性セット

- **ループ背景・ヒーロー動画には原則 `autoplay muted loop playsinline` を付ける** — `muted` がないと自動再生がブロックされる。`playsinline` はモバイルでのインライン再生に必要。
  - 例外: コンテンツ動画（説明・紹介）には付けない
- **`<video>` タグは WebM → MP4 の順に `<source>` を記述する** — 対応ブラウザが WebM を優先して使い、非対応ブラウザは MP4 にフォールバックする。
- **ヒーロー動画には `preload="metadata"` を指定する** — 動画全体の先読みを抑えて初期表示への影響を最小化する。
- **コンテンツ動画には `controls` を付ける** — ユーザーが再生・停止・音量を操作できるようにする。

---

## 用途別の記述パターン

### ループ背景・装飾動画

```html
<video autoplay muted loop playsinline>
  <source src="/assets/videos/bg.webm" type="video/webm">
  <source src="/assets/videos/bg.mp4" type="video/mp4">
</video>
```

### ヒーロー動画（FV 画面いっぱい）

画面全体を覆うレイアウトは CSS で制御する。`preload="metadata"` で初期読み込みを抑える。

```html
<video autoplay muted loop playsinline preload="metadata">
  <source src="/assets/videos/hero.webm" type="video/webm">
  <source src="/assets/videos/hero.mp4" type="video/mp4">
</video>
```

### コンテンツ動画（説明・紹介）

```html
<video controls>
  <source src="/assets/videos/intro.mp4" type="video/mp4">
</video>
```

---

## PHP（WordPress）での記述

WordPress テーマでは `ty_theme_asset_url()` でハッシュ付きパスを解決する。

```php
<video autoplay muted loop playsinline preload="metadata">
  <source src="<?= esc_url(ty_theme_asset_url('src/assets/videos/hero.webm')) ?>" type="video/webm">
  <source src="<?= esc_url(ty_theme_asset_url('src/assets/videos/hero.mp4')) ?>" type="video/mp4">
</video>
```
