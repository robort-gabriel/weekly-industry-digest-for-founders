---
name: digest-writer
description: Synthesize a news scan and a funding/launch tracker file into one short, LinkedIn-ready weekly industry digest for founders. Use this as stage 3 (final) of the Weekly Industry Digest for Founders pipeline, after industry-news-scanner and funding-launch-tracker have produced their output files, or standalone when the user asks to "turn this research into a LinkedIn post" or "write this week's digest".
metadata:
  author: robort.zo.computer
---

# Digest Writer

## Overview

Takes `news-scan.md` (notable news) and `funding-launches.md` (funding rounds + launches) produced for the same niche and run date, and synthesizes them into one short digest post: a hook, 3-6 highlight bullets each traceable to a specific finding, and a closing line built to invite resharing or comments. See `references/output-template.md` for the exact post structure. Never uses em dashes in the written copy.

## Inputs

- `niche` (required): the industry or niche this run covers.
- `news_scan_file` (required): path to this run's `news-scan.md` from `industry-news-scanner`.
- `funding_launches_file` (required): path to this run's `funding-launches.md` from `funding-launch-tracker`.
- `run_date` (optional, default today, `YYYY-MM-DD`).

## Steps

1. Read both input files in full. If either is missing, stop and report which stage's output is missing rather than guessing its contents.
2. Write a **hook**: one punchy opening line that frames why this week mattered for founders in `<niche>` (not a generic "here's your weekly digest" line).
3. Draft **3-6 highlight bullets**, each pulling from the funding rounds, launches, or notable news in the two input files. Each bullet should read like something a founder would want to reshare or comment on: state the fact plainly, then one clause on why it matters for someone building in this niche. Every bullet must cite the specific finding it's derived from, don't invent a highlight that isn't traceable to something in the two input files.
4. Prioritize funding rounds and launches over generic news when picking the 3-6 highlights, since those are the highest-signal items for a founder audience, but include a top news item if it's genuinely more significant than the week's funding/launch activity.
5. Write a closing line: a short discussion question or opinion prompt related to the week's biggest highlight, designed to invite comments (not a generic "what do you think?").
6. Fill in `references/output-template.md` and write the result to `Content/Weekly-Industry-Digest/<niche-slug>/<run_date>.md`.
7. Never fabricate a highlight, statistic, or claim that isn't backed by something in `news_scan_file` or `funding_launches_file`. If the inputs are thin, write fewer, stronger highlights rather than padding with generic commentary. Never use em dashes in the digest copy, use commas or periods instead.

## Output

`Content/Weekly-Industry-Digest/<niche-slug>/<run_date>.md`: the finished LinkedIn-ready digest post the user reads, copies, and posts themselves.
