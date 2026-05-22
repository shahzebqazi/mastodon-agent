# Contributing

Thanks for helping improve **mastodon-agent**. This document is the contributor-facing path: it assumes a normal clone and standard tools—**not** any private configuration repository.

## Agent-driven development (Cursor)

After cloning, **Cursor** loads root **`AGENTS.md`**. The default working charter is **`docs/AGENT_PROMPT.md`** (open-ended tasks, milestones, constraints). **`.cursor/rules/mastodon-agent.mdc`** keeps those paths in context.

You do **not** need a private config repo to build or run the script; agent files here are **redacted patterns only**.

## Prerequisites

- **Python 3.8+** (stdlib only; `scripts/post_status.py` uses `urllib` and `pathlib`).
- A **UTF-8** text editor or shell that preserves encoding when you write post bodies (the script reads files as UTF-8 and sends JSON with `ensure_ascii=False`).

## Environment variables

Copy `.env.example` to `.env` (never commit `.env`). The posting script reads:

| Variable | Meaning |
|----------|---------|
| `MASTODON_INSTANCE_URL` | Server base URL only, e.g. `https://example.social` (no `/@username` path). |
| `MASTODON_ACCESS_TOKEN` | OAuth access token from your Mastodon app (treat like a password). |

Optional CLI flag: `--env /path/to/.env` if the file is not at the repository root.

## Verify locally

```bash
python3 -m compileall -q scripts
```

To exercise the API (requires real credentials in `.env`):

```bash
python3 scripts/post_status.py path/to/draft.txt --visibility unlisted
```

## Optional: Cursor and shared agent patterns

This repository intentionally keeps **product code and Mastodon-facing docs** separate from personal or machine-specific editor setup.

For **generic, redacted, reusable** guidance on structuring optional agent tooling alongside application repos, see **[cursor-agent-config](https://github.com/shahzebqazi/cursor-agent-config)**.

Personal automation, credentials patterns, or anything unsafe to publish belongs in a **private** config repository you maintain yourself; public builds and contributors must not depend on it.

## Pull requests

- Keep changes focused; prefer small PRs.
- Do not add real tokens, app passwords, client secrets, or committed `.env` files.
- If you add scripts or CI, ensure a fresh clone can still run documented steps without extra private repos.

## Remote URL

The GitHub repository is **`shahzebqazi/mastodon-agent`**. If `git remote -v` still shows the old name, run:

```bash
git remote set-url origin git@github.com:shahzebqazi/mastodon-agent.git
```
