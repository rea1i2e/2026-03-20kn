# ai-web-knowledge

Web制作における実務ナレッジを蓄積・再利用するためのリポジトリ。

---

## ディレクトリの役割

| ディレクトリ | 役割 |
|---|---|
| `stock/` | 過去案件から抽出した具体的な知見。案件ごとに1ファイル。 |
| `coding-rules/` | stockから昇格した汎用ルール。Cursorが参照する実装方針。 |
| `asset-compression/` | 画像・動画・フォントの圧縮・変換・設置の考え方。 |
| `prompts/` | ナレッジ抽出・ルール化に使うプロンプト集。 |
| `formats/` | ルールやナレッジを書くためのフォーマット定義。 |

### stock と coding-rules の違い

- **stock** → 案件固有の具体的な知見。「このときこうした」という記録。
- **coding-rules** → 複数案件に共通する汎用ルール。「常にこうする」という方針。

---

## 前提テンプレートリポジトリ

このリポジトリのナレッジは以下のテンプレートを前提としている。

- 静的サイト: [t2025-10-01vite](https://github.com/rea1i2e/t2025-10-01vite)
- WordPress: [t2025-12-24vite-wp](https://github.com/rea1i2e/t2025-12-24vite-wp)

---

## 基本的な使い方

1. **案件終了後** → `prompts/stock-extraction.md` のプロンプトで `stock/` にナレッジを追加する
2. **共通点が見えてきたら** → `prompts/rule-extraction.md` のプロンプトで `coding-rules/` にルールを昇格させる
3. **実装中** → `coding-rules/` を参照して判断の基準にする

---

## コーディングルール 一覧
この一覧は、テンプレ側 `制作テンプレート/t2025-10-01vite/AGENTS.md` から参照される想定です。

| ファイル | 内容 |
|---------|------|
| [common.md](./coding-rules/common.md) | 実装前・設計・判断基準など全体共通の方針 |
| [php.md](./coding-rules/php.md) | PHP（配列記法・データ分離・WordPress固有） |
| [ejs-html.md](./coding-rules/ejs-html.md) | EJS / HTML（テンプレート・データ分離・出力演算子） |
| [sass.md](./coding-rules/sass.md) | Sass/SCSS（BEM・プレフィックス・サイズ・メディアクエリ） |
| [javascript.md](./coding-rules/javascript.md) | JavaScript（モジュール・早期return・セレクタ・アクセシビリティ） |
| [video.md](./coding-rules/video.md) | 動画（属性セット・用途別記述パターン・PHP） |

---

## コーディングルール 早引き

### 必ず守るルール（全案件共通）

- HTMLタグ内のテキストコンテンツは自動補完しない → [ejs-html.md](./coding-rules/ejs-html.md), [php.md](./coding-rules/php.md)
- データ取得とHTML記述は分離する → [php.md](./coding-rules/php.md), [ejs-html.md](./coding-rules/ejs-html.md)
- PHPの配列は `[]` で書く → [php.md](./coding-rules/php.md)
- SCSSのネストは `mq()` 以外では使わない → [sass.md](./coding-rules/sass.md)
- JSで操作する要素は `js-` 接頭辞または `data-*` で管理する → [javascript.md](./coding-rules/javascript.md)

### 迷ったとき

- 命名・構造・コメントスタイルは既存実装を先に確認する → [common.md](./coding-rules/common.md)
