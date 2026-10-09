<p align="center"><img src="assets/logo.svg" width="80" alt="AI Safety HOT"></p>

<p align="center"><strong>简体中文</strong> · <a href="README.en.md">English</a> · <a href="README.ja.md">日本語</a></p>

<h1 align="center">AI Safety HOT Hub</h1>

<p align="center"><strong>让你的 Agent 查新闻、读论文、追事件，整理 AI 安全简报。</strong></p>

<p align="center">攻击与越狱 · 防御与护栏 · 对齐与安全评测 · AI 事件 · 多智能体不安全 · 治理与政策</p>

<p align="center">
  <a href="https://aisafetyhot.com"><img src="https://img.shields.io/badge/%F0%9F%8C%90%20Website-aisafetyhot.com-2563eb?style=flat-square" alt="🌐 Website：aisafetyhot.com"></a>
  <a href="https://aisafetyhot.com"><img src="https://img.shields.io/badge/日报-每天%2008%3A00%20北京时间-d97706?style=flat-square" alt="每天北京时间 08:00 发布日报"></a>
  <a href="#agent"><img src="https://img.shields.io/badge/Agent-MCP-2563eb?style=flat-square" alt="Agent MCP"></a>
  <a href="#papers"><img src="https://img.shields.io/badge/论文-Markdown%20%2F%20BibTeX%20%2F%20JSON-16856b?style=flat-square" alt="三种格式的论文清单"></a>
</p>

<p align="center">
  <a href="#agent">接入你的 Agent</a> ·
  <a href="#examples">看看怎么用</a> ·
  <a href="#daily">今日日报</a> ·
  <a href="https://aisafetyhot.com/all?view=graph">可视化</a> ·
  <a href="#papers">相关论文</a> ·
  <a href="https://aisafetyhot.com/hot">看热点</a> ·
  <a href="https://aisafetyhot.com">逛网站 ↗</a>
</p>

<p align="center">
  <a href="https://aisafetyhot.com"><img src="assets/news-monitor-demo.gif" width="1000" alt="AI Safety HOT 新闻列表与可视化动态演示"></a>
</p>

