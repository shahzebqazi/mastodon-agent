# Mastodon draft — mix/master WIP (2026-05-27)

**Post body (what ships):** `2026-05-27-mix-master-wip.txt` (~280 chars + hashtags)

**Instance:** [social.devilplan.com/@willy](https://social.devilplan.com/@willy)

## Fill in before posting

- [ ] **Track title** (or keep vague if you prefer)
- [ ] **Genre / artist context** (solo, band, client work?)
- [ ] **One concrete detail** (e.g. “stem bounce”, “analog bus”, “Reaper + UAD”, “vocal de-ess pass”)
- [ ] **Visibility:** `public` (default) vs `unlisted` for quieter WIP notes

## Alternate openings (swap first paragraph in `.txt`)

**A — minimal**

```
Mix/master day on a track that’s been in the “almost there” folder for months. Today was low end + vocal balance; mastering moves tomorrow with fresh ears.
```

**B — gear-nerd**

```
Mix/master sprint: got the kick and bass to share space without the vocal drowning. Tomorrow is print-level stuff—limiter, last 0.5 dB of gain riding, then walk away.
```

**C — invite feedback (use sparingly; no @ unless you want replies)**

```
Working mix/master on something new-ish. If you care about low-end / vocal balance wars, I’m in that phase—happy to hear what you listen for before the final loudness pass.
```

## Post when ready

1. Copy `.env.example` → `mastodon-agent/.env` (or add vars to an existing `.env` you pass with `--env`).
2. Mastodon → **Preferences → Development** → app with **`write:statuses`**.
3. Review the `.txt` file, then:

```bash
cd ~/Git/cursor-agents/mastodon-agent
python3 scripts/post_status.py drafts/2026-05-27-mix-master-wip.txt
# or quieter:
python3 scripts/post_status.py drafts/2026-05-27-mix-master-wip.txt --visibility unlisted
```

**Human gate:** edit `2026-05-27-mix-master-wip.txt` until it reads right; only run the command when you want it live.
