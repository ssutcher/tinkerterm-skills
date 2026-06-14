---
name: ui-verify
description: >
  Visual verification for Figma → HTML/CSS/React work. Use after making any
  visual or UI change. Enforces checking code against the Figma spec AND
  screenshots against the design, across both viewports, before declaring done.
  Pairs with ui-build.
---

# UI Verify Skill

## Purpose

Enforce visual self-verification after UI changes. The AI must look at what it built — not punt to the user. Prevents the pattern of making CSS changes and saying "refresh and check."

## Source of truth

**Figma JSON is what you verify code against. Screenshots are evidence that your render matches what you intended to build.** Never read values from a screenshot to figure out what the code "should" be — that's how design bugs get rubber-stamped as "matches." Code-vs-JSON is the authoritative check; screenshot-vs-Figma-PNG is the sanity check on top.

## When to Invoke

Automatically trigger:

- **After making any visual/UI change** (CSS, layout, component styling)
- **Before presenting UI work to the user**
- **Before saying "refresh the page"** or "check if it looks right"

## The Workflow

### 1. Check Code Against Figma Specs

Compare the values in your code against the Figma JSON data.

- Re-read the Figma JSON (`~/.tterm/figma-selection.json` or `~/.tterm/figma-exports/figma-*/selection.json`)
- Verify every value: sizes, colors, fonts, weights, spacing, gaps, borders, radius
- Don't skip "close enough" — if Figma says 44px and you wrote 28px, that's wrong
- Check layout properties too: flex direction, alignment, justify, overflow

### 2. Screenshot the Page

Take a screenshot of the actual running page.

**Playwright (preferred — can control viewport):**
```bash
cd r2 && npx playwright screenshot --viewport-size=1280,720 http://localhost:3000/path /Users/tinkerbox/TinkerBot/scrap/screenshots/r2-verify-desktop.png
npx playwright screenshot --viewport-size=390,844 http://localhost:3000/path /Users/tinkerbox/TinkerBot/scrap/screenshots/r2-verify-mobile.png
```

**macOS screencapture (fallback):**
```bash
screencapture -x /Users/tinkerbox/TinkerBot/scrap/screenshots/r2-verify.png
```

### 3. Read and Compare Visually

Use the Read tool on the screenshot (you're multimodal — use it).

- Does it match what you expect based on the code you wrote?
- Compare against the Figma PNG exports if available (in `~/.tterm/figma-exports/figma-*/` or exported assets)

**Visual comparison checklist:**
- Colors match exactly (compare hex values)
- Dimensions match (within 1px)
- Spacing and gaps correct
- Typography correct (family, size, weight, line-height)
- Layout and alignment right
- No clipping, overflow, or misalignment

**States:**
- Hover state works
- Active/pressed state works
- Disabled state (if applicable)
- Loading state (if applicable)
- Error state (if applicable)
- Focus state (keyboard navigation)

**Edge cases:**
- Empty state renders correctly
- Long/max content doesn't break layout
- Single item vs many items
- Responsive behavior between breakpoints

### 4. Both Viewports

Every time. Not just desktop.

- Screenshot at desktop width (1280 or 1440)
- Screenshot at mobile width (390)
- Compare each against the corresponding Figma frame
- If something looks wrong at either size, fix it before moving on

### 5. Fix and Re-screenshot

If anything doesn't match:

1. Fix the code
2. Take a new screenshot
3. Compare again
4. Repeat until it matches

Do not present work to the user until it visually matches the design.

### 6. Present With Evidence

When showing the user:

```
✅ "Here's the desktop view [screenshot]. Matches the Figma spec — 44px avatars,
    1.5px tan border, 12px gap, Bricolage Grotesque 36px title. Mobile also
    verified [screenshot]."
```

Not:

```
❌ "Refresh the page — the member strip should appear at the bottom."
❌ "I made the CSS changes. Can you check if it looks right?"
```

## Common Violations

### Not looking at all
```
❌ Making 5 CSS changes without ever screenshotting
❌ Adding console.log debug lines instead of looking at the page
```

### Checking one viewport only
```
❌ "Looks good on desktop. Let me know about mobile."
✅ Screenshot both, verify both, present both.
```

### Punting to the user
```
❌ "Refresh and check — it should work now."
✅ "I screenshotted and verified. Here's what it looks like. Desktop and mobile both match the Figma design."
```

### Comparing screenshot to specs instead of design
```
❌ "The screenshot shows 44px avatars so it matches the JSON."
✅ "The code uses 44px matching the JSON spec. The screenshot looks right — avatar sizes, spacing, and layout match the Figma PNG."
```
