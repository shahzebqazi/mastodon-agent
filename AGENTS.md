# Agent instructions (mastodon-agent)

This file is loaded for **Cursor** and other tooling that reads repo-local agent guidance. Treat it as the **index**; the full working charter lives in **`docs/AGENT_PROMPT.md`**.

## Read first

1. **`docs/AGENT_PROMPT.md`** — default session goals, constraints, and suggested workflows (start here when the user opens the repo or says “continue”).
2. **`README.md`** — human-facing overview, quick start, security.
3. **`CONTRIBUTING.md`** — prerequisites, env vars, verification commands.

## Hard rules

- **Never** commit `.env`, tokens, app passwords, client secrets, or real instance-specific credentials. Use `.env.example` only as a template.
- **Never** paste live access tokens into chat, issues, or docs.
- Prefer **small, reviewable changes**; match existing Python style in `scripts/`.
- Post bodies and drafts are **UTF-8**; preserve encoding end-to-end.

## Repo map

| Path | Role |
|------|------|
| `scripts/post_status.py` | Post a UTF-8 file via Mastodon REST API (`/api/v1/statuses`). |
| `.env.example` | Safe env var names and placeholders. |
| `docs/` | GitHub Pages site (`index.html`, `styles.css`, **`images/hero.png`** artwork). |
| `.cursor/rules/` | Cursor rule that reminds agents to load this file + `docs/AGENT_PROMPT.md`. |

## Default stance when the user is vague

Confirm whether they want **runtime work** (script, API, drafts), **docs/Pages**, or **agent/repository hygiene**. If they say “just work,” open **`docs/AGENT_PROMPT.md`**, pick the next unchecked or implied milestone, and state your plan in one short paragraph before editing.
