---
name: design-inspiration
description: >
  Find real-world design inspiration for websites, apps, and UI patterns. Searches,
  curates, and analyzes 5-8 examples with actionable "steal this" notes and cross-cutting
  pattern analysis. Generates an interactive dark-themed gallery HTML page with tag
  filtering and lightbox. Use when the user wants examples of how other sites handle a
  specific design problem — landing pages, dashboards, portfolios, event cards, pricing
  pages, navigation patterns, brand experiences, etc. Triggers on "inspiration", "inspo",
  "examples of", "show me sites", "how do other apps handle", "design reference",
  "find me websites like", "design inspiration for".
---

# Design Inspiration Finder

## When This Applies

User wants real-world design references for something they're building. They describe
a vibe, a UI pattern, a website category, or a functional requirement — and want to
see how others have solved it.

Examples:
- "I need inspiration for event card designs"
- "Find me photography portfolio websites"
- "Show me examples of dark dashboard layouts"
- "How do other apps handle onboarding flows?"
- "I need design references for a pricing page"
- "Brand experience inspiration for [project]"

## Workflow

Follow steps 1-6 in order. The curated analysis is what makes this valuable — not a
dump of links.

### Step 1: Clarify the Ask

If the request is vague ("I need inspiration"), ask:
- What are you building? (app type, website category)
- What specific part? (full page, specific component, layout pattern)
- Any aesthetic direction? (dark, minimal, playful, dense, editorial)

If the request is specific enough ("event card designs"), skip to Step 2.

### Step 2: Search (3 parallel queries)

Run three web searches in parallel to cast a wide net:

1. **Curated roundup:** `"best [topic] design examples 2025 2026"` or `"best [topic] website design inspiration"`
2. **Pattern-specific:** `"[topic] UI design patterns"` or `"[topic] component design"`
3. **Gallery-scoped:** Pick the gallery that fits — `"site:mobbin.com [topic]"` for app UI, `"site:dribbble.com [topic]"` for visual design, `"[topic] awwwards"` for websites

### Step 3: Extract and Curate

Fetch the top 2-3 roundup articles to extract actual site names and URLs.

