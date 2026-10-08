<p align="center"><img src="assets/logo.svg" width="80" alt="AI Safety HOT"></p>

<p align="center"><a href="README.md">简体中文</a> · <strong>English</strong> · <a href="README.ja.md">日本語</a></p>

<h1 align="center">AI Safety HOT Hub</h1>

<p align="center"><strong>Let your Agent find news, read papers, follow events, and prepare AI safety briefings.</strong></p>

<p align="center">Attacks and jailbreaks · Defenses and guardrails · Alignment and safety evaluations · AI incidents · Multi-agent safety risks · Governance and policy</p>

<p align="center">
  <a href="https://aisafetyhot.com"><img src="https://img.shields.io/badge/%F0%9F%8C%90%20Website-aisafetyhot.com-2563eb?style=flat-square" alt="🌐 Website: aisafetyhot.com"></a>
  <a href="https://aisafetyhot.com"><img src="https://img.shields.io/badge/Daily%20digest-Daily%2008%3A00%20Beijing%20%28UTC%2B8%29-d97706?style=flat-square" alt="Daily digest published at 08:00 Beijing time (UTC+8)"></a>
  <a href="#agent"><img src="https://img.shields.io/badge/Agent-MCP-2563eb?style=flat-square" alt="Agent MCP"></a>
  <a href="#papers"><img src="https://img.shields.io/badge/Papers-Markdown%20%2F%20BibTeX%20%2F%20JSON-16856b?style=flat-square" alt="Paper lists in three formats"></a>
</p>

<p align="center">
  <a href="#agent">Connect your Agent</a> ·
  <a href="#examples">See how to use it</a> ·
  <a href="#daily">Daily digest</a> ·
  <a href="https://aisafetyhot.com/all?view=graph">Visualization</a> ·
  <a href="#papers">Related papers</a> ·
  <a href="https://aisafetyhot.com/hot">Trending events</a> ·
  <a href="https://aisafetyhot.com">Visit the website ↗</a>
</p>

<p align="center">
  <a href="https://aisafetyhot.com"><img src="assets/news-monitor-demo.gif" width="1000" alt="Animated demo of the AI Safety HOT news list and visualization"></a>
</p>

<p align="center">The demo interface is in Chinese.</p>

