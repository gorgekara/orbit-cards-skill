# Orbit Cards Skill

Generate shareable X (Twitter) graphics for any public `@handle` or X post URL: **follower mosaic thank-you photos**, **X headers**, **orbit circles**, **monthly recaps**, **profile picture rings**, **post-to-image cards**, **shout-outs**, **milestones**, **Time Machine comparisons**, and **trophies**.

- **265 designs, 631 looks** across 10 sets
- **Free, no API key or X login required**: reads public X data via FxTwitter with automatic VxTwitter fallback
- **Renders locally** to crisp PNG (1× or 2×) or SVG

---

## Quick Start (With Your AI Agent)

Install the skill in one command:

```bash
npx skills add gorgekara/orbit-cards-skill
```

Then just ask your agent in plain English for whatever you want to make. Here are ready-to-use prompts for each category:

### What You Can Ask For

| What you want | Copy-paste prompt |
| :--- | :--- |
| **Follower mosaic thank-you photo** | *"Make a follower mosaic thank-you photo for @yourhandle that spells 2000"* or *"Create a THANK YOU follower mosaic for @yourhandle"* |
| **X profile header / banner** | *"Generate 3 X headers for @yourhandle (Mosaic, Spectrum, and Polaroids)"* |
| **Starter pack (6 best cards)** | *"Make a starter pack of Orbit Cards for @yourhandle"* |
| **Post-to-image card** | *"Turn https://x.com/user/status/1234567890 into a post card (Classic and Minimal)"* |
| **My orbit circle** | *"Render my orbit interaction circle for @yourhandle"* |
| **Monthly / 7d / 90d recap** | *"Make a 30-day X recap card for @yourhandle"* |
| **Profile picture ring** | *"Create a Building in Public profile picture ring for @yourhandle"* |
| **Shout-out card for a friend** | *"Make a shout-out card for @friend from @yourhandle"* |
| **Follower / view milestone** | *"Generate a milestone card for @yourhandle"* |
| **Time Machine (1 year ago)** | *"Make a 1-year-ago Time Machine card for @yourhandle"* |
| **Trophies & badges** | *"Generate a trophy card for @yourhandle"* |

---

## All 10 Card Sets

