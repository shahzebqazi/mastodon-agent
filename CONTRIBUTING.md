# Contributing

Thanks for helping improve **mastodon-agent**. This document is the contributor-facing path: it assumes a normal clone and standard tools—**not** any specific editor or private configuration repository.

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

## Repo rename note

If you cloned this project under an older remote name, update your `origin` URL after the GitHub repository is renamed to **mastodon-agent** (see the README migration section).
