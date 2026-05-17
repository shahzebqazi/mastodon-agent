<div align="center">

# mastodon-agent

**Compose and ship Mastodon posts from the terminal or your editor—without leaking secrets into chat or version control.**

*Fediverse · Plain UTF-8 files · `.env` for credentials*

![AI-generated hero: a robotic, mummified Mastodon rampaging — same art as the GitHub Pages site](docs/images/hero.png)

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Pages](https://img.shields.io/badge/docs-GitHub%20Pages-6ee7ff?logo=github)](https://shahzebqazi.github.io/mastodon-agent/)

*Badges and Pages URLs use the **mastodon-agent** name. Until you rename the GitHub repository from `mastodon-cursor-agent`, replace those URLs with your current repo name where needed.*

</div>

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
| **`docs/`** | A one-page **GitHub Pages** mini-site with a project overview (and a dramatic hero image). |

---

## Runtime path (for humans)

No editor-specific tooling is required.

1. **Prerequisites:** Python **3.8+** on your PATH as `python3`.
2. **Credentials:** On your Mastodon server, open **Preferences → Development → New application** and enable **`write:statuses`** (add read scopes later if you extend the tooling).
3. **Configure:**

   ```bash
   cp .env.example .env
   # Edit .env: set MASTODON_INSTANCE_URL and MASTODON_ACCESS_TOKEN
   ```

   `MASTODON_INSTANCE_URL` must be the **server base only**, e.g. `https://example.social` — not a profile URL with `/@you`.

4. **Write** your post as a **UTF-8** text file (any path/name).
5. **Post:**

   ```bash
   python3 scripts/post_status.py path/to/your_post.txt
   ```

   On success, the script prints the status URL.

### Options

```text
python3 scripts/post_status.py post.txt --visibility unlisted
python3 scripts/post_status.py post.txt --env /path/to/.env
```

### UTF-8

Post bodies are read with **UTF-8** encoding and sent as JSON with Unicode preserved (`ensure_ascii=False`). Use UTF-8 for drafts; avoid mixed encodings from legacy tools.

---

## GitHub Pages (project site)

Enable Pages on the repo (**Settings → Pages → Build and deployment → GitHub Pages** → source **main** / folder **`/docs`**). After the repository is named **mastodon-agent** on GitHub, the default Pages URL is:

**[https://shahzebqazi.github.io/mastodon-agent/](https://shahzebqazi.github.io/mastodon-agent/)**

If you still use the old repository name on GitHub until you rename it, the Pages URL will match that old name until you rename the repo (GitHub retargets `github.io` for renames in the usual way).

The hero image on that page is **AI-generated** project art (robotic / mummified Mastodon vibe). Code and prose in this repo are MIT-licensed; see `LICENSE`.

---

## Security & privacy

- **Never commit** secrets: access tokens, app passwords, client secrets, refresh tokens, or a populated `.env`. Use `.env.example` placeholders only; keep real values in `.env` (gitignored) or your platform’s secret store for CI.
- **Treat access tokens like passwords.** Revoke and rotate if one ever appears in a transcript, screenshot, or committed file.
- **Drafts** in this repo are ordinary files: if a draft contains sensitive or unpublished content, treat the branch or fork like sensitive data and avoid pushing it to public remotes until you intend to share it.
- **Personal automation** (editor hooks, machine paths, identity-specific runbooks) should **not** live in this public product repository long-term; keep them in a **private** configuration area you control. For **generic, redacted** patterns optional for contributors, see **[cursor-agent-config](https://github.com/shahzebqazi/cursor-agent-config)** and [`CONTRIBUTING.md`](CONTRIBUTING.md).
- Prefer **narrow OAuth scopes** and separate apps for “posting script” vs “full account automation” if you split workflows later.
- **This pass:** No known secrets were added to tracked files. If a token was ever committed in the past, rotate it and consider history rewrite only if your org requires it (rewriting history is out of scope here unless explicitly requested).

---

## Optional editor / agent layout

This repo is **product code + Mastodon-facing docs and tooling**. It should build and run for a third party **without** access to any private dotfiles repo.

One pointer for shared, **public** conventions (optional for contributors): **[cursor-agent-config](https://github.com/shahzebqazi/cursor-agent-config)**. Personal or beta Cursor material belongs in a **private** repo you maintain; nothing in this README assumes that repo exists on a contributor’s machine.

---

## Migration (from `mastodon-cursor-agent`)

**Inventory (Cursor-specific):** This tree had **no** `.cursor/` rules, hooks, skills, or editor-only harness files to extract—only `scripts/`, `docs/`, and root docs.

**Rename on GitHub:** When you are ready, rename the repository to **mastodon-agent** in the GitHub UI, then update:

- **Git remote:** `git remote set-url origin https://github.com/shahzebqazi/mastodon-agent.git` (or the SSH equivalent).
- **Default branch / CI:** unchanged unless you renamed the default branch too.
- **Bookmarks / Pages:** GitHub Pages URL will follow the new repo name.

**New public repo:** Add **[cursor-agent-config](https://github.com/shahzebqazi/cursor-agent-config)** as a separate public repository (clone the `cursor-agent-config` directory from your machine and `git init` / push if you are creating it for the first time).

**Private material:** Put personal Cursor infra in your private **`my-cursor-config`** (or equivalent); do not require it for builds.

---

## Roadmap (ideas)

- Thread / chunk helper for long posts  
- Media upload + alt-text prompts  
- Draft conventions for editors and review (e.g. `drafts/*.txt` + checklist)  
- Optional scheduling (only if you want server-side or external job runner complexity)

Contributions welcome—see [`CONTRIBUTING.md`](CONTRIBUTING.md). This is meant to stay **simple at the core** and composable at the edges.

---

## License

MIT — see [`LICENSE`](LICENSE).
