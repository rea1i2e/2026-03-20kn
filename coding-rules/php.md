# PHP

---

## 配列記法

- **配列は `[]` で書く** — `array()` は冗長で古い記法のため使わない。
  - 例: `$items = ['key' => 'value'];`
  - 例外: 外部配布・既存資産をそのまま流用している箇所は、改修時のみ方針に寄せる

---

## データとHTMLの分離

- **データ取得とHTML出力は分離する** — ロジックと描画が混在すると読みにくく、保守コストが上がるため。
  - 例: PHPブロックでデータを組み立て、その後にHTMLを出力する

```php
<?php
$nav_items = [
  ['slug' => 'about', 'text' => ''],
  ['slug' => 'news',  'text' => ''],
];
?>
<nav>
  <?php foreach ($nav_items as $item): ?>
    <a href="<?php page_path($item['slug']); ?>"><?php echo esc_html($item['text']); ?></a>
  <?php endforeach; ?>
</nav>
```

---

## 早期return

- **条件を満たさない場合は早期returnする** — ネストが深くなるのを防ぎ、意図が読みやすくなるため。
  - 例: `if (!$query->have_posts()) return;`
  - 例外: 複数の条件が絡む場合は可読性を優先して判断する

---

## テキストコンテンツの自動補完禁止

- **HTMLタグ内のテキストは自動補完しない** — デザイン・要件にある文言のみを使用する。
  - 例: 見出し・段落・ボタン文字は設計の文言（または既存実装）から参照する

---

## WordPress固有

- **関数には `my_` プレフィックスを付ける** — テーマ固有関数の名前衝突を防ぐため。
  - 例: `function my_setup() { ... }`

- **コンポーネントは `get_template_part()` で読み込む** — 再利用性と構造の明確化のため。
  - 例: `get_template_part('components/c-heading', null, ['en' => 'News', 'ja' => '']);`

- **出力は必ずエスケープする** — XSS対策のため、用途に応じた関数を使う。

| 用途 | 関数 |
|------|------|
| 通常テキスト | `esc_html()` |
| 属性値 | `esc_attr()` |
| URL | `esc_url()` |
| HTML許可 | `wp_kses_post()` |
