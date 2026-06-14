---
name: brand-brief
description: >
  Build a moodboard/brand brief page from moodboard app data and client reference images.
  Analyzes liked images by keyword, synthesizes brand directions, builds a shareable HTML
  deliverable (cover + directions + synthesis), and deploys to Vercel. Triggers on
  "build the brand brief", "brand directions", "moodboard page", "brand brief",
  "create a brand brief", "moodboard brief".
---

# Brand Brief Builder

Turn a client's moodboard session + reference images into a polished, shareable brand brief.
Output: a single-page HTML file with a cover, 4-6 named brand directions, and a synthesis/
recommendation section — deployed to a public Vercel URL.

## When To Invoke

- User says "build the brand brief", "brand directions page", "moodboard page"
- User drops a moodboard JSON file and asks for brand direction analysis
- User wants to synthesize client swipe data into a shareable deliverable

## What You Need

**Always:**
- Moodboard JSON file path (export from dave-moodboard app — usually in ~/Downloads/)

**Often:**
- Client reference images they've manually sent (HEICs, screenshots from their phone/desktop)
- These carry MORE signal than the swipe data — they're intentional, not reactive

**Optional:**
- Client name (for output filename + Vercel project name)
- Known context: what they do, what they want the brand to feel like, who their audience is

---

## The Workflow

### Step 1: Analyze the Moodboard JSON

The JSON is large (500KB+). Never read it directly — extract via inline Python.

**JSON structure:** Root keys are `liked`, `disliked`, `skipped`, `stats`. Each image entry has:
`imageId`, `imageUrl`, `thumbUrl`, `source`, `keyword`, `photographer`, `vote`, `timestamp`

```bash
python3 -c "
import json
from collections import Counter

data = json.load(open('/path/to/moodboard.json', 'rb'))
liked = data['liked']
disliked = data['disliked']
skipped = data.get('skipped', [])

total = len(liked) + len(disliked) + len(skipped)
print(f'Total: {total} | Liked: {len(liked)} | Disliked: {len(disliked)} | Skipped: {len(skipped)}')

# Keyword frequency for liked
kw_liked = Counter(i['keyword'] for i in liked)
kw_disliked = Counter(i['keyword'] for i in disliked)

print('\n=== KEYWORDS BY LIKE RATE ===')
all_kws = set(kw_liked) | set(kw_disliked)
kw_stats = []
for kw in all_kws:
    l = kw_liked.get(kw, 0)
    d = kw_disliked.get(kw, 0)
    total_kw = l + d
    if total_kw > 0:
        rate = l / total_kw
        kw_stats.append((rate, l, d, kw))
kw_stats.sort(reverse=True)
for rate, l, d, kw in kw_stats[:30]:
    bar = '█' * l + '░' * d
    print(f'  {rate:.0%} ({l}L/{d}D) {kw} {bar}')

# Source breakdown
print('\n=== SOURCES (liked vs disliked) ===')
src_liked = Counter(i['source'] for i in liked)
src_disliked = Counter(i['source'] for i in disliked)
for s in set(list(src_liked.keys()) + list(src_disliked.keys())):
    print(f'  {s}: {src_liked.get(s, 0)} liked / {src_disliked.get(s, 0)} disliked')
"
```

Then pull all liked images with URLs for building the HTML:

```bash
python3 -c "
import json
data = json.load(open('/path/to/moodboard.json', 'rb'))
for img in data['liked']:
    print(f\"{img['keyword']} | {img['source']} | {img['photographer']} | {img['imageUrl']}\")
"
```

**What to look for:**
- Keywords with high like rate on multiple appearances → strongest signal for directions
- Hard dislikes (0 likes, several dislikes) → equally useful, tells you what to avoid
- Pattern clusters: are there 3-4 keywords that feel like the same emotional territory?
- Source quality: if one stock library has much lower hit rate, the image pool is the problem

### Step 2: Analyze Client Reference Images

If the client sent personal reference images (phone photos, screenshots of brands they admire),
read them with the Read tool — it works on HEICs and PNGs visually.

Look for:
- **Color palette signals** — warm/cool, saturated/muted, dark/light
- **Typography territory** — serif/sans, editorial, handmade, geometric
- **Aesthetic mode** — minimal, editorial, organic, graphic, nostalgic, bold
- **What these have in common with the moodboard data** — and where they contradict it
- **The thing they can't articulate** — what the references have in common that they didn't name

### Step 3: Synthesize Brand Directions

Before writing any HTML, do this thinking in your head. Each direction needs to be:

- **A named territory** — evocative, not generic. "The Signal", "The Maker-Father", "The Witness", not "Direction A: Minimal"
- **A core tension** — what's interesting/unexpected about this direction for *this person*
- **3-5 anchor images** pulled from their liked set (real URLs from the JSON)
- **A color palette** — 3-4 hex values derived from the images, not invented
- **A voice sample** — 1-2 sentences in the actual tone this direction would use
- **An honest take** — where does this work, what's the trap, what makes their version different from generic

**Rules for good directions:**
- Name the thing they're actually doing, not the aesthetic category
- The best directions have a slightly surprising twist ("The Frame" = "a person who builds the container for other people's work")
- Dislikes are directional data too — if they rejected every "rock concert" image, the direction isn't "music lover", it's "intimate music"

### Step 4: Build the HTML

Output: `~/Downloads/[client]-brand-directions.html`

**Required structure — in this order:**

**1. Cover section** (full-viewport, dark background `#1a1a1a`)
- Eyebrow: client name + "Personal Brand"
- Large title (light weight + bold contrast): e.g., "Five\n**Directions**"
- 2-3 sentence framing: what they're looking at, what you want from them, how to react
- Metadata row: date, number of directions, prepared by

**2. Sticky nav bar**
- Links to each direction + synthesis
- Intersection observer active state
- Eyebrow with client name

**3. For each direction — chapter break + content section:**
- Chapter break: full-width divider (colored bar + direction number + name + rule line + ghost number)
- Content section: two-column grid
  - Left: direction number (huge, 120px+, light), concept name, voice sample, color palette swatches, honest take block
  - Right: moodboard image grid (CSS grid, `object-fit: cover`, 3-4 real images from their liked set)

**4. Synthesis section**
- Comparison table: all directions side-by-side (name, palette swatches, one-line voice, core tension)
- Your recommendation: where is the strongest signal and why
- What you'd want to explore next if they want to go deeper

**Design language:**
```
Background: #f5f0e8 (warm parchment — editorial, not clinical)
Cover: #1a1a1a
Font: -apple-system, BlinkMacSystemFont, 'Helvetica Neue', Arial (system stack)
Type scale: 300/800 weight contrast, tight letter-spacing (-.03em for display)
Direction numbers: 120px+, font-weight 200 — graphic element, not label
Each direction: one accent color from its palette
Image grid: 2-3 columns, aspect-ratio 4/3, object-fit cover, no borders
Honest take block: subtle background, left border in accent color
```

### Step 5: Preview and Refine

```bash
open ~/Downloads/[client]-brand-directions.html
```

Check: cover frames the brief correctly, nav active state works as you scroll, images load,
honest takes are sharp not generic, synthesis recommendation is specific enough to push back on.

### Step 6: Deploy to Vercel

```bash
mkdir -p /Users/tinkerbox/TinkerBot/scrap/workspace/[client]-brand-deploy
cp ~/Downloads/[client]-brand-directions.html /Users/tinkerbox/TinkerBot/scrap/workspace/[client]-brand-deploy/index.html
cd /Users/tinkerbox/TinkerBot/scrap/workspace/[client]-brand-deploy && vercel --prod --yes
```

The production URL follows the pattern `https://[project-name].vercel.app`. Give the user that URL.

If the URL is behind Vercel's Deployment Protection, tell the user: Vercel Dashboard → project →
Settings → Deployment Protection → set to "Only Preview Deployments" or disable entirely.

---

## The Honest Take Pattern

This is the highest-value part of the brief. It shows strategic thinking, not just aesthetic assembly.
Every direction section must end with one.

**Structure:**
- What works — the specific thing about *this person's* version of the direction
- The risk — what the generic version of this looks like (the trap)
- The key — what makes their version different from the generic trap

**Example from Dave's brief:**
*"This is the most visually appealing direction and the most dangerous. The risk is looking like
every 'aesthetic' Instagram account from 2023. The only way it works for Dave is if it's anchored
to his specific objects in his specific places — his mug, his notebook in the garden, his daughter's
broken mug handle in his jacket pocket. Generic Anderson is a trap. Dave's Anderson is something else."*

The honest take should make the client feel like you've actually thought about them, not just assembled a mood.

---

## Quality Checks

**Directions:** 4-6 is the sweet spot. More than 6 and the client is overwhelmed. Fewer than 4 and you haven't shown enough range.

**Naming:** If any direction name is a generic aesthetic label ("Minimal", "Bold", "Earthy"), rename it to something that names what the person is *doing* or *being*, not what the design looks like.

**Images:** Use `imageUrl` (not `thumbUrl`) for full resolution in the HTML. Pixabay thumbs end in `_150.jpg` — the full res is usually the same URL without that suffix.

**The synthesis rec:** Must be specific enough that the client can push back on it. "We think Direction 1 is the strongest because..." not "All directions are valid options."

**The cover:** If it reads like a document header, it's wrong. Add a sentence from you (the strategist) about what you learned from their data and what question you're trying to answer together.
