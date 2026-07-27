---
name: industry-news-scanner
description: Scan recent news and social discourse for a given industry or niche and summarize what happened this week. Use this as stage 1 of the Weekly Industry Digest for Founders pipeline, or standalone when the user asks to "scan news for [industry]", "what happened in [niche] this week", or "summarize industry news for [industry]".
metadata:
  author: robort.zo.computer
---

# Industry News Scanner

## Overview

Given an industry or niche, this skill scans recent news and social discourse for the current week and produces a plain-language news summary with source links. It relies only on `web_search` (with `topic="news"`) and `x_search`. No paid news-monitoring or media-intelligence API is used.

## Inputs

- `niche` (required): the industry or niche, e.g. "AI coding assistants for solo founders".
- `topic_file` (optional, default `config/digest-topic.md`): read the `## Focus Areas` section if present, to narrow which sub-topics to prioritize.
- `run_date` (optional, default today, `YYYY-MM-DD`).
- `time_range` (optional, default `week`): how far back to look for news.

## Steps

1. **Scan recent news.** Run `web_search(topic="news", time_range=time_range)` with 2-3 differently-worded queries about `<niche>` (and each focus area, if given) to get broad coverage.
2. **Scan social discourse.** Run `x_search` for `<niche>` to capture founder/practitioner commentary and reactions that haven't hit mainstream news coverage yet.
3. **Pick the items worth a founder's attention.** Filter down to 5-10 items that a founder in this niche would actually want to know about this week: policy/regulatory shifts, notable partnerships, notable hires, platform changes, or any story generating real discussion. Skip generic churn (routine minor updates, recycled press releases).
4. **Write the output file** at `Content/Weekly-Industry-Digest/<niche-slug>/<run_date>/news-scan.md` using this structure:

```markdown
# News Scan: <niche> (<run_date>)

## This Week's Notable News
- <Plain-language one-line recap of the item>, Source: <URL>
- <Plain-language one-line recap of the item>, Source: <URL>

## Notes
<Anything ambiguous, single-sourced, or worth flagging to the digest-writer stage.>
```

5. Every item must carry a source URL. Never fabricate a news item, a quote, or a statistic that wasn't actually returned by a search.

## Output

`Content/Weekly-Industry-Digest/<niche-slug>/<run_date>/news-scan.md`: consumed by `digest-writer` in stage 3.