Curate down to **5-8 examples** by:
- Deduplicating across sources
- Filtering for relevance (a search for "event cards" might return event platform homepages — you want the card UI)
- Preferring real shipped products over Dribbble mockups
- Preferring variety (don't return 5 sites that all look the same)

For each site, write:
- **Why it's relevant** — what makes this example useful for the user's specific ask
- **Steal this** — one specific, actionable design pattern worth borrowing. Be precise: "Uses a 3-column card grid that collapses to single-column on mobile, with generous 24px gaps" is helpful. "Uses a grid layout" is not.
- **Tags** — 2-3 words capturing the design approach (minimal, dark, editorial, interactive, playful, dense)

Also identify **cross-cutting patterns** — what do the best examples have in common? What layout/color/typography patterns recur? What's the dominant approach vs interesting outliers?

### Step 4: Screenshots (if Playwright available)

**Detection:** Run `npx playwright --version` to check if Playwright is installed. If it fails or is not found, skip this step entirely — the gallery will still work with metadata-only cards.

**If Playwright is available**, capture desktop and mobile screenshots for each curated site:

1. Write a small Node.js script to the output directory (`~/Downloads/design-inspo-[topic]-[date]/capture.js`) that:
   - Launches Chromium via Playwright
   - For each site URL, captures two screenshots:
     - **Desktop:** 1440×900 viewport → `01-site-name-desktop.png`
     - **Mobile:** 390×844 viewport with iPhone UA string → `01-site-name-mobile.png`
   - Waits for `networkidle` plus a base delay (4000ms default, 8000ms+ if `<canvas>` elements detected)
   - Dismisses cookie banners and popups between captures using common selectors:
     - Cookie/consent: buttons matching "Accept All", "Accept Cookies", "Got it", `[class*="cookie"] button`
     - Promo/newsletter: modal close buttons, "No thanks", "Maybe later", SVG close icons
     - Runs dismissal up to 3 rounds to catch cascading popups

2. Run the script: `node ~/Downloads/design-inspo-[topic]-[date]/capture.js`

3. Verify each screenshot by reading the PNG files. Retake any that show:
   - Loading spinners or blank pages
   - Cookie banners still visible
   - Popups blocking content
   - For failed captures, retry with `--wait 12000` or try an alternate URL

4. Add `screenshots` field to each site in `sites.json`:
   ```json
   "screenshots": ["01-site-name-desktop.png", "01-site-name-mobile.png"]
   ```

**If Playwright is NOT available**, skip this step. The `screenshots` field will be absent from `sites.json` and the gallery renders metadata-only cards (still fully functional).

### Step 5: Generate Interactive Gallery

Create a self-contained HTML gallery page. Write a `sites.json` data file first (if not already written in Step 4), then generate the gallery HTML.

**Data file format** (`sites.json`):

```json
{
  "topic": "Design Inspiration: [Topic]",
  "brief": "Context about what the user is building",
  "sites": [
    {
      "name": "Site Name",
      "url": "https://example.com",
      "why": "Why this site is relevant",
      "steal": "Specific actionable design pattern to borrow",
      "screenshots": ["01-site-name-desktop.png", "01-site-name-mobile.png"],
      "tags": ["interactive", "minimal", "dark"]
    }
  ],
  "patterns": [
    "Cross-cutting pattern observed across examples"
  ]
}
```

Note: The `screenshots` field is optional. If Step 4 was skipped (no Playwright), omit it.

**Gallery HTML:** Generate a complete, self-contained HTML file with:
- Dark theme (#0a0a0a background, #e0e0e0 text)
- Header with topic title, brief, and site count
- Filter bar with tag buttons (pill-shaped, toggle active state)
- Card per site: name (linked), URL, why-it's-relevant, steal-this, tags
- **If screenshots exist:** thumbnail strip per card with clickable lightbox (fullscreen overlay on click, close on Escape/click-outside)
- Cross-cutting patterns section at bottom
- Tag filtering via JavaScript (show/hide cards based on data-tags attribute)
- Responsive layout (single column on mobile)

Save to `~/Downloads/design-inspo-[topic]-[date]/gallery.html` and open in browser.

### Step 6: Brief Summary

After opening the gallery, give a 2-3 sentence summary in chat. Don't repeat everything — the gallery is the deliverable. Just highlight the 1-2 most relevant examples and any key insight.

## Rules

- **5-8 curated examples** — not 15+ links with no analysis
- **Real shipped products** over Dribbble mockups. Mix in real sites
- **Specific steal-this notes** — "uses a grid" is useless. Describe spacing, color, typography, interaction details
- **Cross-cutting patterns** are required — what do the best examples share?
- **Don't present AI-generated designs** as inspiration — users want real-world references
- **Gallery is the deliverable** — don't just list URLs in chat

## Gallery HTML Template

Use this structure for the generated gallery. Adapt the content but keep the dark-themed card layout, tag filtering, and responsive design:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>[Topic]</title>
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }
    body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; background: #0a0a0a; color: #e0e0e0; line-height: 1.6; }
    .header { padding: 48px 48px 32px; border-bottom: 1px solid #1a1a1a; }
    .header h1 { font-size: 32px; font-weight: 600; color: #fff; }
    .header .brief { margin-top: 12px; color: #888; font-size: 15px; max-width: 680px; }
    .filters { padding: 16px 48px; border-bottom: 1px solid #1a1a1a; display: flex; gap: 8px; flex-wrap: wrap; }
    .filter-btn { background: #1a1a1a; border: 1px solid #2a2a2a; color: #888; padding: 4px 12px; border-radius: 16px; font-size: 12px; cursor: pointer; }
    .filter-btn:hover { border-color: #444; color: #ccc; }
    .filter-btn.active { background: #fff; color: #000; border-color: #fff; }
    .content { padding: 32px 48px; }
    .site-card { background: #111; border: 1px solid #1a1a1a; border-radius: 12px; margin-bottom: 32px; overflow: hidden; }
    .site-card.hidden { display: none; }
    .site-header { padding: 24px 28px; }
    .site-info h2 { font-size: 20px; font-weight: 600; }
    .site-info h2 a { color: #fff; text-decoration: none; }
    .site-info h2 a:hover { color: #6eb5ff; }
    .site-url { font-size: 13px; color: #555; text-decoration: none; }
    .site-notes { padding: 24px 28px; display: grid; grid-template-columns: 1fr 1fr; gap: 24px; }
    .note h3 { font-size: 11px; text-transform: uppercase; letter-spacing: 1px; color: #555; margin-bottom: 6px; }
    .note p { font-size: 14px; color: #bbb; }
    .tags { padding: 0 28px 20px; display: flex; gap: 6px; flex-wrap: wrap; }
    .tag { font-size: 11px; color: #666; background: #1a1a1a; padding: 2px 10px; border-radius: 10px; }
    .patterns { background: #111; border: 1px solid #1a1a1a; border-radius: 12px; padding: 28px; margin-top: 16px; }
    .patterns h2 { font-size: 16px; font-weight: 600; color: #fff; margin-bottom: 16px; }
    .patterns li { padding: 8px 0; border-bottom: 1px solid #1a1a1a; font-size: 14px; color: #999; list-style: none; }
    @media (max-width: 768px) { .header, .content, .filters { padding-left: 20px; padding-right: 20px; } .site-notes { grid-template-columns: 1fr; } }
  </style>
</head>
<body>
  <!-- Header, filter buttons, site cards, patterns section -->
  <!-- Tag filtering: data-tags on .site-card, JS toggles .hidden class -->
</body>
</html>
```
