<p align="center"><img src="assets/logo.svg" width="80" alt="AI Safety HOT"></p>

<p align="center"><a href="README.md">简体中文</a> · <a href="README.en.md">English</a> · <strong>日本語</strong></p>

<h1 align="center">AI Safety HOT Hub</h1>

<p align="center"><strong>エージェントでニュースを調べ、論文を読み、出来事を追い、AI安全性のブリーフィングをまとめましょう。</strong></p>

<p align="center">攻撃とジェイルブレイク · 防御とガードレール · アラインメントと安全性評価 · AIインシデント · マルチエージェントの安全性リスク · ガバナンスと政策</p>

<p align="center">
  <a href="https://aisafetyhot.com"><img src="https://img.shields.io/badge/%F0%9F%8C%90%20%E3%82%A6%E3%82%A7%E3%83%96%E3%82%B5%E3%82%A4%E3%83%88-aisafetyhot.com-2563eb?style=flat-square" alt="🌐 ウェブサイト：aisafetyhot.com"></a>
  <a href="https://aisafetyhot.com"><img src="https://img.shields.io/badge/%E6%97%A5%E5%A0%B1-%E6%AF%8E%E6%97%A5%2008%3A00%20%E5%8C%97%E4%BA%AC%E6%99%82%E9%96%93-d97706?style=flat-square" alt="毎日北京時間08:00に日報を公開"></a>
  <a href="#agent"><img src="https://img.shields.io/badge/%E3%82%A8%E3%83%BC%E3%82%B8%E3%82%A7%E3%83%B3%E3%83%88-MCP-2563eb?style=flat-square" alt="エージェント接続：MCP"></a>
  <a href="#papers"><img src="https://img.shields.io/badge/%E8%AB%96%E6%96%87-Markdown%20%2F%20BibTeX%20%2F%20JSON-16856b?style=flat-square" alt="3つの形式で提供する論文リスト"></a>
</p>

<p align="center">
  <a href="#agent">エージェントを接続</a> ·
  <a href="#examples">使い方を見る</a> ·
  <a href="#daily">最新の日報</a> ·
  <a href="https://aisafetyhot.com/all?view=graph">可視化</a> ·
  <a href="#papers">関連論文</a> ·
  <a href="https://aisafetyhot.com/hot">注目の出来事</a> ·
  <a href="https://aisafetyhot.com">ウェブサイトを見る ↗</a>
</p>

<p align="center">
  <a href="https://aisafetyhot.com"><img src="assets/news-monitor-demo.gif" width="1000" alt="AI Safety HOTのニュース一覧と可視化のデモ"></a>
</p>

<p align="center">デモの操作画面は中国語です。</p>

