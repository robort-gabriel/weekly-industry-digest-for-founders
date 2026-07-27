<h1 align="center">Weekly Industry Digest for Founders</h1>

<p align="center">
  An AI agent automation workflow that scans an industry or niche for this week's notable news, funding rounds, and product launches.<br/>
  Get one short, reshare-ready LinkedIn digest post, built on Zo Computer and compatible with Claude AI.
</p>

<table align="center">
  <tr>
    <td align="center"><img src="https://zo.pub/robort/weekly-industry-digest-for-founders/zo-logo.png" alt="Zo Computer" width="64" /></td>
    <td align="center"><img src="https://zo.pub/robort/weekly-industry-digest-for-founders/claude-logo.png" alt="Claude AI" width="64" /></td>
  </tr>
</table>

<p align="center">
  <img src="https://zo.pub/robort/weekly-industry-digest-for-founders/pipeline-diagram.svg" alt="Scan to Track to Digest pipeline" width="560" />
</p>

<p align="center">
  <img alt="workflow: 3-stage pipeline" src="https://img.shields.io/badge/workflow-3--stage%20pipeline-38bdf8" /> <img alt="cadence: weekly" src="https://img.shields.io/badge/cadence-weekly-16a34a" />
</p>
<p align="center">
  <img alt="output: linkedin digest" src="https://img.shields.io/badge/output-linkedin%20digest-fb7185" /> <img alt="storage: Content/" src="https://img.shields.io/badge/storage-Content%2F-2563eb" />
</p>
<p align="center">
  <img alt="external APIs: none" src="https://img.shields.io/badge/external%20APIs-none-brightgreen" /> <img alt="publishing: manual copy-paste" src="https://img.shields.io/badge/publishing-manual%20copy--paste-be185d" />
</p>
<p align="center">
  <img alt="runtime: Zo Computer" src="https://img.shields.io/badge/runtime-Zo%20Computer-111827" /> <img alt="model: Claude AI" src="https://img.shields.io/badge/model-Claude%20AI-CC785C?logo=claude&logoColor=white" />