| Set (`--set`) | Designs | What it makes | Default size |
| :--- | :---: | :--- | :--- |
| `thanks` | 15 | **Follower mosaic** (spells any text out of follower photos), Welcome mat, Guest list, Arrivals board, Wall of faces | `square` (1080×1080) |
| `header` | 25 | X profile banners (Spectrum, Mosaic, Constellation, Polaroids, Skyline, Ticker, Unboxed, and more) | `header` (1500×500) |
| `ring` | 23 | Profile picture badge rings (Building in public, Follower club, On fire, Laurel wreath, Neon, Streak) | `square` (1080×1080) |
| `post` | 23 | Styled quote/post cards from any X post URL or your top post (Classic, Minimal, Terminal, Polaroid, Receipt) | `square` (1080×1080) |
| `circle` | 25 | "My orbit" interaction maps showing who you talk with most (Dinner table, Constellation, Tarot, Name tags) | `square` (1080×1080) |
| `recap` | 30 | 7-day, 30-day, and 90-day activity recaps, heatmaps, and Unboxed summaries | `square` (1080×1080) |
| `shoutout` | 22 | One-person appreciation cards (My #1, Two-way street, MVP, Magazine cover, Wanted poster, Duo) | `square` (1080×1080) |
| `milestone` | 48 | Follower, view, and streak milestone celebration cards | `square` (1080×1080) |
| `timemachine` | 24 | 12-month growth charts and 1-year-ago comparisons | `square` (1080×1080) |
| `achievement` | 30 | Trophies, medals, enamel pins, gold records, and plaques | `square` (1080×1080) |

Browse every card ID and colourway in [references/designs.md](./skills/orbit-cards/references/designs.md).

---

## Direct CLI Recipes (Optional)

You can also run the bundled CLI directly without an agent. First, install its 3 small Node dependencies once:

```bash
npm install --prefix skills/orbit-cards/scripts --no-audit --no-fund
```

### 1. Follower Mosaic Thank-You Photo
Spells any word or milestone number (`"500"`, `"2000"`, `"10K"`, `"THANK YOU"`) using your followers' circular profile photos in an `A-Z` / `1-N` coordinate grid:

```bash
# Milestone number (Dark look, 2x crisp PNG)
node skills/orbit-cards/scripts/orbit-cards.mjs render \
  --handle @yourhandle --card thanks-mosaic --text "2000" --scale 2 --out ./thanks-2000.png

# Custom message (auto-wraps cleanly into two lines)
node skills/orbit-cards/scripts/orbit-cards.mjs render \
  --handle @yourhandle --card thanks-mosaic --text "THANK YOU" --scale 2 --out ./thank-you.png

# Light look (:1) or Midnight look (:2), fetching as many followers as available
node skills/orbit-cards/scripts/orbit-cards.mjs render \
  --handle @yourhandle --card thanks-mosaic:1 --text "10K" --followers all --scale 2 --out ./thanks-10k.png
```

### 2. X Profile Headers
```bash
# Generate 3 popular headers at once
node skills/orbit-cards/scripts/orbit-cards.mjs render \
  --handle @yourhandle \
  --card header-mosaic --card header-spectrum --card header-polaroids \
  --scale 2 --out ./headers
```

### 3. Curated Starter Pack (6 Cards Across Sets)
Generates 2 headers + orbit circle + monthly recap + shout-out + profile ring in one run:

```bash
node skills/orbit-cards/scripts/orbit-cards.mjs render \
  --handle @yourhandle --pack --out ./cards
```

### 4. Turn Any X Post URL into a Card
Works on any public post URL without reading the full account:

```bash
node skills/orbit-cards/scripts/orbit-cards.mjs render \
  --post-url "https://x.com/user/status/1234567890" \
  --card post-classic --card post-minimal:1 --scale 2 --out ./post-cards
```

### 5. Profile Picture Ring & Shout-Out
```bash
# Profile picture ring with custom text
node skills/orbit-cards/scripts/orbit-cards.mjs render \
  --handle @yourhandle --card ring-building --ring-text "BUILDING IN PUBLIC" --scale 2 --out ./ring.png

# Shout-out card for a specific person
node skills/orbit-cards/scripts/orbit-cards.mjs render \
  --handle @yourhandle --card shout-number-one --person @friend --scale 2 --out ./shout.png
```

### 6. Explore & Search All 265 Designs
```bash
# List every design in a set
node skills/orbit-cards/scripts/orbit-cards.mjs list --set header
node skills/orbit-cards/scripts/orbit-cards.mjs list --set thanks

# Search by keyword
node skills/orbit-cards/scripts/orbit-cards.mjs list --search mosaic
node skills/orbit-cards/scripts/orbit-cards.mjs list --search unboxed

# Inspect an account's cached stats, top orbit people, and top posts
node skills/orbit-cards/scripts/orbit-cards.mjs inspect @yourhandle
```

---

## Handy Flags

| Flag | What it does |
| :--- | :--- |
| `--card <id[:look]>` | Pick one or more designs and optional colourway index (e.g. `thanks-mosaic:1`, `header-spectrum:2`) |
| `--set <setId>` | Render every design in a set (add `--all-looks` for every colourway) |
| `--text "2000"` | Custom text for `thanks-mosaic` and text-led cards (alias for `--line`) |
| `--followers <n\|all>` | Max followers to fetch for `thanks-mosaic` (default `600`, or `all`) |
| `--scale 2` | Render at 2× high resolution |
| `--size <size>` | `square`, `portrait`, `story`, `landscape`, or `header` |
| `--format svg` | Output vector SVG instead of PNG |
| `--no-mark` | Hide the `"Made with Orbit Cards"` watermark |
| `--no-numbers` | Hide stand-alone numbers (also hides `A-Z` / `1-N` coordinates on `thanks-mosaic`) |
| `--refresh` | Bypass the 24-hour local cache (`~/.cache/orbit-cards/`) and fetch fresh data |

For full documentation and every option, see [skills/orbit-cards/SKILL.md](./skills/orbit-cards/SKILL.md).

Built by [Orbit Cards](https://orbitcards.app).
