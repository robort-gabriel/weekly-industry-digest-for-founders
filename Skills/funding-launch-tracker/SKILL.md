---
name: funding-launch-tracker
description: Track recent funding rounds and product launches for a given industry or niche. Use this as stage 2 of the Weekly Industry Digest for Founders pipeline, or standalone when the user asks to "who raised funding in [industry]", "what launched in [niche] this week", or "track funding rounds for [industry]".
metadata:
  author: robort.zo.computer
---

# Funding & Launch Tracker

## Overview

Given an industry or niche, this skill scans for recent funding rounds and new product/feature launches. It relies only on `web_search` (with `topic="news"`), `web_research` (categories `company` and `financial report`), and `x_search`. No paid funding-database, deal-tracking, or firmographic API is used.

## Inputs

- `niche` (required): the industry or niche, e.g. "AI coding assistants for solo founders".
- `topic_file` (optional, default `config/digest-topic.md`): read the `## Companies to Watch` section if present, to seed/scope the search instead of starting cold.
- `run_date` (optional, default today, `YYYY-MM-DD`).
- `time_range` (optional, default `week`): how far back to look.

## Steps

1. **Track funding rounds.** If `config/digest-topic.md` lists companies to watch, check each for recent funding news first. Then broaden with `web_search(topic="news", time_range=time_range)` and `web_research(category="financial report")` queries like `"<niche> funding round"`, `"<niche> raises"`, `"<niche> seed"`, `"<niche> Series A"`. Capture: company, round size/stage (if disclosed), lead investor (if disclosed), and source.
2. **Track product launches.** Run `web_search`/`x_search`/`web_research(category="company")` queries like `"<niche> launches"`, `"<niche> new feature"`, `"Product Hunt <niche>"` to surface notable product or feature launches this week.
3. **Write the output file** at `Content/Weekly-Industry-Digest/<niche-slug>/<run_date>/funding-launches.md` using this structure:

```markdown
# Funding & Launches: <niche> (<run_date>)

## Funding Rounds
- **<Company>** raised <amount or "undisclosed amount"> (<round stage, if known>)<, led by <investor>, if known>. Source: <URL>

## Product Launches
- **<Company/Product>**: <one-line description of what launched>. Source: <URL>

## Notes
<Anything unconfirmed (e.g. rumored round, unverified amount) or worth flagging to the digest-writer stage.>
```

4. Only report a funding amount or investor name if a source actually states it — write "undisclosed amount" rather than guessing a figure. Never fabricate a company, round, or launch that wasn't actually returned by a search.

## Output

`Content/Weekly-Industry-Digest/<niche-slug>/<run_date>/funding-launches.md`: consumed by `digest-writer` in stage 3.
