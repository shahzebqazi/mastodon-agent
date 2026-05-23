# Mastodon agent — product specification

**Tool- and AI-agnostic.** This document defines behavior, trust boundaries, and evolution of the Mastodon toolkit. Implementations may use Python scripts, cron, CI, or any assistant runtime; nothing here assumes a specific editor or LLM vendor.

## Vision

A **small, reliable** foundation for composing and publishing on Mastodon: UTF-8 drafts, credentials outside version control, explicit human approval before public posts, and room to grow into read-side automation **only with consent**.

## Non-goals

- Mass surveillance of timelines, hashtags, or arbitrary accounts.
- Non-consensual profiling (e.g. inferring taste or mood from others’ posts without opt-in).
- Storing access tokens in git, issues, or shared docs.
- Replacing instance moderation or Terms of Service compliance.

## Personas

| Persona | Need | MVP support |
|---------|------|-------------|
| **Poster** | Ship text from a file or pipeline | `scripts/post_status.py` |
| **Listener-logger** | Publish listening habits (scrobble-style) to own account | Future: scheduled job + template |
| **Curator** | Build playlists from **authorized** social signals | Future; requires consent + external music API |
| **Operator** | Debug failed posts, rotate tokens | Docs + clear HTTP errors |

## Trust model

- **Credentials:** `MASTODON_INSTANCE_URL` and `MASTODON_ACCESS_TOKEN` in local `.env` only (see `.env.example`).
- **OAuth scopes:** Start with `write:statuses`; add read scopes only when read features ship.
- **Human gate:** Default flow is **draft file → review → post**. Automated posting should use narrow tokens and visibility defaults (`unlisted` where appropriate).
- **Retention:** No long-term storage of others’ posts unless a feature documents purpose, retention, and deletion.

## Architecture (logical)

```
┌─────────────┐     ┌──────────────────┐     ┌─────────────────────┐
│ Draft store │────▶│ Transform/validate│────▶│ Mastodon REST client │
│ (UTF-8 files)│     │ (length, UTF-8)  │     │ POST /api/v1/statuses│
└─────────────┘     └──────────────────┘     └─────────────────────┘
                              ▲
                              │ optional future
                    ┌─────────┴──────────┐
                    │ Ingestion (opt-in) │
                    │ streaming / poll   │
                    └────────────────────┘
```

**Current implementation:** draft file + `post_status.py` only. Ingestion and LLM layers are **future** and must not block the posting critical path.

## API anchors

- Post status: [Mastodon API — statuses](https://docs.joinmastodon.org/methods/statuses/)
- Visibility: `public`, `unlisted`, `private`, `direct`
- Rate limits: respect instance limits; backoff on `429`
- Instance URL: scheme + host only (no `/@username` path)

## Fediverse etiquette

- Avoid unsolicited @-mentions and reply spam.
- Honor `#nobot` and instance bot policies where applicable.
- Document bot behavior in account bio or pinned post when running automated accounts.

## Phases

### Phase 0 (current)

- UTF-8 post from file
- `.env` credentials
- CI: syntax check only (no network)

**Exit criteria:** Contributor can clone, configure `.env`, post once, without any AI or editor tooling.

### Phase 1 — Posting hardening

- Dry-run mode, clearer HTTP error bodies, character-count validation
- Optional `--spoiler-text`, thread/chunk helper for long posts

**Exit criteria:** Failed posts are diagnosable without pasting tokens into logs.

### Phase 2 — Draft workflow

- Conventional `drafts/` layout, templates, review checklist in CONTRIBUTING

**Exit criteria:** Draft → review → post is documented and repeatable.

### Phase 3 — Opt-in read / listen-log (stretch)

- **Listen-log:** publish own listening events (Ampache, MPD, Last.fm-style) to **own** account via templates
- **Curator:** only after explicit consent model + external playlist API; never silent scraping of others’ feeds

**Exit criteria:** Privacy section in this spec updated; each feature has opt-in documented.

## Evaluation

| Metric | How |
|--------|-----|
| Post success rate | Count 2xx vs 4xx/5xx in operator logs |
| Secret hygiene | No tokens in git; periodic grep in CI |
| UTF-8 fidelity | Round-trip test with non-ASCII sample draft |

## Cursor / editor integration

**Not part of this repository.** For Cursor-specific rules and session prompts, use **[cursor-agents](https://github.com/shahzebqazi/cursor-agents)** (`mastodon-agent-cursor/` alongside the submodule). This spec remains the single product authority.