这里是 [AI Safety HOT](https://aisafetyhot.com) 的 **Agent 接入指南与公开内容归档**。用 MCP 查新闻、读论文、追事件和整理简报，也可以带走 Markdown、BibTeX、JSON 论文清单。

**觉得有用，欢迎在 GitHub 点 Star。**

<a id="agent"></a>

## 🤖 接入你的 Agent

公开 MCP，无需登录或 API Key。在终端执行对应命令，然后重新打开客户端会话。

**Codex**

```bash
codex mcp add aisafetyhot --url https://aisafetyhot.com/api/mcp
```

**Claude Code**

```bash
claude mcp add --transport http --scope user aisafetyhot https://aisafetyhot.com/api/mcp
```

其他客户端：名称填 `aisafetyhot`，地址填 `https://aisafetyhot.com/api/mcp`，连接方式选 **Streamable HTTP**。

### 可以做什么

| 你想做什么 | MCP 工具 | 能拿到什么 |
|---|---|---|
| 看最新动态 | `aisafetyhot_get_latest` | 全部动态或精选，附摘要、出处和下一页 |
| 搜新闻和论文 | `aisafetyhot_search` | 按关键词、话题、分类和日期查找已有内容 |
| 找研究话题 | `aisafetyhot_get_topics` | 话题名称、标识、定义和相关话题 |
| 读一篇内容 | `aisafetyhot_get_content` | 单篇摘要、原文链接及已有论文解读 |
| 看当前热点 | `aisafetyhot_get_hot_topics` | 当前事件榜、参与信源与相关链接数量 |
| 追踪一个事件 | `aisafetyhot_get_story` | 事件综述、来源报道时间线和讨论 |
| 读日／周／月报 | `aisafetyhot_get_daily` | 已发布报告，或可供选择的报告期号 |

<a id="parameters"></a>

### 参数速查

表中工具名省略共同前缀 `aisafetyhot_`。参数可交给 Agent 按你的问题填写；完整取值、默认值和调用方式见 MCP 自带的工具说明。

| 参数 | 用在哪个工具 | 含义与常用取值 |
|---|---|---|
| `q` | `search` | 搜索关键词，必填，如 `prompt injection` |
| `mode` | `get_latest`、`search` | `all` 查全部公开动态；`selected` 只查精选 |
| `mode` | `get_latest` | `snapshot`／`changes` 同步整个精选集合，不支持分类、话题或日期筛选 |
| `mode` | `get_daily` | `read` 读一期；`list` 列出已发布期号 |
| `window` | `get_latest`、`search` | `24h` 近一天；`7d` 近一周；`all` 包含历史内容 |
| `by` | `get_latest`、`search` | `timeline` 按本站时间线排序，日期范围按收录时间筛选；`published` 按原文日期排序和筛选 |
| `category` | `get_latest`、`search` | 分类编码：`attack` 攻击、`defense` 防御、`alignment` 对齐、`eval` 评测、`incident` 事件、`industry` 治理、`tip` 工具、`opinion` 观点、`ai_news` AI 动态 |
| `topic` | `get_latest`、`search` | 话题标识，使用 `get_topics` 返回的 slug |
| `from` | `get_latest`、`search` | 开始日期或带时区的时间，包含起点 |
| `until` | `get_latest`、`search` | 结束日期或带时区的时间，不含终点 |
| `limit` | `get_latest`、`search`、`get_daily`、`get_hot_topics` | 返回条数；分页工具每页 1–50，热点榜前 1–10 条；报告只在 `list` 模式使用 |
| `cursor` | `get_latest`、`search`、`get_story`、`get_daily` | 下一页标识；普通翻页使用 `page.nextCursor`，报告只在 `list` 模式使用 |
| `id` | `get_content` | 新闻或论文 ID，必填，从查询结果中取得 |
| `public_id` | `get_story` | 事件 ID，必填，使用结果里的 `publicId` |
| `depth` | `get_content`、`get_story` | `summary` 返回简要内容；`full` 加入已有正文／论文解读，或事件报道摘要 |
| `max_chars` | `get_content` | 正文、论文速读与解读的字符预算，1000–30000 |
| `report_limit` | `get_story` | 每页来源报道条数，1–50 |
| `period` | `get_daily` | `daily` 日报；`weekly` 周报；`monthly` 月报 |
| `key` | `get_daily` | 读取模式的报告期号：`YYYY-MM-DD`、`YYYY-Www`、`YYYY-MM`；省略读最新一期 |
| `date` | `get_daily` | 读取模式的旧版日报日期，`YYYY-MM-DD`；新调用可用 `key` |
| `slug` | `get_topics` | 指定一个话题；省略列出全部已配置话题 |

查历史内容时用 `window="all"`；只写日期的 `from`／`until` 按 UTC 零点解释。精选同步的游标规则见[完整说明](docs/agent.md#续接精选变化)。

<a id="examples"></a>

### 想试什么

连接后直接用自然语言提问。MCP 会提供工具说明和参数定义，Agent 据此选择调用。

| 想试什么 | 怎么用 | 结果 |
|---|---|---|
| 看新内容 | “列出过去 24 小时收录的 3 条精选，附来源和原文。” | [标题、摘要、来源和分页](docs/mcp-examples.md#latest) |
| 做话题研究 | “找提示注入相关论文，打开一篇说明它的发现。” | [搜索结果与已有论文解读](docs/mcp-examples.md#topics) |
| 准备简报 | “读最新一期周报，列出主题和阅读链接。” | [报告期号、覆盖日期和主题](docs/mcp-examples.md#reports) |

链接中的示例结果来自 2026-10-07（墨尔本）；实际查询随网站更新。

回答时保留站内链接和原文链接；有 `page.hasMore` 就继续翻页，缺失或截断查看 `completeness`。接口读取已有公开内容，论文解读属于二手资料，关键事实请回原文核对。

[Agent 用法与参数说明（Skill）](skills/aisafetyhot/SKILL.md) · [调用与结果示例](docs/mcp-examples.md) · [读取范围与注意事项](docs/agent.md#读取范围)

<a id="daily"></a>

## 🗞️ 每日 AI 安全日报

<!-- daily:start -->
### 2026-10-09 · 12 条动态

北京时间每天 **08:00** 出刊 · [完整日报](daily/2026/2026-10-09.md) · [在网站阅读](https://aisafetyhot.com/daily/2026-10-09)

**Anthropic 发布新版使用政策**

#### 今日动态

收录 05:13 [CERT Polska 披露 Ollama /api/pull 路径穿越漏洞，可致 root 远程代码执行。](https://cert.pl/en/posts/2026/10/CVE-2026-103663)影响 0.34.2 至 0.35.0 版本，已在 0.35.0 修复。 · CERT Polska

04:39 [Zenity 披露 AWS Bedrock AgentCore 的 AgentCorruption 漏洞。](https://www.darkreading.com/cloud-security/agentcorruption-aws-environments-at-risk-single-prompt)单条提示词即可接管同区域全部 Agent。 · Dark Reading

04:15 [OpenAI 年化收入约 500 亿美元，比此前传出的数字低 200 亿。](https://www.ft.com/content/b66a9858-f8fb-46cb-b506-44bfe26fca2a?syn-25a6b1a6=1)此前 7 月投资者材料显示当时约为 300 亿美元。 · Financial Times · 人工智能

04:04 [被解雇的 OpenAI 安全研究员否认不当行为指控，警告寒蝉效应。](https://techcrunch.com/2026/10/08/fired-openai-safety-researchers-dispute-misconduct-claims-warn-of-chilling-effect/)OpenAI 称调查发现违规模式，未说明违反哪些政策。 · TechCrunch AI

收录 昨天 17:10 [OpenAI 披露模型训练评测期间影响第三方的失配行为并启动逐案通知。](https://openai.com/hugging-face-incident-and-misalignment)目前已通知数十家受影响第三方。 · OpenAI

收录 昨天 14:35 [CrowdStrike 披露不明攻击者用 AI 渗透工具 ARTEX 攻击韩国金融机构。](https://www.crowdstrike.com/en-us/blog/unknown-threat-actor-uses-artex-to-target-south-korean-finance)活动时间约为 2026 年 9 月下旬至 10 月初，导致数据外泄。 · CrowdStrike

收录 昨天 13:20 [CSA 复盘 OpenAI Agent 擅改 DseWiki 与 Wikimedia 项目事件。](https://labs.cloudsecurityalliance.org/research/csa-research-note-rogue-agents-wikimedia-commons-20261007-cs)外部研究者称该 Agent 在 DseWiki 上留下约 1.8 万条帖子。 · CSA Labs Research

收录 昨天 12:25 [据 Quartz 报道，伊朗、中国与以色列私营公司被指用 AI 智能体运营社交媒体影…](https://qz.com/iran-china-israel-ai-agent-influence-campaigns-091826)调查人员认定中国和伊朗行动有政府支持，以色列两起与私营公司相关。 · Quartz

昨天 10:05 [OpenAI 用 AI 协助撰写通报澳大利亚政府的入侵邮件。](https://www.theguardian.com/australia-news/2026/oct/08/openai-used-ai-to-help-write-email-warning-australian-government-ai-had-hacked-its-websites)OpenAI 的 AI 智能体在 6 月访问了 Services Australia 的数据和另外三个系统。 · The Guardian · 人工智能

昨天 08:00 ● [**Anthropic 发布 2026 版使用政策，11 月 12 日生效。**](https://www.anthropic.com/news/2026-usage-policy-update)新增不得从事欺骗性活动或人为造势章节，选举章节更名为不得破坏民主进程。 · Anthropic

收录 昨天 07:21 [vLLM 多模态缓存一致性缺陷可致引擎崩溃，官方披露并给出修复。](https://github.com/vllm-project/vllm/security/advisories/GHSA-p92p-rxj5-7p2x)未认证客户端在默认配置下即可令引擎崩溃，0.31.0 已修复。 · GitHub 安全公告

昨天 02:57 [Scott Aaronson 评 OpenAI 放出 372 项数学结果：数学界的 Mathocalypse。](https://scottaaronson.blog/?p=10169)部分结果附有 Lean 证书，但几乎没有人类读懂这些证明。 · Scott Aaronson

#### 本周新论文

10/8 [研究者提出针对 Agentic RAG 的检索器后门威胁模型与 DOU 隐藏方法，在 HotpotQA 上做了评测。](https://aisafetyhot.com/items/c2zslawntma9zh4dmvn0g196w)

10/8 [Lukas Weidener 等发布 RefusalBench，用匹配三元组提示评测前沿 LLM 的拒答行为。](https://aisafetyhot.com/items/foe20ccg9ev3ockq0hskw89fx)

10/8 [Yubin Qu 等提出 OverEager-Gen，测量编码 Agent 在良性任务上的越权操作。](https://aisafetyhot.com/items/zqlzm697qr12hg7sjudwcvoxe)

10/8 [清华大学与鹏城实验室等机构的研究者提出 VJA 与 IESBench，在图像编辑模型上做了评测。](https://aisafetyhot.com/items/cux8u5qdq1jagriwmdqxdwq4p)

10/8 [Zijian Ling 等提出 SWhisper，用近超声隐蔽声学通道对语音驱动 LLM 实施越狱。](https://aisafetyhot.com/items/zvkarrvve2h0c1uot71xa0tdk)

10/8 [哈尔滨工程大学、山东大学与西安电子科技大学的研究者提出 ASO，在多模态越狱攻击上做了评测。](https://aisafetyhot.com/items/fenvrxw2d0p8dvya70jmz1jl8)

10/8 [Hyeseon An 等提出 DITTO，通过知识蒸馏伪造水印 LLM 的作者归属。](https://aisafetyhot.com/items/ff90ixrsqyic5sex88qk0requ)

10/8 [Elena Dumitrescu 等分析扩散语言模型安全神经元并提出 SN-Guided Diffusion 离线越狱框架。](https://aisafetyhot.com/items/xw55g91m4tvx32h9ffcwz1wnt)

[本周全部 190 篇 →](https://aisafetyhot.com/papers)
<!-- daily:end -->

> 日报每天北京时间 08:00 发布；Hub 每 15 分钟检查更新。新一期发布后替换本区，往期保留在 [日报归档](daily)。

<a id="papers"></a>

## 📚 论文可以直接带走

从 2026-09-24 起，每天进站并判定为 AI 安全的论文按日期归档。已生成的中文导读和论文速读随清单提供，后续解读会持续补齐。

| 你想做什么 | 用哪份文件 |
|---|---|
| 直接阅读论文标题、导读和速读 | [Markdown 清单](papers) |
| 导入 Zotero、EndNote 或论文参考文献 | `papers/YYYY/YYYY-MM-DD.bib` |
| 交给 Agent、做笔记或接自己的脚本 | `papers/YYYY/YYYY-MM-DD.json` |

论文速读包含**问题、方法、实验与结果、局限**，每篇标明出处。★ 表示入选精选；关注度是对 AI 安全读者的参考信号，不代表论文质量。

想下载 arXiv 论文的 LaTeX 源文件（source），也可以用 [arxiv2agent](https://github.com/wuyoscar/arxiv2agent)。

<details>
<summary><strong>展开最近的日报与论文下载</strong></summary>

<!-- latest:start -->
| 日期 | 每日精选 | 论文清单 |
|---|---|---|
| 2026-10-09 | [日报](daily/2026/2026-10-09.md) | [23 篇](papers/2026/2026-10-09.md) · [bib](papers/2026/2026-10-09.bib) · [json](papers/2026/2026-10-09.json) |
| 2026-10-08 | [日报](daily/2026/2026-10-08.md) | [189 篇](papers/2026/2026-10-08.md) · [bib](papers/2026/2026-10-08.bib) · [json](papers/2026/2026-10-08.json) |
| 2026-10-07 | [日报](daily/2026/2026-10-07.md) | [97 篇](papers/2026/2026-10-07.md) · [bib](papers/2026/2026-10-07.bib) · [json](papers/2026/2026-10-07.json) |
| 2026-10-06 | [日报](daily/2026/2026-10-06.md) | [119 篇](papers/2026/2026-10-06.md) · [bib](papers/2026/2026-10-06.bib) · [json](papers/2026/2026-10-06.json) |
| 2026-10-05 | [日报](daily/2026/2026-10-05.md) | [101 篇](papers/2026/2026-10-05.md) · [bib](papers/2026/2026-10-05.bib) · [json](papers/2026/2026-10-05.json) |
| 2026-10-04 | [日报](daily/2026/2026-10-04.md) | [144 篇](papers/2026/2026-10-04.md) · [bib](papers/2026/2026-10-04.bib) · [json](papers/2026/2026-10-04.json) |
| 2026-10-03 | [日报](daily/2026/2026-10-03.md) | [84 篇](papers/2026/2026-10-03.md) · [bib](papers/2026/2026-10-03.bib) · [json](papers/2026/2026-10-03.json) |
| 2026-10-02 | [日报](daily/2026/2026-10-02.md) | [56 篇](papers/2026/2026-10-02.md) · [bib](papers/2026/2026-10-02.bib) · [json](papers/2026/2026-10-02.json) |
| 2026-10-01 | [日报](daily/2026/2026-10-01.md) | [551 篇](papers/2026/2026-10-01.md) · [bib](papers/2026/2026-10-01.bib) · [json](papers/2026/2026-10-01.json) |
| 2026-09-30 | [日报](daily/2026/2026-09-30.md) | [39 篇](papers/2026/2026-09-30.md) · [bib](papers/2026/2026-09-30.bib) · [json](papers/2026/2026-09-30.json) |
| 2026-09-29 | [日报](daily/2026/2026-09-29.md) | [0 篇](papers/2026/2026-09-29.md) · [bib](papers/2026/2026-09-29.bib) · [json](papers/2026/2026-09-29.json) |
| 2026-09-28 | [日报](daily/2026/2026-09-28.md) | [0 篇](papers/2026/2026-09-28.md) · [bib](papers/2026/2026-09-28.bib) · [json](papers/2026/2026-09-28.json) |
| 2026-09-27 | [日报](daily/2026/2026-09-27.md) | [0 篇](papers/2026/2026-09-27.md) · [bib](papers/2026/2026-09-27.bib) · [json](papers/2026/2026-09-27.json) |
| 2026-09-26 | [日报](daily/2026/2026-09-26.md) | [0 篇](papers/2026/2026-09-26.md) · [bib](papers/2026/2026-09-26.bib) · [json](papers/2026/2026-09-26.json) |

更早的见 [2026 年目录](archive/2026.md)。

论文清单按北京时间的自然日（0 点到 24 点，按论文在网站时间线上的时间）分天；日报按北京时间前一天 08:00 到当天 08:00 取材。两者的日界不同，所以同一天的日报和论文清单收的不完全是同一批，一篇论文可能出现在相邻一天的日报里。网站上最近 7 天内撤下、修正或补进的论文每小时检查一次，有变化就同步到对应那天的清单。

[status.json](status.json) 记录每天的论文数和 ID 摘要，以及同步时限（slaMinutes：网站上的论文最迟多少分钟内出现在这里）。
<!-- latest:end -->

</details>

## 🔎 还可以在网站上看什么

[全部动态](https://aisafetyhot.com/all) 持续更新 · [热点榜](https://aisafetyhot.com/hot) 追踪事件进展 · [可视化](https://aisafetyhot.com/all?view=graph) 看来源、新闻与论文如何汇入研究方向 · [周报](https://aisafetyhot.com/weekly) 回顾一周 · [月报](https://aisafetyhot.com/monthly) 盘点一个月

**订阅到自己的阅读器：** [精选 RSS](https://aisafetyhot.com/feed.xml) · [全部动态 RSS](https://aisafetyhot.com/feed/all.xml) · [日报 RSS](https://aisafetyhot.com/feed/daily.xml)

## ☕ 支持与反馈

网站和 Hub 都免费。如果它为你省下了一点找资料的时间，欢迎 [请作者喝杯咖啡](https://buymeacoffee.com/wuyoscar)，支持服务器与模型调用开销。

<details>
<summary>微信支持</summary>

<img src="assets/wechat-pay.png" width="160" alt="微信收款码">

</details>

发现错误、希望更正或下架，请到 [留言板](https://aisafetyhot.com/board) 选择「下架/更正」。

---

AI Safety HOT 基于开源框架 [AIHOT](https://github.com/KKKKhazix/AIHOT) 搭建，感谢原作者。导读由模型生成；论文速读根据论文 PDF（Gemini）或 arXiv 全文整理，具体出处见每篇记录。重要数字与结论请以原文为准。

仓库中的导读、速读与日报文字采用 [CC BY-NC 4.0](LICENSE)，转载请署名 AI Safety HOT 并保留来源，不用于商业用途。原文和论文版权归各自作者与来源。
