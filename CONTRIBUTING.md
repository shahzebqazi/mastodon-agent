# Contributing

Thanks for helping improve **mastodon-agent**. This path is **tool-agnostic**: Python, shell, or CI—no particular editor required.

## Product authority

Behavior and roadmap: **[`docs/SPEC.md`](docs/SPEC.md)**. Propose spec changes in the same PR as code when behavior shifts.

## Prerequisites

- **Python 3.8+** (stdlib only; `scripts/post_status.py` uses `urllib` and `pathlib`).
- **UTF-8** drafts end-to-end.

## Environment variables

Copy `.env.example` to `.env` (never commit `.env`):

| Variable | Meaning |
|----------|---------|
| `MASTODON_INSTANCE_URL` | Server base URL only, e.g. `https://example.social` |
| `MASTODON_ACCESS_TOKEN` | OAuth access token (treat like a password) |

Optional CLI flag: `--env /path/to/.env` if the file is not at the repository root.

## Verify locally

```bash
python3 -m compileall -q scripts
python3 scripts/post_status.py path/to/draft.txt --visibility unlisted   # needs .env
```

## Cursor / monorepo

**Do not** add `.cursor/` or editor-specific prompts here. Use **[cursor-agents](https://github.com/shahzebqazi/cursor-agents)** for Cursor integration (`mastodon-agent-cursor/`).

## Pull requests

- Keep changes focused; align with `docs/SPEC.md` phases where applicable.
- No tokens, secrets, or real `.env` in git.
