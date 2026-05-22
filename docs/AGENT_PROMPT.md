# Default session charter — mastodon-agent

Use this document when **starting work in a fresh clone** or when the user says **continue**, **pick up**, or **what should we do** without a narrower task.

## Mission

Grow this repository into a **small, reliable Mastodon toolkit**: plain-text drafts, credentials in `.env`, a minimal posting script, and room for safe automation (threads, media, moderation helpers) **without** turning the repo into personal editor config or leaking secrets.

## Product boundaries

- **In scope:** Python stdlib tooling, docs, GitHub Pages under `docs/`, CI that needs **no** secrets (e.g. `compileall`), clear contributor docs.
- **Out of scope for committed files:** machine-specific paths, private tokens, “my” infra hostnames, or anything that belongs in a **private** dotfiles/config repo.
- **Artwork:** Preserve **`docs/images/hero.png`** and existing Pages layout unless the user explicitly requests a redesign.

## Technical anchors

- **Posting:** `python3 scripts/post_status.py <file.txt>` — reads `MASTODON_INSTANCE_URL` and `MASTODON_ACCESS_TOKEN` from `.env` (see `.env.example`).
- **API:** Mastodon REST [`POST /api/v1/statuses`](https://docs.joinmastodon.org/methods/statuses/) — respect rate limits and visibility (`public`, `unlisted`, `private`, `direct`).
- **Fediverse etiquette:** avoid spammy bots, unsolicited mentions, or scraping without consent; document opt-in when adding read/search features.

## Suggested workstreams (pick one per session unless asked otherwise)

1. **Harden posting:** clearer errors from HTTP 4xx/5xx, dry-run flag, max length / validation, spoiler text support.
2. **Draft workflow:** `drafts/` layout, template file, short checklist in README or CONTRIBUTING.
3. **Docs:** tighten README/Pages; link official Mastodon docs where API behavior is non-obvious.
4. **Spec / roadmap:** extend toward listen-log / playlist-style ideas **only** with explicit privacy and consent design (no silent profiling).

## Session checklist

- [ ] Read `AGENTS.md` (index) and this file.
- [ ] Run `python3 -m compileall -q scripts` after Python edits.
- [ ] Do not add secrets; grep for accidental token patterns before finishing.
- [ ] If changing Pages, keep **`docs/images/hero.png`** referenced and working.

## Optional external patterns

For **generic, reusable** Cursor/agent repo patterns (not required to run this project), see **[cursor-agent-config](https://github.com/shahzebqazi/cursor-agent-config)** if published under that name; otherwise skip.
