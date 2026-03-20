# コーディングルール 目次

Web制作全般に適用する共通ルール集。案件を問わず常に参照する。

---

## ルール一覧

| ファイル | 内容 |
|---------|------|
| [common.md](./common.md) | 実装前・設計・判断基準など全体共通の方針 |
| [php.md](./php.md) | PHP（配列記法・データ分離・WordPress固有） |
| [ejs-html.md](./ejs-html.md) | EJS / HTML（テンプレート・データ分離・出力演算子） |
| [sass.md](./sass.md) | Sass/SCSS（BEM・プレフィックス・サイズ・メディアクエリ） |
| [javascript.md](./javascript.md) | JavaScript（モジュール・早期return・セレクタ・アクセシビリティ） |

---

## 早引き

### 必ず守るルール（全案件共通）

- HTMLタグ内のテキストコンテンツは自動補完しない → [ejs-html.md](./ejs-html.md), [php.md](./php.md)
- データ取得とHTML記述は分離する → [php.md](./php.md), [ejs-html.md](./ejs-html.md)
- PHPの配列は `[]` で書く → [php.md](./php.md)
- SCSSのネストは `mq()` 以外では使わない → [sass.md](./sass.md)
- JSで操作する要素は `js-` 接頭辞または `data-*` で管理する → [javascript.md](./javascript.md)

### 迷ったとき

- 命名・構造・コメントスタイルは既存実装を先に確認する → [common.md](./common.md)
