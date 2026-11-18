# CLAUDE.md

色管理 (カラーサイエンス) のドキュメントサイト。GitHub Pages でそのまま公開する静的 HTML。
ツール本体は隣のリポジトリ `../dev-colormanagement` (colorchart)。

**Claude Code は基本的に `../dev-colormanagement` をメインの作業ディレクトリとして使い、このリポジトリはそこから編集する。**
2 つのリポジトリの関係・作業の流れ・コミットの分け方は `../dev-colormanagement/CLAUDE.md` の
「2 つのリポジトリの関係」が正。このファイルには、このリポジトリの中の約束だけを書く。

## 進め方

- 会話・説明・コミットメッセージは日本語。ユーザーは技術初学者なので、専門用語は初出で一言説明する
- ページの追加・大きな書き換えは、方針を説明して了承を得てから着手する
- コミットは指示があるまでしない。指示があったらメッセージ案を見せてからコミットする

## 構成

- `.nojekyll` — GitHub Pages に Markdown 変換 (Jekyll) をさせず、ファイルをそのまま公開させる目印。消さない
- `index.html` — トップページ
- `knowledge.html` — 用語と考え方。人ではなく Claude が HTML を直接書く前提
- `assets/style.css` — index / knowledge 共通の見た目 (色はすべて `:root` の変数。ダークモード対応)
- `reports/` — ツールが自動生成するレポート (HTML + JSON)。**手で編集しない**。
  作り直しはツール側で `colorchart reference --out ../color-science-docs/reports/charts.html` など

## 書き方の約束

- 外部ファイル (フォント・CDN・画像 URL) は読み込まない。オフラインでも同じ表示にする
- 章・小見出し・用語索引には英字の固定 id を付け、**見出しの文言を変えても id は変えない**。
  ツール側 (`dev-colormanagement/src/colorchart/reference_html.py` の `KNOWLEDGE_ANCHORS`) が
  `knowledge.html#<id>` にリンクしており、テストで実在を確かめている。id を変える・消すときはツール側も直す
- 用語索引 (`#glossary`) の表の 1 列目は用語名だけを書く (ツール側テストが照合する)
- 色の数値・規格の値を書くときは出典 (規格名・ライブラリ名) を添える
- スマホ幅 (375px) でも横にはみ出さない。広い表は `.table-wrap` で囲んで横スクロールにする