</p>

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [Folder Structure](#folder-structure)

## Overview

Stay visible on LinkedIn without spending your week reading the news. This AI agent automation workflow runs a three-stage pipeline: it scans this week's notable industry news and social discourse, tracks funding rounds and product launches in the same niche, then synthesizes both into one short digest post, a hook, a handful of highlight bullets, and a discussion prompt, ready to copy, personalize, and post. Runs entirely on free, built-in Zo Computer research tools (`web_search`, `web_research`, `x_search`), no paid news-monitoring, funding-database, or firmographic API required. Every skill is also compatible with Claude AI or any agentic framework, not just Zo's own routing. Nothing is ever posted automatically, the digest is always a draft for you to review and publish yourself.

## Features

| Skill | What it does |
| --- | --- |
| `industry-news-scanner` | Scans this week's notable news and social discourse for the niche via `web_search`/`x_search`, filtering down to items a founder would actually want to reshare or discuss. |
| `funding-launch-tracker` | Tracks recent funding rounds and product/feature launches in the niche via `web_search`/`web_research`/`x_search`, capturing amount, stage, and investor only when a source states them. |
| `digest-writer` | Synthesizes both into one short LinkedIn-ready post: a hook, 3-6 traceable highlight bullets, and a closing discussion question. Never uses em dashes. |

## Requirements

- Built-in web tools only: `web_search`, `web_research`, `x_search`. No setup needed.
- No integration, API key, or paid third-party service is required or supported. This pipeline never calls a paid news-monitoring, funding-database, or firmographic API.

## Installation

### Fast path (recommended)

1. Open a **new Zo chat**.
2. Paste the entire contents of `installation-prompt.md` from this repo, with the repo URL filled in (it defaults to `https://github.com/robort-gabriel/weekly-industry-digest-for-founders`, swap it if you're installing from a fork).
3. Send it. The AI will fetch this repo into `Zo-Automations/Projects/weekly-industry-digest-for-founders/` on your Zo, verify the three skills, help you fill in `config/digest-topic.md`, create a dedicated "Weekly Industry Digest for Founders" persona scoped to this project, and ask whether to run the pipeline ad hoc and/or schedule it as a recurring automation, confirming with you before creating anything that runs unsupervised.

This is the whole install: no packages, no build step, no API keys.

### Manual path

If you'd rather install by hand:

1. Clone or download this repo.
2. Copy the whole folder into your Zo workspace at `/home/workspace/Zo-Automations/Projects/weekly-industry-digest-for-founders/`, preserving the structure below. The three skills must stay project-local at `Skills/industry-news-scanner/`, `Skills/funding-launch-tracker/`, `Skills/digest-writer/`, they are not installed globally, and moving them elsewhere breaks the project's scoping.
3. Edit `config/digest-topic.md` and replace the placeholder example with your real industry/niche, optionally companies to watch and focus areas.
4. (Optional) In a chat, ask Zo to create a persona for this project using the exact text in `persona.md` so you don't have to restate the pipeline every time.
5. Try it: paste one of the examples from `starter-prompts.md` into a chat.

### Claude AI path

The three skills (`industry-news-scanner`, `funding-launch-tracker`, `digest-writer`) are plain `SKILL.md` files with no Zo-specific dependencies, so they also run under Claude AI. There are two ways to install, depending on whether "chat" means claude.ai (Cowork) or Claude Code.

#### claude.ai (Cowork), pure chat, no terminal

Requires a Claude plan with Skills and code execution enabled (Pro, Max, Team, or Enterprise; not available on the Free plan).

1. Open a new claude.ai chat and paste the entire contents of `installation-prompt-claude.md` from this repo, with the repo URL filled in. Claude will fetch the three skill files from GitHub, package each one into its own downloadable `.zip`, and draft your Project custom instructions and knowledge files for you.
2. Go to **Settings → Capabilities** and turn on **Code execution**, **File creation**, and **Web search**. Code execution and file creation must be on before Skills can run or write files; web search is the direct substitute for this project's `web_research`/`web_search`/`x_search` calls.
3. Go to **Settings → Capabilities → Skills** and upload the three `.zip` files Claude generated for you, one per skill (`industry-news-scanner`, `funding-launch-tracker`, `digest-writer`). Skills must be uploaded as one zip per skill, not the whole `Skills/` folder as one zip. Toggle each one on after uploading.
4. Create a **Project** named "Weekly Industry Digest for Founders". Paste the custom instructions Claude drafted from `automation-prompt.md` into the Project's custom instructions, and upload `config/digest-topic.md` and `persona.md` as Project knowledge files. Every chat inside this Project then has the pipeline logic, the niche/topic config, and the three skills in scope automatically.
5. To run it, open a chat inside the Project and name a niche (see `starter-prompts.md` for examples). With code execution and file creation on, Claude creates and edits files during the conversation, covering `news-scan.md` → `funding-launches.md` → the finished digest post. This is chat-scoped file creation, not a persistent folder tree like the Zo version, so download the digest post you want to keep from each run.
6. For recurring runs, use Claude Cowork's **Scheduled Tasks** (Settings → Capabilities, or the schedule option in a chat) to describe the weekly job once and set it to run on a schedule, using the same instructions from `automation-prompt.md`. Nothing is ever posted automatically either way, the digest still needs your manual review, copy, and publish step.

#### Claude Code (CLI, higher fidelity)

Because the skills already live at `Skills/<name>/SKILL.md` with no Zo dependencies, Claude Code can run this project close to unmodified:

1. Copy or symlink this repo's `Skills/` folder into `.claude/skills/` in your Claude Code project (Claude Code reads skills from `.claude/skills/<name>/SKILL.md`), or point Claude Code's working directory at this repo and adjust the path if you'd rather leave the structure as-is.
2. Claude Code's native `WebSearch` tool directly replaces every `web_research`/`web_search`/`x_search` call in the three `SKILL.md` files, no extra setup needed.
3. Because Claude Code has a real filesystem, output files land in a persistent folder tree (`Content/Weekly-Industry-Digest/<niche-slug>/<run_date>.md`) exactly as designed, with no re-upload or context loss between runs.
4. Run the three stages in order in the main thread, or as subagents if you want each stage isolated with its own context window.
5. For recurring runs, Claude Code's scheduled task support (Routines) is the closest equivalent to Zo's scheduled agents, using the same `automation-prompt.md` instructions.

No API key or extra sign-up beyond your existing Claude AI access is required for either path.

## Configuration

No secrets required. Per-run parameters, passed stage to stage:

| Parameter | Required | Default | Used by |
| --- | --- | --- | --- |
| `niche` | Yes (or set in `config/digest-topic.md`) | - | all three skills |
| `topic_file` | No | `config/digest-topic.md` | `industry-news-scanner` / `funding-launch-tracker` |
| `run_date` | No | today's date | all three skills |
| `notify` | No | `none` (`email` also supported) | `digest-writer` / automation |

## Usage

**Ad hoc:** ask for each stage in sequence, or ask for the full pipeline in one request (see `starter-prompts.md`). The stages hand off through files:

```
industry-news-scanner  -> Content/Weekly-Industry-Digest/<niche-slug>/<date>/news-scan.md
funding-launch-tracker  -> Content/Weekly-Industry-Digest/<niche-slug>/<date>/funding-launches.md
digest-writer           -> Content/Weekly-Industry-Digest/<niche-slug>/<date>.md
```

**Recurring:** create a scheduled agent using `automation-prompt.md` as the instructions, with `niche` and `notify` set as preferred and a weekly frequency (the natural cadence for this project). Scheduling a recurring agent is not done automatically by this project, confirm the niche and frequency explicitly, since each run is a full Zo session. No matter the schedule, the digest is never posted to LinkedIn or anywhere else automatically, copy it, personalize it if you like, and post it yourself.

## Folder Structure

```
Zo-Automations/Projects/weekly-industry-digest-for-founders/
├── README.md
├── installation-prompt.md            # paste into a new Zo chat to auto-install everything
├── installation-prompt-claude.md     # paste into a new claude.ai chat to auto-install everything
├── persona.md                        # exact text for the dedicated "Weekly Industry Digest for Founders" persona
├── automation-prompt.md              # instructions for the scheduled agent
├── starter-prompts.md                # example prompts
├── config/
│   └── digest-topic.md               # editable niche, companies to watch, and focus areas
└── Skills/
    ├── industry-news-scanner/
    │   └── SKILL.md
    ├── funding-launch-tracker/
    │   └── SKILL.md
    └── digest-writer/
        ├── SKILL.md
        └── references/
            └── output-template.md    # final digest post template
```
