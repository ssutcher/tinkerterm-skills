---
name: ui-build
description: >
  Figma → HTML/CSS/React implementation workflow. Use when translating a Figma
  design into working code — building components, styling, implementing from a
  spec. Enforces the right order: read the design spec first, then map to design
  tokens, then build. Pairs with ui-verify for visual checking after the build.
---

# UI Build Skill

## Purpose

Enforce the correct workflow for implementing UI: start from the design spec, map to existing tokens and components, then build. Prevents the common pattern of coding first and eyeballing later.

## When to Invoke

Automatically trigger when:

- **Starting work on a UI component or visual change**
- **Implementing a design from Figma**
- **Making CSS/styling changes** to existing components
- **Building new components** that have a design reference

## The Workflow

### 0. Asset Inventory (GATE — must complete before coding)

Before writing any code, audit every visual asset in the design.

**Scan the Figma spec for:**
- **Icons** — every icon instance (navigation, actions, status indicators, decorative)
- **Illustrations** — hero images, empty state graphics, decorative artwork
- **Photos/imagery** — profile pictures, product images, backgrounds
- **Logos** — brand marks, partner logos, third-party badges

**For each asset, check:**
- Do I have the actual SVG/PNG/image file? (Check `public/`, `src/assets/`, project asset directories)
- Is it available in the Figma export data?
- Or is it missing entirely?

**If ANY asset is missing — STOP and ask the user.**

```
❌ NEVER do this:
   "I'll use a placeholder icon for now..."
   "I'll add a generic avatar circle..."
   <div className="w-6 h-6 bg-gray-300 rounded" /> {/* placeholder */}

✅ ALWAYS do this:
   "I found 3 icons in this design that I don't have:
    - Search icon (magnifying glass in the header)
    - Notification bell (top-right corner)
    - Chevron-right (in each list row)

    Can you provide the SVGs, or should I use a specific icon library?"
```

**This gate is NON-NEGOTIABLE.** A placeholder icon or stock image is never "close enough" — it's a missing asset that the user will have to catch and fix later. Surface it now.

### 1. Parse Figma Specs First

Before writing any code, extract exact values from the Figma export.

**Figma JSON is the source of truth for implementation. PNGs are visual reference only.**

- Read `~/.tterm/figma-selection.json` or `~/.tterm/figma-exports/figma-*/selection.json`
- Extract exact values: sizes (px), colors (rgba/hex), font families, font weights, font sizes, line heights, spacing, gaps, border radius, border widths
- Parse the JSON programmatically — don't eyeball PNGs for pixel values
- **Walk `children[]` recursively. Instance overrides on color and text live in `children[].fills[]` and `children[].characters`, NOT in `componentProperties.Variant`.** A Dark Mode variant can keep `Variant="Half"` while its text child is overridden to white via the child's `fills[]`. Reading `componentProperties` alone misses these; only walking rendered children catches them.
- Note the component hierarchy and layout (flex direction, alignment, justify)

### 2. Map to Design Tokens

Before hardcoding any value, check if a token already exists.

