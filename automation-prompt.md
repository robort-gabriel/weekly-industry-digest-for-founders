# Weekly Industry Digest for Founders: Automation Prompt

## Objective

Deliver a short, LinkedIn-ready weekly digest for a given industry or niche: scan this week's notable news, track funding rounds and product launches, and write one reshare/comment-ready post, by running the three project-local skills in sequence: `industry-news-scanner` -> `funding-launch-tracker` -> `digest-writer`.

## Inputs

- `niche` (required): the industry or niche to cover, e.g. "AI coding assistants for solo founders". If not given, read `config/digest-topic.md`'s `## Industry / Niche` section.
- `topic_file` (optional, default `config/digest-topic.md`): companies to watch and focus areas to seed/scope the scan.
- `run_date` (optional, default today, `YYYY-MM-DD`).
- `notify` (optional, default `none`): `none` | `email`. If `email`, email the finished digest to the user via `send_email_to_user` after saving it. Any other delivery channel (Slack, SMS, etc.) requires the user to explicitly request it in the same run.

## Steps

1. Run the `industry-news-scanner` skill (`Skills/industry-news-scanner/SKILL.md`) for `niche`. It scans this week's notable news and social discourse using only `web_search` and `x_search`. Never a paid news-monitoring API. Output: `Content/Weekly-Industry-Digest/<niche-slug>/<run_date>/news-scan.md`.
2. Run the `funding-launch-tracker` skill (`Skills/funding-launch-tracker/SKILL.md`) for `niche`. It tracks recent funding rounds and product launches using only `web_search`, `web_research`, and `x_search`. Never a paid funding-database or deal-tracking API. Output: `Content/Weekly-Industry-Digest/<niche-slug>/<run_date>/funding-launches.md`.
3. Run the `digest-writer` skill (`Skills/digest-writer/SKILL.md`) on this run's `news-scan.md` and `funding-launches.md`. It synthesizes both into one short, LinkedIn-ready digest post with a hook, 3-6 traceable highlight bullets, and a closing discussion prompt. Output: `Content/Weekly-Industry-Digest/<niche-slug>/<run_date>.md`.
4. Do not fabricate a news item, funding round, launch, or highlight at any stage. Only report what was actually observed or retrieved from a real source, with a source URL for every factual claim. Never use em dashes in the digest copy.
5. Never post the digest to LinkedIn or any other platform automatically. This automation only ever produces a draft post for the user to review, copy, and publish themselves.
6. If `notify` is `email`, email the digest post (or a clear summary + file path) to the user via `send_email_to_user`. If `notify` is `none`, just report the file path. Do not send anything else.

## Outputs

- `Content/Weekly-Industry-Digest/<niche-slug>/<run_date>/news-scan.md`
- `Content/Weekly-Industry-Digest/<niche-slug>/<run_date>/funding-launches.md`
- `Content/Weekly-Industry-Digest/<niche-slug>/<run_date>.md`: the LinkedIn-ready post the user reads and publishes

Plus a short chat/report summary: niche covered, number of notable news items, number of funding rounds and launches tracked, the digest's file path, and a reminder that publishing to LinkedIn is a separate manual step.

## Error handling

- If no `niche` is given and `config/digest-topic.md` has no real entry (only the placeholder example), stop and ask the user for a niche rather than guessing one.
- If a news or funding source page fails to load, skip that source (not the whole run) and note it rather than fabricating content for it.
- If `digest-writer` can't find `news-scan.md` or `funding-launches.md` for the run date, stop and report which stage's output is missing rather than guessing its contents.
- Never call a paid or external API at any stage, even if a source is hard to parse without one. Report the limitation instead.
