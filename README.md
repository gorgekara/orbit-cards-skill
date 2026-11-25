# Orbit Cards Skill

An agent skill for generating shareable X (Twitter) headers, profile picture rings, "My orbit" interaction circles, monthly recaps, shout-out cards, post cards, Time Machine cards, milestones, thanks cards, and trophies for any public X `@handle` or post URL.

- **265 designs, 631 looks** across 10 sets
- **Follower mosaic thank-you photos**: spell any text (like `"2000"` or `"THANK YOU"`) out of circular follower avatars in a coordinate-labelled grid (`A-Z`, `1-N`)
- **No API key or X login required**: reads public X data through FxTwitter (`api.fxtwitter.com`) with automatic VxTwitter (`api.vxtwitter.com`) profile fallback
- **Renders locally** to PNG (1×/2×) or SVG with Satori + Resvg

## Install

```bash
npx skills add gorgekara/orbit-cards-skill
```

## Example Prompts

- *"Generate an X header for @yourhandle"*
- *"Make a 2000 followers thank-you mosaic photo for @yourhandle"*
- *"Create a THANK YOU follower mosaic for @yourhandle"*
- *"Make a starter pack of Orbit Cards for @yourhandle"*
- *"Turn https://x.com/user/status/1234567890 into a post card"*
- *"Render a monthly recap and my orbit circle for @yourhandle"*

## Manual CLI Usage

```bash
# One-time dependency install
npm install --prefix skills/orbit-cards/scripts --no-audit --no-fund

# Follower mosaic thank-you photo (any custom text or milestone number)
node skills/orbit-cards/scripts/orbit-cards.mjs render --handle @yourhandle \
  --card thanks-mosaic --text "2000" --scale 2 --out ./thanks-2000.png

node skills/orbit-cards/scripts/orbit-cards.mjs render --handle @yourhandle \
  --card thanks-mosaic --text "THANK YOU" --scale 2 --out ./thank-you.png

# Starter pack (2 headers + orbit + recap + shout-out + ring)
node skills/orbit-cards/scripts/orbit-cards.mjs render --handle @yourhandle --pack --out ./cards

# Specific designs
node skills/orbit-cards/scripts/orbit-cards.mjs render --handle @yourhandle \
  --card header-mosaic --card header-spectrum --card header-polaroids \
  --out ./headers

# List all 265 designs
node skills/orbit-cards/scripts/orbit-cards.mjs list
```

See [skills/orbit-cards/SKILL.md](./skills/orbit-cards/SKILL.md) and [skills/orbit-cards/references/designs.md](./skills/orbit-cards/references/designs.md) for the full catalog and options.

Built by [Orbit Cards](https://orbitcards.app).
