# Weekly Industry Digest for Founders: Installation Prompt (claude.ai)

Paste everything below the line into a **new claude.ai chat** and send it. It's self-contained, the AI reading it has no memory of how this project was built, so it spells out every step. Swap the repo URL first if you're installing from a fork.

This path is for claude.ai (Cowork), not Claude Code. It requires a plan with Skills and code execution enabled (Pro, Max, Team, or Enterprise). Before sending this prompt, go to **Settings → Capabilities** and turn on **Code execution**, **File creation**, and **Web search**, they're required for the steps below to work.

---

Help me install the "Weekly Industry Digest for Founders" automation from this public GitHub repo:

`https://github.com/robort-gabriel/weekly-industry-digest-for-founders`

Do the following, in order. Steps marked **(confirm)** must not proceed until I explicitly approve, don't treat silence or a prior approval as blanket permission.

### 1. Fetch the three skills

- Using web search / fetch, retrieve the raw contents of these three files from the repo:
  ```
  Skills/industry-news-scanner/SKILL.md
  Skills/funding-launch-tracker/SKILL.md
  Skills/digest-writer/SKILL.md
  Skills/digest-writer/references/output-template.md
  ```
- Confirm each SKILL.md file has valid frontmatter (`name` matching its skill folder, non-empty `description`). If any file can't be fetched or looks malformed, stop and tell me which one and why, rather than guessing its contents.

### 2. Package each skill as its own zip

- Using code execution, create three separate folders (`industry-news-scanner/`, `funding-launch-tracker/`, `digest-writer/`), each containing that skill's `SKILL.md` (and, for `digest-writer`, its `references/output-template.md` too), then zip each folder individually.
- Skills must be uploaded to claude.ai as one zip per skill, never the whole set as a single zip. Give me all three `.zip` files to download.
- Tell me plainly: I still need to go to **Settings → Capabilities → Skills** myself and upload each zip, then toggle it on, that part can't be done from inside a chat.

### 3. Fetch the config and instruction files

- Fetch the raw contents of:
  ```
  config/digest-topic.md
  persona.md
  automation-prompt.md
  starter-prompts.md
  ```
- Turn `config/digest-topic.md` and `persona.md` into downloadable files exactly as fetched (I'll upload these as Project knowledge files myself).
- **(confirm)** Ask me whether I want to fill in a real niche and companies-to-watch in `digest-topic.md` now, or leave the placeholder example and just use this ad hoc, naming a niche each time in chat. If I give you a niche, replace the placeholder and regenerate the downloadable file.

### 4. Draft the Project custom instructions

- Using `automation-prompt.md`'s content (objective + steps) and `persona.md`'s prompt text, draft a single combined custom-instructions text suitable for pasting into a claude.ai Project's custom instructions field. It should describe: the three-stage pipeline (`industry-news-scanner` → `funding-launch-tracker` → `digest-writer`), that every stage only uses public web search (never a paid news-monitoring, funding-database, or firmographic API), that no news item/funding round/launch/highlight may be fabricated, and that the digest is never posted to LinkedIn or anywhere else automatically, it's always a draft for me to copy and post myself.
- Show me the drafted text before I use it. Don't shorten or drop the no-fabrication or no-auto-post rules, they're load-bearing.

### 5. Guide me through creating the Project

- Tell me the exact manual steps: create a new Project named "Weekly Industry Digest for Founders", paste in the custom instructions from step 4, and upload `config/digest-topic.md` and `persona.md` (from step 3) as Project knowledge files.
- Explain that chats inside this Project will then have the pipeline logic, niche/topic config, and skills in scope automatically, and that file creation inside a Project chat is chat-scoped, not a persistent folder tree, so I'll need to download the digest post I want to keep from each run.

### 6. Offer a scheduled run

- **(confirm)** Ask me whether I want recurring runs via Claude Cowork's Scheduled Tasks, and if so, what frequency (weekly is the natural default given the project's name, but confirm rather than assume) and whether I want the digest emailed/delivered as a summary or just left in the chat as a downloadable file.
- Explain plainly that Scheduled Tasks run in the cloud on the schedule I set, using the same instructions from `automation-prompt.md`, and that no matter the schedule, the digest is never posted to LinkedIn or anywhere else automatically, every post still needs my manual review, copy, and publish step.
- Since Scheduled Tasks are set up through claude.ai's own scheduling UI rather than from inside a chat, give me the exact task description text to paste in when I create it there.

### 7. Report back

- Confirm: which files were fetched successfully, the three zip files are ready for me to download and upload manually, whether a real niche/topic was filled in (and what's in it), the drafted Project custom instructions, and whether I want to set up a Scheduled Task (and its frequency) or leave it for later.
- Give me one ready-to-run example prompt from `starter-prompts.md` so I can try the pipeline ad hoc once the Project is set up.

Throughout all of this, never fabricate a news item, funding round, product launch, or highlight, never call a paid news-monitoring or funding-database API (only public web search), and never post the digest to LinkedIn or any other platform, this project only ever produces a draft post for me to review, copy, and publish myself.
