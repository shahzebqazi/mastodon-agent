<div align="center">

# Mastodon Cursor Agent

**Compose and ship Mastodon posts from your editor—without leaking secrets into chat.**

*Fediverse · Cursor · Plain UTF-8 files · `.env` for credentials*

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Pages](https://img.shields.io/badge/docs-GitHub%20Pages-6ee7ff?logo=github)](https://shahzebqazi.github.io/mastodon-cursor-agent/)

</div>

---

## Why this exists

If you live in **Cursor** and you’re spending more time on **Mastodon**, you probably want a workflow that feels like code: drafts in a file, review in git, credentials in `.env`, and a tiny script your agent can run—**not** copy-pasting tokens into prompts.

This repo is that starting point: a **small, boring, reliable** poster plus room to grow into scheduling, threads, media, and moderation helpers as your needs grow.

---

## What you get today

| Piece | What it does |
|--------|----------------|
| **`scripts/post_status.py`** | Posts a UTF-8 text file via the Mastodon API (`/api/v1/statuses`). |
| **`.env.example`** | Safe template—copy to `.env` and fill in locally. **Never commit `.env`.** |
| **`docs/`** | A one-page **GitHub Pages** mini-site with a project overview (and a dramatic hero image). |

---

## Quick start

1. **Clone** this repository.

2. **Create credentials** on your Mastodon server:  
   **Preferences → Development → New application**  
   Enable **`write:statuses`** (add read scopes later if you extend the tooling).

3. **Configure locally**

   ```bash
   cp .env.example .env
   # Edit .env: set MASTODON_INSTANCE_URL and MASTODON_ACCESS_TOKEN
   ```

   `MASTODON_INSTANCE_URL` should be the **server base only**, e.g. `https://example.social` — not a profile URL with `/@you`.

4. **Write a post** (any filename), then:

   ```bash
   python3 scripts/post_status.py path/to/your_post.txt
   ```

   On success, the script prints the status URL.

### Options

```text
python3 scripts/post_status.py post.txt --visibility unlisted
python3 scripts/post_status.py post.txt --env /path/to/.env
```

---

## GitHub Pages (project site)

After you enable Pages on the repo (**Settings → Pages → Build and deployment → GitHub Pages** → source **main** / folder **`/docs`**), the site will be available at:

**[https://shahzebqazi.github.io/mastodon-cursor-agent/](https://shahzebqazi.github.io/mastodon-cursor-agent/)**

The hero image on that page is **AI-generated** project art (robotic / mummified Mastodon vibe). Code and prose in this repo are MIT-licensed; see `LICENSE`.

---

## Security

- **Treat access tokens like passwords.** Revoke and rotate if one ever appears in a transcript, screenshot, or committed file.
- **Never commit** `.env`. This repo’s `.gitignore` ignores it by default.
- Prefer **narrow OAuth scopes** and separate apps for “posting bot” vs “full account automation” if you split workflows later.

---

## Roadmap (ideas)

- Thread / chunk helper for long posts  
- Media upload + alt-text prompts  
- Draft conventions for Cursor (e.g. `drafts/*.txt` + review checklist)  
- Optional scheduling (only if you want server-side or external job runner complexity)

Contributions and issues welcome—this is meant to stay **simple at the core** and composable at the edges.

---

## License

MIT — see [`LICENSE`](LICENSE).