This is the **Agent connection guide and public content archive** for [AI Safety HOT](https://aisafetyhot.com). Use MCP to find news, read papers, follow events, and prepare briefings, or download paper lists in Markdown, BibTeX, and JSON.

This is the English guide. Linked documentation, daily digests, archives, and service content are currently primarily in Chinese.

**If you find it useful, please give the project a Star on GitHub.**

<a id="agent"></a>

## 🤖 Connect your Agent

The public MCP service requires no login or API key. Run the command for your client in a terminal, then reopen the client session.

**Codex**

```bash
codex mcp add aisafetyhot --url https://aisafetyhot.com/api/mcp
```

**Claude Code**

```bash
claude mcp add --transport http --scope user aisafetyhot https://aisafetyhot.com/api/mcp
```

For other clients, set the name to `aisafetyhot`, the URL to `https://aisafetyhot.com/api/mcp`, and the connection type to **Streamable HTTP**.

### What you can do

| What you want to do | MCP tool | What you get |
|---|---|---|
| See the latest updates | `aisafetyhot_get_latest` | All updates or selected items, with summaries, sources, and pagination |
| Search news and papers | `aisafetyhot_search` | Existing content filtered by keyword, topic, category, and date |
| Explore research topics | `aisafetyhot_get_topics` | Topic names, identifiers, definitions, and related topics |
| Read an individual item | `aisafetyhot_get_content` | An item summary, the original source link, and any existing paper commentary |
| See trending events | `aisafetyhot_get_hot_topics` | The current event ranking, contributing sources, and related link counts |
| Follow an event | `aisafetyhot_get_story` | An event overview, a timeline of source reports, and discussions |
| Read daily, weekly, or monthly reports | `aisafetyhot_get_daily` | Published reports or a list of available report keys |

<a id="parameters"></a>

### Parameter quick reference

Tool names in this table omit the shared `aisafetyhot_` prefix. Your Agent can fill in the parameters based on your question. For all allowed values, defaults, and invocation details, see the tool descriptions provided by MCP.

| Parameter | Used by | Meaning and common values |
|---|---|---|
| `q` | `search` | Required search keyword, such as `prompt injection` |
| `mode` | `get_latest`, `search` | `all` searches all public updates; `selected` searches selected items only |
| `mode` | `get_latest` | `snapshot` / `changes` synchronizes the entire selected collection; category, topic, and date filters are not supported |
| `mode` | `get_daily` | `read` reads one report; `list` lists published report keys |
| `window` | `get_latest`, `search` | `24h` covers the past day; `7d` covers the past week; `all` includes historical content |
| `by` | `get_latest`, `search` | `timeline` sorts by the site timeline and filters date ranges by the time an item was added to the site; `published` sorts and filters by the original publication date |
| `category` | `get_latest`, `search` | Category codes: `attack` attacks, `defense` defenses, `alignment` alignment, `eval` evaluations, `incident` incidents, `industry` governance, `tip` tools, `opinion` opinions, `ai_news` AI updates |
| `topic` | `get_latest`, `search` | Topic identifier; use a slug returned by `get_topics` |
| `from` | `get_latest`, `search` | Start date or timestamp with a time zone; inclusive |
| `until` | `get_latest`, `search` | End date or timestamp with a time zone; exclusive |
| `limit` | `get_latest`, `search`, `get_daily`, `get_hot_topics` | Number of returned items: 1–50 per page for paginated tools, or the top 1–10 trending events; for reports, used only in `list` mode |
| `cursor` | `get_latest`, `search`, `get_story`, `get_daily` | Next-page identifier; use `page.nextCursor` for ordinary pagination; for reports, used only in `list` mode |
| `id` | `get_content` | Required news or paper ID, obtained from query results |
| `public_id` | `get_story` | Required event ID; use the `publicId` in the results |
| `depth` | `get_content`, `get_story` | `summary` returns a brief overview; `full` adds any existing body text or paper commentary, or event report summaries |
| `max_chars` | `get_content` | Character budget for body text, paper quick reads, and commentary: 1000–30000 |
| `report_limit` | `get_story` | Number of source reports per page: 1–50 |
| `period` | `get_daily` | `daily` for daily digests; `weekly` for weekly reports; `monthly` for monthly reports |
| `key` | `get_daily` | Report key in read mode: `YYYY-MM-DD`, `YYYY-Www`, or `YYYY-MM`; omit to read the latest published report |
| `date` | `get_daily` | Legacy daily digest date in read mode, in `YYYY-MM-DD` format; new calls can use `key` |
| `slug` | `get_topics` | Selects one topic; omit to list all configured topics |

Use `window="all"` to search historical content. Date-only `from` / `until` values are interpreted as midnight UTC. For cursor rules when synchronizing selected items, see the [full guide (Chinese)](docs/agent.md#续接精选变化).

<a id="examples"></a>

### What to try

Once connected, ask questions in natural language. MCP provides tool descriptions and parameter definitions, which your Agent uses to choose the calls.

| What to try | How to use it | Result |
|---|---|---|
| See new content | “List 3 selected items added to the site in the past 24 hours, with their sources and original links.” | [Titles, summaries, sources, and pagination (Chinese)](docs/mcp-examples.md#latest) |
| Research a topic | “Find papers about prompt injection, then open one and explain its findings.” | [Search results and existing paper commentary (Chinese)](docs/mcp-examples.md#topics) |
| Prepare a briefing | “Read the latest weekly report and list its themes and reading links.” | [Report key, coverage dates, and themes (Chinese)](docs/mcp-examples.md#reports) |

The linked example results were sampled on 2026-10-07 (Melbourne). Actual query results change as the website updates.

Keep both the site links and original source links in your answers. If `page.hasMore` is true, continue paginating; check `completeness` for missing or truncated content. The service reads existing public content. Paper commentary is secondary material, so verify key facts against the original source.

[Agent usage and parameter guide (Skill, Chinese)](skills/aisafetyhot/SKILL.md) · [Calls and example results (Chinese)](docs/mcp-examples.md) · [Reading scope and caveats (Chinese)](docs/agent.md#读取范围)

<a id="daily"></a>

## 🗞️ Daily AI safety digest

Read the latest digest and earlier editions through these regularly updated entries:

- [Latest digest (Chinese)](README.md#daily)
- [Daily digest archive (Chinese)](daily)
- [Daily reports on the website (Chinese)](https://aisafetyhot.com/daily)

> The daily digest is published each day at **08:00 Beijing time (UTC+8)**. The Hub checks for updates every 15 minutes. Each new edition replaces the digest section in the Chinese README; earlier editions remain in the [daily digest archive (Chinese)](daily).

<a id="papers"></a>

## 📚 Download the paper lists

Since 2026-09-24, papers added to the site and classified as AI safety research have been archived by date. Existing Chinese reading guides and paper quick reads are included in the lists, with further commentary added over time.

| What you want to do | File to use |
|---|---|
| Read paper titles, reading guides, and quick reads | [Markdown lists (Chinese)](papers) |
| Import into Zotero, EndNote, or a paper's bibliography | `papers/YYYY/YYYY-MM-DD.bib` |
| Give the data to an Agent, take notes, or use your own scripts | `papers/YYYY/YYYY-MM-DD.json` |

Paper quick reads cover the **problem, method, experiments and results, and limitations**, with the source identified for each paper. ★ marks a selected item. Attention scores are a reference signal for AI safety readers, not a measure of paper quality.

To download the LaTeX source files of arXiv papers, you can also use [arxiv2agent](https://github.com/wuyoscar/arxiv2agent).

<details>
<summary><strong>Browse recent digests and paper downloads</strong></summary>

- [Latest digests and paper downloads (Chinese)](README.md#papers)
- [2026 archive (Chinese)](archive/2026.md)
- [Paper lists (Chinese)](papers)

Paper lists are grouped by Beijing calendar day (00:00–24:00), using the paper's timestamp on the website timeline. Daily digests cover the window from 08:00 on the previous day to 08:00 on the current day, Beijing time (UTC+8). Because these day boundaries differ, a digest and paper list for the same date do not contain exactly the same set of items; a paper may appear in the digest for an adjacent date. Papers removed, corrected, or added on the website within the most recent 7 days are checked hourly, and any changes are synchronized to the list for the corresponding day.

[status.json](status.json) records each day's paper count and an ID digest, as well as the synchronization time limit (`slaMinutes`: the maximum number of minutes before papers on the website appear here).

</details>

## 🔎 More to explore on the website

[All updates](https://aisafetyhot.com/all) are continuously updated · [Trending events](https://aisafetyhot.com/hot) tracks event developments · [Visualization](https://aisafetyhot.com/all?view=graph) shows how sources, news, and papers connect to research areas · [Weekly reports](https://aisafetyhot.com/weekly) review the week · [Monthly reports](https://aisafetyhot.com/monthly) recap the month

**Subscribe in your own feed reader:** [Selected items RSS](https://aisafetyhot.com/feed.xml) · [All updates RSS](https://aisafetyhot.com/feed/all.xml) · [Daily digest RSS](https://aisafetyhot.com/feed/daily.xml)

## ☕ Support and feedback

The website and Hub are free. If they save you some time finding resources, you are welcome to [buy the author a coffee](https://buymeacoffee.com/wuyoscar) to help cover server and model API costs.

<details>
<summary>Support via WeChat</summary>

<img src="assets/wechat-pay.png" width="160" alt="WeChat payment QR code">

</details>

To report an error or request a correction or removal, visit the [message board (Chinese)](https://aisafetyhot.com/board) and select 「下架/更正」 (removal/correction).

---

AI Safety HOT is built on the open-source framework [AIHOT](https://github.com/KKKKhazix/AIHOT), with thanks to its original author. Reading guides are generated by models. Paper quick reads are prepared from paper PDFs using Gemini or from arXiv full text; each record identifies the specific source. Refer to the original sources for important numbers and conclusions.

Reading guides, quick reads, and daily digest text in this repository are licensed under [CC BY-NC 4.0](LICENSE). When republishing, credit AI Safety HOT and retain the source attribution; commercial use is not permitted. Copyright in the original articles and papers belongs to their respective authors and sources.
