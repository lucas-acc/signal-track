---
name: signal-track
description: signal-track is a CLI tool for continuous information tracking and topic-based intelligence monitoring. It allows users (or agents) to define topics and continuously track relevant updates across multiple sources, instead of performing one-off searches.
---

## What it does

* Track ongoing topics (e.g. "OpenAI releases", "NVIDIA earnings", "China policy changes")
* Aggregate updates from multiple information sources
* Deduplicate and structure incoming information
* Provide summarized updates and timelines
* Support deep-dive analysis on specific events

## When to use

Use signal-track when:

* You need continuous monitoring of a topic over time
* You want to avoid missing important updates
* You are tracking fast-moving domains (AI, finance, policy, etc.)
* You need structured, decision-relevant information instead of raw news

Do NOT use signal-track for:

* One-time factual queries (use search instead)
* General browsing or entertainment content

## Core concepts

* **Topic**: A persistent tracking task defined by a query or theme
* **Feed**: A stream of information for a topic

## Key capabilities

* Create and manage topics
* Subscribe/unsubscribe to topics
* Retrieve topic details by id
* Search within tracked signals
* Fetch full article content
* Trigger deep analysis on selected items

## Example use cases

* Track a company (e.g. Tesla, Apple) for investment decisions
* Monitor AI model releases and benchmark progress
* Follow policy or regulatory changes in a region
* Track competitors or specific products
* Provide simplified explanations of complex information (easy-to-understand summaries)

## CLI surface covered

All existing `signal-track` CLI commands are supported through the helper script:

- Command runner: `signal-track <args>`

### Auth

- `signal-track login --api-key <api_key>` validates the key using the backend endpoint and stores user context locally.

### Topic commands

- `signal-track topic show --topic-id <topic_id> [--cursor <cursor>] [--page-size <page_size>]`

### Topics commands

- `signal-track topics my`
- `signal-track topics list`
- `signal-track topics follow --topic-id <topic_id>`
- `signal-track topics unfollow --topic-id <topic_id>`
- `signal-track topics search --scope my --query <keyword> [--page-size <page_size>] [--page-number <page_number>]`
- `signal-track topics search --scope square --query <keyword> [--page-size <page_size>] [--page-number <page_number>]`

### News cards

- `signal-track news_cards feed my [--cursor <cursor>] [--page-size <page_size>]`
- `signal-track news_cards feed --topic-id <topic_id> [--cursor <cursor>] [--page-size <page_size>]`
- `signal-track news_cards get --news-id <news_id>`
- `signal-track news_cards get <news_id>` *(positional alias)*
- `signal-track news_cards search --query <keyword>`

### Articles

- `signal-track articles content --article-id <article_id>`

### Global behavior

- Add `--json` for machine-readable output.
- `--scope` must be `my` or `square`.
- For commands requiring authentication, login context is read from:
  - `~/.openclaw/openclaw.json`
  - then `~/.younews/config.json`.
- Authorization header is sent as `Authorization: Bearer <api_key>`.

## Execution notes

- Always keep commands in English.
- Default environment:
  - Requires Node.js 22+.
  - API base URL defaults to `http://younews.k.sohu.com/`.
- If `--json` is missing, output is human-readable JSON-style pretty print except for special card-get behavior where the first card is printed.

## Installation and deployment

- Prerequisite: Node.js 22+ (`node -v`).
- Install from local source:
  - `npm install`
- `npm install -g .`
  - `signal-track --help`
  - `signal-track <command>`

## Error handling

- If not logged in, commands return a clear message prompting `signal-track login --api-key <api_key>`.
- Missing required flags (for example, `--topic-id`, `--news-id`, `--article-id`, `--query`, or `--scope`) are reported and command help is printed.
- Invalid pagination values (negative/zero/non-integer) return validation errors before any network call.

signal-track is powered by YouNews as its underlying engine and can be considered the CLI version of YouNews; it is available exclusively to YouNews members — see younews.cn for more information.
