---
name: orbit-cards
description: >-
  Generate shareable X (Twitter) headers, profile picture rings, "My orbit"
  interaction circles, monthly recaps, shout-out cards, post cards, Time Machine
  cards, milestones, follower mosaic thank-you photos (spelling any text like
  "2000" or "THANK YOU" out of circular follower avatars), thanks cards, and
  trophies for any public X @handle or X post URL. Reads public X data free with
  no API key or login via FxTwitter (with VxTwitter profile fallback) and
  renders 265 designs (631 looks) to PNG or SVG locally. Use whenever the user
  asks to make an X header, Twitter banner, orbit card, follower circle,
  follower thank-you mosaic, monthly X recap, profile ring, shout-out card,
  post-to-image card, milestone card, or Orbit Cards graphic.
---

# Orbit Cards

Generate high-resolution X (Twitter) cards and headers for any public `@handle` or post URL using the bundled CLI at [orbit-cards.mjs](./scripts/orbit-cards.mjs).

No API key or X login is required: the CLI reads public X data through FxTwitter (`api.fxtwitter.com`) with automatic VxTwitter (`api.vxtwitter.com`) profile fallback and timeline fallback, then renders locally with Satori + Resvg.

## One-Time Setup

The CLI is self-contained except for three small Node packages (`satori`, `@resvg/resvg-js`, `react`). Before the first run, check if `scripts/node_modules` exists; if not, install them once:

```bash
SKILL_DIR="<path-to-this-skill>"
test -d "$SKILL_DIR/scripts/node_modules" || npm install --prefix "$SKILL_DIR/scripts" --no-audit --no-fund
```

## Workflow

### 1. Fetch & Inspect an X Account (Optional Separate Step)

`render --handle @user` reads automatically and caches the snapshot at `~/.cache/orbit-cards/<handle>.json` for 24 hours. To read upfront or inspect top orbit people and top post IDs first:

```bash
node "$SKILL_DIR/scripts/orbit-cards.mjs" fetch @handle          # full public read (30d + followers + 12-month history)
node "$SKILL_DIR/scripts/orbit-cards.mjs" fetch @handle --fast   # light read (posts & mentions only)
node "$SKILL_DIR/scripts/orbit-cards.mjs" inspect @handle        # shows followers, top orbit people, top post IDs
```

### 2. Choose Designs

There are **10 sets** (265 designs, 631 looks):

| Set ID | What it makes | Default size |
| :--- | :--- | :--- |
| `header` | X profile headers (Mosaic, Spectrum, Constellation, Polaroids, Unboxed, …) | `header` (1500×500) |
| `ring` | Profile picture badge rings (Follower club, Building in public, Streak, …) | `square` (1080×1080) |
| `shoutout` | One-person shout-out cards (My #1, Two-way street, MVP, Duo, …) | `square` |
| `post` | Styled quote/post cards from their top post or any `--post-url` | `square` |
| `recap` | Monthly / 7d / 90d activity recaps, heatmaps, Unboxed summaries | `square` |
| `circle` | "My orbit" interaction maps (Dinner table, Tarot, Name tags, …) | `square` |
| `timemachine` | 12-month & 1-year-ago comparisons | `square` |
| `milestone` | Follower, view, and streak milestone cards | `square` |
| `thanks` | Follower thank-you cards (Follower mosaic, Welcome mat, Receipt, Guestbook, …) | `square` |
| `achievement` | Trophies, enamel pins, gold records | `square` |

For the full list of card IDs, look indices, and sizes, read [designs.md](./references/designs.md) or run:

```bash
node "$SKILL_DIR/scripts/orbit-cards.mjs" list --set header
node "$SKILL_DIR/scripts/orbit-cards.mjs" list --search unboxed
```

### 3. Render Cards

```bash
# Starter pack (2 headers + orbit + recap + shout-out + ring)
node "$SKILL_DIR/scripts/orbit-cards.mjs" render --handle @handle --pack --out ./cards

# Specific cards and looks (cardId:colourIndex)
node "$SKILL_DIR/scripts/orbit-cards.mjs" render --handle @handle \
  --card header-mosaic:1 --card circle-dinner --card recap-wrapped \
  --out ./cards

# Single card to a specific PNG path at 2x resolution
node "$SKILL_DIR/scripts/orbit-cards.mjs" render --handle @handle \
  --card header-spectrum --look 2 --scale 2 --out ./banner.png

# Turn any single X post URL into a post card (no full account read needed)
node "$SKILL_DIR/scripts/orbit-cards.mjs" render \
  --post-url "https://x.com/user/status/1234567890" \
  --card post-classic --out ./post.png

# Follower mosaic thank-you photo (spells any text out of circular follower avatars with A-Z / 1-N coordinates)
node "$SKILL_DIR/scripts/orbit-cards.mjs" render --handle @handle \
  --card thanks-mosaic --text "2000" --scale 2 --out ./thanks-2000.png

node "$SKILL_DIR/scripts/orbit-cards.mjs" render --handle @handle \
  --card thanks-mosaic --text "THANK YOU" --scale 2 --out ./thank-you.png

# Shout-out for a specific person, or custom copy
node "$SKILL_DIR/scripts/orbit-cards.mjs" render --handle @handle \
  --card shout-number-one --person @friend --no-mark --out ./shout.png
```

### Useful Render Flags

- **Input:** `--handle @user`, `--post-url <url|id>`, `--snapshot <file.json>`, `--refresh` (bypass 24h cache), `--fast` (light read), `--tz <IANA>`
- **Selection:** `--card <id[:look]>` (repeatable/comma-separated), `--set <setId>` (with optional `--all-looks`), `--pack`, `--picks <picks.json>`
- **Output:** `--out <dir-or-file>`, `--format png|svg`, `--scale 1|2`, `--size square|portrait|story|landscape|header`, `--json`
- **Customization:** `--look <n>` (for `thanks-mosaic`: `0`=Dark, `1`=Light, `2`=Midnight), `--who mix|orbit|followers`, `--period 7|30|90`, `--person @handle`, `--post <postId>`, `--title`, `--subtitle`, `--text` / `--line` (custom text for text-led designs & `thanks-mosaic`, e.g. `"2000"` or `"THANK YOU"`), `--followers <n|all>` (max followers to paginate, default `600` for `thanks-mosaic`, or `all` for every follower), `--date YYYY-MM-DD`, `--ring-text`, `--full-circle`, `--accent #RRGGBB`, `--shape circle|rounded|square`, `--border none|ring|shadow`, `--grain`, `--hide-names`, `--no-handles`, `--no-numbers` (also hides A-Z / 1-N coordinates on `thanks-mosaic`), `--no-mark`, `--seed <n>`, `--people-count <n>`, `--people-order closeness|colour|random`, `--include h1,h2`, `--exclude h1,h2`

## Verification

- Check the CLI exit code and output paths. If FxTwitter is temporarily flaky and a part comes back missing, the CLI notes it and still renders every card the remaining data supports; pass `--refresh` later for a fresh read.
- When the CLI prints a `caption:` line, include the suggested X post text alongside the rendered image paths.
