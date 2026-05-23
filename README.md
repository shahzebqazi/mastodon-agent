<div align="center">

# mastodon-agent

**Compose and ship Mastodon posts from the terminal—without leaking secrets into chat or version control.**

*Fediverse · Plain UTF-8 files · `.env` for credentials*

![AI-generated hero: a robotic, mummified Mastodon rampaging — same art as the GitHub Pages site](docs/images/hero.png)

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Pages](https://img.shields.io/badge/docs-GitHub%20Pages-6ee7ff?logo=github)](https://shahzebqazi.github.io/mastodon-agent/)

</div>

---

## Why this exists

Drafts in a file, review in git, credentials in `.env`, and a small script you or automation can run—**not** copy-pasting tokens into prompts.

This repo is a **tool- and AI-agnostic** Mastodon toolkit. Product behavior and roadmap live in **[`docs/SPEC.md`](docs/SPEC.md)**.

---

## What you get today

| Piece | What it does |
|--------|----------------|
| **`scripts/post_status.py`** | Posts a UTF-8 text file via the Mastodon API (`/api/v1/statuses`). |
| **`.env.example`** | Safe template—copy to `.env` locally. **Never commit `.env`.** |
| **`docs/SPEC.md`** | Product spec (vision, trust model, phases)—editor-neutral. |
| **`docs/`** | GitHub Pages mini-site (**`images/hero.png`** hero artwork). |

---

## Runtime path

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

Enable **Settings → Pages** → source **main**, folder **`/docs`**:

**[https://shahzebqazi.github.io/mastodon-agent/](https://shahzebqazi.github.io/mastodon-agent/)**

---

## Security & privacy

- **Never commit** secrets, tokens, app passwords, or a populated `.env`.
- **Treat access tokens like passwords.** Rotate if one appears in chat or git.

---

## Cursor integration (optional)

Cursor-specific rules and session prompts live in the **[cursor-agents](https://github.com/shahzebqazi/cursor-agents)** monorepo (`mastodon-agent-cursor/` + submodule). They are **not required** to clone, build, or post from this repository.

---

## License

MIT — see [`LICENSE`](LICENSE).
