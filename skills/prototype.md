---
name: prototype
description: >
  ALWAYS load before building HTML prototypes. Contains generation rules
  that prevent common AI quality issues (generic layouts, slop patterns).
  Activate when the user asks to prototype, mockup, wireframe, or build
  an HTML page, demo, or UI exploration.
---

## Before You Generate

Capture a brief from the user before writing any HTML. You need three things:

1. **What it is** — Dashboard? Landing page? Settings screen? Multi-page flow?
2. **Who it's for** — Internal tool? Client presentation? User-facing product?
3. **Visual direction** — Brand colors? Dark/light? Minimal/dense? Reference site?

If the user gave enough context in their request, don't ask — just build. If the direction is ambiguous, ask one focused question, not three.

## Generation Rules

**Structure:**
- Self-contained HTML. All CSS in a `<style>` block in `<head>`.
- Tailwind CDN via `<script src="https://cdn.tailwindcss.com"></script>` for utility classes. Use Tailwind for layout and spacing; use the `<style>` block for component-specific styles and custom properties.
- Design tokens as CSS custom properties at the top of `<style>`:
  ```css
  :root {
    --color-primary: #002136;
    --color-surface: #F0F1F3;
    --color-text: #1a1a1a;
    --font-body: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
    --radius: 8px;
  }
  ```
- Always include `<meta name="viewport" content="width=device-width, initial-scale=1.0">`.

**Content:**
- Use real, plausible content — names, dates, numbers, copy. Never lorem ipsum.
- If the prototype is for a known brand/project, match their voice and terminology.
- Navigation, headers, and footers should feel complete, not placeholder.

**Anti-slop — avoid these AI defaults:**
- No centered-everything layouts. Use left-aligned text, asymmetric grids, real page structure.
- No purple/blue gradients as hero backgrounds. Pick colors that match the brief.
- No uniform border-radius on everything. Vary it — sharp cards, rounded buttons, pill badges.
- No Inter font by default. Use the system font stack or the brand's font.
- No "Welcome to [Product]" hero sections with a single centered CTA. Build the actual UI.
- No grey-on-white low-contrast placeholder text.

**Multi-page prototypes:**
- Use relative links between pages (`<a href="about.html">`).
- Share navigation structure across pages — copy the nav HTML, don't reference external files.
- Each page is a separate file.

## Workflow

1. Capture brief (or infer from context).
2. Generate the HTML.
3. Save the file(s) and show them to the user.
4. When iterating, update the specific file(s) that changed.

## What Not To Do

- Don't create a build step, package.json, or config files. It's just HTML.
- Don't use external CSS files. Everything in one `<style>` block per page.
- Don't over-explain what you're building. Generate and show — the browser is the explanation.
