---
name: aisafety-related-work
description: Draft a related-work section for an AI safety paper or project from the AI Safety HOT paper library, grouped by line of work, with BibTeX. Use when the user gives a paper title, abstract or idea and asks for related work, prior work, or citations.
---

# Related work from AI Safety HOT

1. Read the user's title/abstract. List its 2–4 core ideas (threat model, method, setting, evaluation).
2. Retrieve papers using the `aisafety-paper-scout` [retrieval and fallback rules](../aisafety-paper-scout/SKILL.md), including source outcome tracking, relevance from `title`/`titleZh`/`line`/`topics`, bounded published daily-list fallback, separate publication and edition date constraints, ID deduplication, metadata/source preservation, and citation limits. Apply these rules to the core ideas together: one latest published daily list by default, or at most 3 matching editions for an explicit edition-date request; do not create a separate retrieval policy here.
3. Group the kept papers into 2–4 lines of work. For each group write one paragraph: what the line does, the representative papers (cite as [n]), and how the user's work differs — state the difference only from what the user told you.
4. End with the numbered reference list and BibTeX where the metadata supports it, following `aisafety-paper-scout`'s citation rules. No invented authors, venues or results; say "per the paper's one-line summary" where you only have `line`. A title/link-only pick is a discovery lead, not evidence for a synthesized finding or a fabricated citation.
5. Report source outcomes and actual daily-list coverage as in `aisafety-paper-scout`, and tell the user which ideas had few matches so they can search elsewhere. Limit any no-match claim to the checked sources/dates.