このリポジトリは、[AI Safety HOT](https://aisafetyhot.com)の**エージェント接続ガイドと公開コンテンツのアーカイブ**です。MCPを使ってニュースの検索、論文の読解、出来事の追跡、ブリーフィングの作成ができます。論文リストはMarkdown、BibTeX、JSON形式で持ち出せます。

このREADMEは日本語のガイドです。リンク先の補足ドキュメント、日報、アーカイブ、およびサービスが提供するコンテンツは、現在主に中国語です。最新の日報と論文一覧は、以下の中国語版・アーカイブへのリンクから確認できます。

**役に立ったら、GitHubでStarを付けていただけるとうれしいです。**

<a id="agent"></a>

## 🤖 エージェントを接続する

公開MCPサービスなので、ログインもAPI Keyも不要です。利用するクライアントに対応したコマンドをターミナルで実行し、クライアントのセッションを開き直してください。

**Codex**

```bash
codex mcp add aisafetyhot --url https://aisafetyhot.com/api/mcp
```

**Claude Code**

```bash
claude mcp add --transport http --scope user aisafetyhot https://aisafetyhot.com/api/mcp
```

その他のクライアントでは、名前に`aisafetyhot`、アドレスに`https://aisafetyhot.com/api/mcp`を入力し、接続方式に**Streamable HTTP**を選択してください。

### できること

| やりたいこと | MCPツール | 取得できる内容 |
|---|---|---|
| 最新の動向を知る | `aisafetyhot_get_latest` | 全記事または厳選記事、要約、出典、次のページへの情報 |
| ニュースや論文を探す | `aisafetyhot_search` | キーワード、トピック、カテゴリ、日付で検索した既存のコンテンツ |
| 研究トピックを探す | `aisafetyhot_get_topics` | トピック名、識別子、定義、関連トピック |
| 1件のコンテンツを読む | `aisafetyhot_get_content` | 要約、原文リンク、既存の論文解説 |
| 注目の出来事を知る | `aisafetyhot_get_hot_topics` | 現在の出来事ランキング、関連する情報源、関連リンク数 |
| 出来事を追跡する | `aisafetyhot_get_story` | 出来事の概要、関連報道の時系列、議論 |
| 日報・週報・月報を読む | `aisafetyhot_get_daily` | 公開済みのレポート、または選択できる発行号の一覧 |

<a id="parameters"></a>

### パラメータ早見表

表のツール名では、共通の接頭辞`aisafetyhot_`を省略しています。パラメータは質問に応じてエージェントに指定させることができます。すべての設定値、既定値、呼び出し方は、MCPが提供するツール説明を参照してください。

| パラメータ | 使用するツール | 意味と主な設定値 |
|---|---|---|
| `q` | `search` | 検索キーワード。必須。例：`prompt injection` |
| `mode` | `get_latest`、`search` | `all`はすべての公開記事、`selected`は厳選記事のみを検索 |
| `mode` | `get_latest` | `snapshot`／`changes`は厳選記事の集合全体を同期。カテゴリ、トピック、日付による絞り込みには非対応 |
| `mode` | `get_daily` | `read`は1号を読む、`list`は公開済みの発行号を一覧表示 |
| `window` | `get_latest`、`search` | `24h`は直近1日、`7d`は直近1週間、`all`は過去のコンテンツも含む |
| `by` | `get_latest`、`search` | `timeline`はサイトのタイムライン順に並べ、日付範囲をサイトへの収録時刻で絞り込む。`published`は原文の公開日で並べ替え・絞り込み |
| `category` | `get_latest`、`search` | カテゴリコード：`attack`攻撃、`defense`防御、`alignment`アラインメント、`eval`評価、`incident`インシデント、`industry`ガバナンス、`tip`ツール、`opinion`意見、`ai_news`AIの動向 |
| `topic` | `get_latest`、`search` | トピック識別子。`get_topics`が返すslugを使用 |
| `from` | `get_latest`、`search` | 開始日またはタイムゾーン付きの時刻。開始点を含む |
| `until` | `get_latest`、`search` | 終了日またはタイムゾーン付きの時刻。終了点を含まない |
| `limit` | `get_latest`、`search`、`get_daily`、`get_hot_topics` | 返す件数。ページ分割するツールは1ページ1–50件、注目ランキングは上位1–10件。レポートでは`list`モードのみで使用 |
| `cursor` | `get_latest`、`search`、`get_story`、`get_daily` | 次のページの識別子。通常のページ送りでは`page.nextCursor`を使用。レポートでは`list`モードのみで使用 |
| `id` | `get_content` | ニュースまたは論文のID。必須。検索結果から取得 |
| `public_id` | `get_story` | 出来事のID。必須。結果に含まれる`publicId`を使用 |
| `depth` | `get_content`、`get_story` | `summary`は簡潔な内容を返す。`full`は既存の本文・論文解説、または出来事に関する報道の要約を含める |
| `max_chars` | `get_content` | 本文、論文の要約・解説に割り当てる文字数の上限。1000–30000 |
| `report_limit` | `get_story` | 1ページに返す関連報道の件数。1–50 |
| `period` | `get_daily` | `daily`は日報、`weekly`は週報、`monthly`は月報 |
| `key` | `get_daily` | 読み取りモードで指定する発行号：`YYYY-MM-DD`、`YYYY-Www`、`YYYY-MM`。省略すると最新号を読む |
| `date` | `get_daily` | 読み取りモードで使う旧形式の日報の日付。`YYYY-MM-DD`。新規の呼び出しでは`key`を使用可能 |
| `slug` | `get_topics` | 特定のトピックを指定。省略すると設定済みの全トピックを一覧表示 |

過去のコンテンツを検索する場合は`window="all"`を指定してください。日付だけを指定した`from`／`until`は、UTCの午前0時として解釈されます。厳選記事を同期する際のカーソルの扱いは、[詳しい説明（中国語）](docs/agent.md#续接精选变化)を参照してください。

<a id="examples"></a>

### 試してみる

接続したら、自然な言葉で質問してください。MCPがツール説明とパラメータ定義を提供し、エージェントがそれに基づいて呼び出すツールを選びます。

| 試したいこと | 質問例 | 結果 |
|---|---|---|
| 新しい記事を見る | 「過去24時間に収録された厳選記事を3件挙げて、出典と原文リンクを付けてください。」 | [タイトル、要約、出典、ページ送り（中国語）](docs/mcp-examples.md#latest) |
| トピックを調べる | 「プロンプトインジェクションに関する論文を探し、そのうち1本を開いて研究で分かったことを説明してください。」 | [検索結果と既存の論文解説（中国語）](docs/mcp-examples.md#topics) |
| ブリーフィングを準備する | 「最新の週報を読み、テーマと閲覧リンクを一覧にしてください。」 | [発行号、対象期間、テーマ（中国語）](docs/mcp-examples.md#reports) |

リンク先の結果例は2026-10-07（メルボルン）時点のものです。実際の検索結果はサイトの更新に伴って変わります。

回答にはサイト内リンクと原文リンクを残してください。`page.hasMore`がtrueなら次のページも読み、欠落や切り詰めの有無は`completeness`で確認してください。インターフェースは既存の公開コンテンツを読み取ります。論文解説は二次資料なので、重要な事実は原文で確認してください。

[エージェントの使い方とパラメータ説明（Skill、中国語）](skills/aisafetyhot/SKILL.md) · [呼び出しと結果の例（中国語）](docs/mcp-examples.md) · [取得範囲と注意事項（中国語）](docs/agent.md#读取范围)

<a id="daily"></a>

## 🗞️ 毎日のAI安全性日報

最新の日報と過去の号は、以下のリンクから確認できます。日報本文は中国語です。

- [最新の日報（中国語）](README.md#daily)
- [日報アーカイブ（中国語）](daily)
- [ウェブサイトで日報を読む（中国語）](https://aisafetyhot.com/daily)

> 日報は毎日北京時間（UTC+8）**08:00**に公開され、Hubは**15分ごと**に更新を確認します。中国語版READMEでは新しい号の公開後に日報欄が置き換わり、過去の号は[日報アーカイブ（中国語）](daily)に保存されます。

<a id="papers"></a>

## 📚 論文リストをダウンロードする

2026-09-24以降、毎日サイトに収録され、AI安全性に関するものと判定された論文を日付別に保存しています。生成済みの中国語の導入解説と論文要約はリストに含まれ、その後の解説も順次追加されます。

| やりたいこと | 使用するファイル |
|---|---|
| 論文のタイトル、導入解説、要約を読む | [Markdownリスト（中国語）](papers) |
| Zotero、EndNote、論文の参考文献に取り込む | `papers/YYYY/YYYY-MM-DD.bib` |
| エージェントに渡す、メモを作る、自分のスクリプトに取り込む | `papers/YYYY/YYYY-MM-DD.json` |

論文要約では、**研究課題、方法、実験と結果、限界**を整理し、各論文の出典を示しています。★は厳選記事への選出を表します。注目度はAI安全性に関心のある読者向けの参考指標であり、論文の質を示すものではありません。

arXiv論文のLaTeXソースファイル（source）をダウンロードするには、[arxiv2agent](https://github.com/wuyoscar/arxiv2agent)も利用できます。

<details>
<summary><strong>最新の日報と論文ダウンロードへのリンクを開く</strong></summary>

- [最新の日報と論文ダウンロード（中国語）](README.md#papers)
- [2026年の目次（中国語）](archive/2026.md)
- [論文リスト（中国語）](papers)

論文リストは北京時間（UTC+8）の暦日（00:00から24:00まで）ごとに、サイトのタイムライン上の時刻を基準に分類します。日報の対象期間は、北京時間の前日08:00から当日08:00までです。日付の区切りが異なるため、同じ日付の日報と論文リストに含まれる論文は完全には一致せず、隣接する日付の日報に掲載されることもあります。直近7日分について、サイトでの論文の取り下げ、修正、追加を1時間ごとに確認し、変更があれば該当日のリストに同期します。

[status.json](status.json)には、各日の論文数、IDのダイジェスト、同期の制限時間を記録しています。`slaMinutes`は、サイト上の論文がこのリポジトリに反映されるまでの最大許容時間を分単位で表します。

</details>

## 🔎 ウェブサイトで見られるもの

[全記事（中国語）](https://aisafetyhot.com/all)は随時更新 · [注目ランキング（中国語）](https://aisafetyhot.com/hot)で出来事の進展を追跡 · [可視化（中国語）](https://aisafetyhot.com/all?view=graph)で情報源・ニュース・論文と研究分野のつながりを確認 · [週報（中国語）](https://aisafetyhot.com/weekly)で1週間を振り返る · [月報（中国語）](https://aisafetyhot.com/monthly)で1か月を振り返る

**お使いのRSSリーダーで購読：** [厳選記事RSS（中国語）](https://aisafetyhot.com/feed.xml) · [全記事RSS（中国語）](https://aisafetyhot.com/feed/all.xml) · [日報RSS（中国語）](https://aisafetyhot.com/feed/daily.xml)

## ☕ 支援とフィードバック

ウェブサイトもHubも無料です。資料探しの時間短縮に役立ったら、[作者にコーヒーをごちそうする](https://buymeacoffee.com/wuyoscar)ことで、サーバーとモデル呼び出しの費用をご支援いただけます。

<details>
<summary>WeChatで支援する</summary>

<img src="assets/wechat-pay.png" width="160" alt="WeChatの支払い用QRコード">

</details>

誤りの報告、修正、取り下げの依頼は、[掲示板（中国語）](https://aisafetyhot.com/board)で「下架/更正」（取り下げ・修正）を選択してください。

---

AI Safety HOTはオープンソースフレームワーク[AIHOT](https://github.com/KKKKhazix/AIHOT)を基に構築しています。原作者に感謝します。導入解説はモデルによって生成されています。論文要約は、論文PDF（Geminiを使用）またはarXivの全文を基に作成しており、具体的な出典は各記録に記載しています。重要な数値や結論は原文を確認してください。

このリポジトリの導入解説、論文要約、日報の文章は[CC BY-NC 4.0](LICENSE)で提供します。転載する場合はAI Safety HOTをクレジットし、出典を残してください。商用利用は認められません。原文と論文の著作権は、それぞれの著者および情報源に帰属します。
