---
name: design-inspiration
description: >
  Find real-world design inspiration for websites, apps, and UI patterns. Searches and
  curates 5-8 examples with "steal this" notes and cross-cutting pattern analysis, then
  generates a dark-themed gallery page with desktop + mobile screenshots. Use when looking
  for design references for a pattern you're building — pricing pages, dashboards, event
  cards, landing pages, navigation, portfolios.
---

# Design Inspiration Finder

## When This Applies

User wants real-world design references for something they're building. They describe a vibe, a UI pattern, a website category, or a functional requirement — and want to see how others have solved it.

Examples:
- "I need inspiration for event card designs"
- "Find me photography portfolio websites"
- "Show me examples of dark dashboard layouts"
- "How do other apps handle onboarding flows?"
- "I need design references for a pricing page"

## What To Do

Follow this 5-step workflow. Do all steps — the screenshots are what make this valuable.

### Step 1: Clarify the Ask

Make sure you understand what they want. If the request is vague ("I need inspiration"), ask:
- What are you building? (app type, website category)
- What specific part? (full page, specific component, layout pattern)
- Any aesthetic direction? (dark, minimal, playful, dense, editorial)

If the request is specific enough ("event card designs"), skip straight to Step 2.

### Step 2: Search (3 parallel queries)

Run three WebSearch queries in parallel to cast a wide net:

1. **Curated roundup:** `"best [topic] design examples 2025 2026"` or `"best [topic] website design inspiration"`
2. **Pattern-specific:** `"[topic] UI design patterns"` or `"[topic] component design"`
3. **Gallery-scoped:** `"site:mobbin.com [topic]"` OR `"site:dribbble.com [topic]"` OR `"[topic] awwwards"` (pick whichever gallery fits the ask — Mobbin for app UI, Dribbble for visual design, Awwwards for websites)

### Step 3: Extract and Curate

WebFetch the top 2-3 search results (the roundup articles) to extract actual site names and URLs.

Then curate down to **5-8 examples** by:
- Deduplicating across sources
- Filtering for relevance (a search for "event cards" might return event *platform* homepages — you want the card UI)
- Preferring real shipped products over Dribbble mockups
- Preferring variety (don't return 5 sites that all look the same)

### Step 4: Screenshot Each Site

Run the screenshot script to capture each site at desktop and mobile viewports:

```bash
node /Users/tinkerbox/TinkerBot/.claude/skills/design-inspiration/scripts/screenshot-sites.js \
  --topic "[topic-slug]" \
  --urls "https://site1.com,https://site2.com,https://site3.com"
```

This saves all screenshots to a single flat folder: `~/Downloads/design-inspo-[topic]-[date]/`. Filenames include the viewport: `01-site-name-desktop.png`, `01-site-name-mobile.png`.

**Options:**
- `--wait [ms]` — Base wait time after page load (default: 4000ms). The script auto-detects canvas/WebGL elements and extends the wait to 8s+ for those sites. For lists with known heavy sites (3D portfolios, WebGL experiences, Three.js), use `--wait 12000`.

**After screenshots are taken, you MUST visually verify each one** by reading the screenshot files with the Read tool. Common problems to check for:
- **Loading screens** — spinners, progress bars, "loading..." text, blank pages with a single element. These indicate the site hadn't finished loading.
- **Cookie/consent banners** — overlays covering the actual content.
- **Newsletter/promo popups** — modal dialogs blocking the view.
- **Blank/white pages** — the site may require JavaScript interaction (click-to-enter) or longer load times.

**If any screenshots are bad**, retake just the failed sites with `--wait 12000` or higher. Don't present loading screens as inspiration — that's useless to the user. Iterate until every screenshot shows real site content.

**If the script fails** (Playwright not installed, sites block automation), fall back to providing URLs without screenshots. Don't let screenshot failures block the whole workflow.

### Step 5: Generate Interactive Gallery

Create a JSON data file and use the gallery generator to build an interactive HTML page:

**1. Write the data file** to the output directory as `sites.json`:

```json
{
  "topic": "Design Inspiration: [Topic]",
  "brief": "Context about what the user is building and what we're looking for",
  "sites": [
    {
      "name": "Site Name",
      "url": "https://example.com",
      "why": "Why this site is relevant to the user's ask",
      "steal": "Specific actionable design pattern to borrow",
      "screenshots": ["01-site-name-desktop.png", "01-site-name-mobile.png"],
      "tags": ["interactive", "minimal", "dark"]
    }
  ],
  "patterns": [
    "Cross-cutting pattern observed across examples",
    "Another pattern"
  ]
}
```

**Tags** should capture the design approach (e.g. "minimal", "dark", "editorial", "interactive", "playful", "dense"). Use 2-3 tags per site. These become filterable in the gallery.

**Patterns** should cover:
- What do the best examples have in common?
- What layout/color/typography patterns recur?
- What's the dominant approach vs interesting outliers?

**2. Generate the gallery:**

```bash
node /Users/tinkerbox/TinkerBot/.claude/skills/design-inspiration/scripts/generate-gallery.js \
  --dir ~/Downloads/design-inspo-[topic]-[date] \
  --data ~/Downloads/design-inspo-[topic]-[date]/sites.json
```

**3. Open in browser:**

```bash
open ~/Downloads/design-inspo-[topic]-[date]/gallery.html
```

The gallery provides:
- Dark-themed card layout with all sites
- Click any screenshot to view full-size (lightbox)
- Filter by tags
- Links to live sites
- Why-it's-relevant and steal-this notes per site
- Cross-cutting patterns section

### Step 6: Brief Summary in Chat

After opening the gallery, give a brief summary in chat (2-3 sentences). Don't repeat everything that's in the gallery — the user has the visual reference now. Just highlight the 1-2 most relevant examples and any key insight.

## What NOT To Do

- Don't return 15+ links with no analysis — 5-8 curated examples with insight beats a dump of URLs
- Don't return only Dribbble shots — those are concept mockups, not shipped products. Mix in real sites
- Don't skip screenshots — URLs alone require the user to open each one manually. The visual output is the whole point
- Don't over-describe obvious things — "uses a grid layout" isn't helpful. "Uses a 3-column card grid that collapses to single-column on mobile, with generous 24px gaps that prevent the dense content from feeling cramped" is helpful
- Don't present AI-generated designs as inspiration — the user wants real-world references