- Read `src/styles/tokens.css` (or project equivalent)
- Read `src/styles/CLAUDE.md` for the token reference
- Map Figma values to existing tokens (e.g., Figma says `#272727` → that's `--r2-color-black`)
- If a token exists for the value, use it. Never hardcode what a token covers.
- If no token exists and the value is reusable (appears in multiple places or fits the system), create one
- Only use a raw value if it's truly one-off

### 3. Check Component Library

Before building anything new, check if it already exists.

- Read `src/components/ui/CLAUDE.md` for the component registry
- Search for similar components (`Glob` for the component name)
- If it exists, use it or extend it. Don't rebuild.
- If it doesn't exist, create one — especially if it'll be used in multiple places or represents a distinct UI pattern

### 4. Build Both Viewports Together

Don't build desktop first and retrofit mobile later.

- Check Figma for both desktop and mobile frames
- Implement responsive behavior from the start
- Use the breakpoints defined in the design system
- If Figma only shows one viewport, ask about the other before building

### 4.5 Source Data Missing? Leave It Blank.

**No judgment calls. No scope creep. No filling in gaps from PNGs.**

If the Figma JSON has the CSS for a node, you build it pixel perfect from that data.

If the JSON does NOT have CSS for a node — variant has `_error`, the node was never resolved, the component-set didn't expose its children — you do NOT:

- Eyeball the PNG and infer values
- Reuse "similar" values from other variants
- Make up "reasonable" defaults
- Use a placeholder

You DO:

- Leave the variant blank (catalog renders "no source data")
- Add it to a "needs re-export" list in your findings
- Tell the user explicitly when reporting

**Why:** an inferred value looks done but isn't. The user discovers the discrepancy later when comparing against the real design. The cost of "I'll just make it look about right" is trust. A blank variant is honest; a fake variant is technical debt with a smile painted on it.

```
❌ "I don't see CSS for the disabled state, but I'll grey it out — looks roughly right."
✅ "Disabled state has no CSS in the JSON (component-set _error). Catalog shows it as blank with a 'needs re-export' note. Listed in findings."
```

### 5. Handle Content Edge Cases

Don't just build the happy path.

- **Empty states** — what shows when there's no data?
- **Overflow** — what happens with long text, many items?
- **Single vs many** — does it work with 1 item and 50 items?
- **Loading** — what shows while data is fetching?

### 6. Pixel-Perfect Self-Check (GATE — must complete before reporting done)

After implementation, you MUST verify your own work before telling the user it's done. Do not rely on the user to catch visual discrepancies.

**The process:**

1. **Screenshot what you built** — use Playwright or the browser automation tool to capture the actual rendered output at the correct viewport(s)
2. **Compare against the Figma spec** — go value by value:
   - Colors: exact hex/rgba match (not "close enough")
   - Spacing/gaps: exact pixel values from Figma JSON
   - Font sizes, weights, line heights: exact match
   - Border radius, border widths: exact match
   - Layout: flex direction, alignment, justify — match the Figma hierarchy
   - Element dimensions: width, height constraints
3. **Fix discrepancies** — if anything doesn't match, fix it before reporting
4. **Re-screenshot after fixes** — confirm the fix actually worked
5. **Present evidence** — when reporting done, show what you verified:
   ```
   ✅ Verified against Figma:
   - Header height: 56px ✓
   - Card gap: 16px ✓
   - Avatar size: 44px with 1.5px border ✓
   - Font: Inter 14px/500 for body text ✓
   - Colors: all mapped to design tokens ✓
   ```

**If you can't screenshot** (no dev server, no browser tool), explicitly say so:
```
"I've matched all values from the Figma JSON but I couldn't visually verify —
 the dev server isn't running. Want me to start it and verify?"
```

**NEVER say "done" or "implemented" without either visual verification or an explicit disclaimer that you haven't verified yet.**

## Common Violations

### Coding before reading the spec
```
❌ "Let me add a flex container with some spacing..."
✅ "Figma JSON shows: flex, gap: 12px, align-items: center, height: 44px. Let me implement those exact values."
```

### Eyeballing PNGs for values
```
❌ "The avatars look like about 36-40px..."
✅ "Figma JSON: ELLIPSE 44x44, border: 1.5px solid #F6F1EC"
```

### Hardcoding token values
```
❌ color: '#272727'
✅ color: 'var(--r2-color-black, #272727)'
```

### Building desktop only
```
❌ "Refresh and check — I'll do mobile later."
✅ "I've checked both the desktop and mobile Figma frames. Here's how they differ..."
```

### Using placeholder assets
```
❌ "I'll use a generic icon for now, you can replace it later."
❌ <div className="w-8 h-8 bg-gray-200 rounded-full" />
✅ "The design has 4 icons I don't have SVGs for: [list]. Can you provide them?"
```

### Saying "done" without verifying
```
❌ "I've implemented the design. Take a look!"
❌ "Done — let me know if anything needs adjusting."
✅ "I've verified against the Figma spec: [checklist]. Here's a screenshot comparison."
✅ "Implementation complete but I couldn't visually verify — dev server isn't running. Want me to start it?"
```
