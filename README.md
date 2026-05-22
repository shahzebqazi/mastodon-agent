<div align="center">

# mastodon-agent

**Compose and ship Mastodon posts from the terminal or your editor—without leaking secrets into chat or version control.**

*Fediverse · Plain UTF-8 files · `.env` for credentials*

![AI-generated hero: a robotic, mummified Mastodon rampaging — same art as the GitHub Pages site](docs/images/hero.png)

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Pages](https://img.shields.io/badge/docs-GitHub%20Pages-6ee7ff?logo=github)](https://shahzebqazi.github.io/mastodon-agent/)

</div>

---

## Clone → agent session (Cursor)

This repo ships **repo-local agent guidance** so a clone is ready to work:

| File | Purpose |
|------|--------|
| **`AGENTS.md`** | Short index and hard rules (Cursor loads this for the workspace). |
| **`docs/AGENT_PROMPT.md`** | Default session charter when you say *continue* or start without a narrow task. |
| **`.cursor/rules/mastodon-agent.mdc`** | Reminds agents to read the two files above. |

After `git clone`, open the folder in Cursor: follow **`AGENTS.md`** then **`docs/AGENT_PROMPT.md`** before large changes.

---

## Why this exists

If you spend time on **Mastodon**, a workflow that feels like code helps: drafts in a file, review in git, credentials in `.env`, and a small script you or automation can run—**not** copy-pasting tokens into prompts.

This repo is that starting point: a **small, boring, reliable** poster plus room to grow into scheduling, threads, media, and moderation helpers as your needs grow.

---

## What you get today

| Piece | What it does |
|--------|----------------|
| **`scripts/post_status.py`** | Posts a UTF-8 text file via the Mastodon API (`/api/v1/statuses`). |
| **`.env.example`** | Safe template—copy to `.env` and fill in locally. **Never commit `.env`.** |
| **`docs/`** | GitHub Pages mini-site (**`images/hero.png`** hero artwork preserved). |

---

## Runtime path (for humans)

1. **Prerequisites:** Python **3.8+** as `python3`.
2. **Credentials:** Mastodon **Preferences → Development → New application** with **`write:statuses`**.
3. **Configure:**

   ```bash
   cp .env.example .env
   # MASTODON_INSTANCE_URL (base URL only), MASTODON_ACCESS_TOKEN
   ```

4. **Post:**

   ```bash
   python3 scripts/post_status.py path/to/your_post.txt
   ```

### Options

```text
python3 scripts/post_status.py post.txt --visibility unlisted
python3 scripts/post_status.py post.txt --env /path/to/.env
```

### UTF-8

Drafts are read as **UTF-8**; JSON is sent with Unicode preserved (`ensure_ascii=False`).

---

## GitHub Pages

Enable **Settings → Pages** with source **main** and folder **`/docs`**. The project site is typically:

**[https://shahzebqazi.github.io/mastodon-agent/](https://shahzebqazi.github.io/mastodon-agent/)**

---

## Security & privacy

- **Never commit** secrets, tokens, app passwords, or a populated `.env`.
- **Treat access tokens like passwords.** Rotate if one appears in chat or git.
- **Personal automation** belongs in a **private** config repo; optional public patterns: **[cursor-agent-config](https://github.com/shahzebqazi/cursor-agent-config)**.

---

## Related monorepo (optional)

A broader **cursor-agents** monorepo may also carry a copy of this toolkit. **This repository remains the focused clone** for Mastodon posting + Pages + agent bootstrap files above. Prefer PRs here unless you intentionally consolidate upstream.

---

## License

MIT — see [`LICENSE`](LICENSE).
