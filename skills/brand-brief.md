---
name: brand-brief
description: >
  Generate a brand brief through structured collaborative process. Builds a complete
  brand identity document: Onliness Statement (swap-tested), North Star, IS/IS NOT,
  audience definition, founding insight, enemy, values through constraint, voice spec
  with "This NOT That" pairs, visual direction, naming territory, AI-readable layer,
  and brand card. Works standalone or as downstream from business-strategy (receives
  Onliness Statement and Brand Brief Handoff block).
  Triggers on: "build a brand brief", "create a brand brief", "let's do brand",
  "brand identity", "define the brand", "brand strategy", "brand voice", "brand brief
  for [product]", "what should the brand sound like", /brand-brief.
---

# Brand Brief Skill

## What This Is

A structured, collaborative brand brief builder. The output is a complete brand identity
document — not a mood board, not a logo exploration, not a tagline brainstorm. It's the
strategic foundation that every downstream brand decision (naming, visual design, copy,
campaigns, packaging) references as source of truth.

The AI drives the process section by section. The founder provides raw material, reacts
to drafts, and shapes the voice. Brand is collaborative by nature — AI can research and
structure, but only the founder knows what feels right.

**Distinct from business-strategy:** Strategy answers "what's the bet?" Brand brief
answers "what does the bet sound like, look like, and feel like to the people we're
building for?" Don't run brand-brief before the strategic fundamentals are settled.

**Inputs from business-strategy:** If a Strategic Memo exists with a Brand Brief Handoff
block (Onliness Statement, Category, JTBD, Founding Insight, Why Now, The Enemy), load
it. This skill doesn't re-derive the Core Bet — it builds the brand layer on top.


## When to Invoke

- Building or formalizing brand identity for a product or company
- After business-strategy when positioning is settled and brand work is next
- When "what should this brand sound like?" is the open question
- When voice, tone, or visual direction needs to be codified
- Before naming work (brand-brief feeds brand-naming with naming territory inputs)
- Before design work (brand-brief feeds visual direction to designers)

## When NOT to Invoke

- Just writing marketing copy — the brand brief should already exist; reference it
- Quick tactical question about tone — just answer it using existing brief
- Logo or visual design execution — this produces direction, not deliverables
- The strategic bet isn't settled yet — run business-strategy first


## Auto-Trigger Behavior

When this skill auto-triggers, confirm scope before diving in:

> "Want me to build a full brand brief for this? I'll work through it section by
> section — positioning, voice, visual direction, the whole identity document. We'll
> collaborate on each piece. Takes a focused session."

If the user has a Strategic Memo with a Brand Brief Handoff block, acknowledge what
carries forward and what's new:

> "I see the strategic memo already has an Onliness Statement and enemy definition.
> I'll carry those forward and build the brand layer on top — voice, visual direction,
> values, the full brief. Ready?"

Wait for confirmation. If yes, proceed to Phase 1.


---

## The Process

```
INPUTS → SECTION-BY-SECTION BUILD → REVIEW → AI-READABLE LAYER → SAVE
```

This is not a linear waterfall. Sections inform each other. Voice work may reframe the
enemy. Visual direction may sharpen the IS/IS NOT. The AI works section by section but
flags when a later section changes something earlier.


---

## Phase 1: Gather Inputs

**Goal:** Understand what exists and what needs to be built.

**Check for prior strategy work:**
- Search for an existing Strategic Memo: `search_bits("strategic memo [product-name]")`
- Search for existing personas: `search_bits("persona [product-name]")`
- Search for existing GTM work: `search_bits("gtm [product-name]")`

**If Strategic Memo with Brand Brief Handoff exists:**
Carry forward: Onliness Statement, Category, JTBD (functional/emotional/social), Founding
Insight, Why Now, The Enemy. These are inputs, not immutable — brand work may refine them.

**If starting from scratch, collect from the founder (conversationally):**

1. **What is it?** — product/company, in 1-3 sentences
2. **Who is it for?** — push for specificity beyond demographics
3. **What's the competitive landscape?** — who else is in this space
4. **What's the founding insight?** — the thing you know that the market hasn't figured out
5. **What should it NOT feel like?** — often more revealing than what it should feel like
6. **Any existing brand material?** — prior copy, visual references, competitor examples
   they admire or despise

**AI behavior:**
- Ask 1-2 questions at a time, not a form
- Don't accept "everyone" as a customer — push for the specific person
- Pay attention to the founder's own language — how they naturally describe the product
  is often the right voice


---

## Phase 2: Build the Brief (Section by Section)

The brand brief has 13 sections. AI drafts each one, presents it, founder reacts, AI
refines. Don't dump all 13 at once — work in groups of 2-3, check in, then continue.

**Pacing:** Present sections in batches. After each batch, ask: "How does this land?
What would you change?" Don't proceed until the founder has reacted.

---

### The 13 Sections

**Section 1: ONLINESS STATEMENT**

Format: "[Brand] is the only [category] that [differentiated benefit] for [specific
customer] who [specific context]."

**Validation tests (all three must pass):**
- **Swap test:** Replace the brand name with each major competitor. If the statement
  still works, the differentiation isn't real. Run this explicitly against 3-4 competitors.
- **Cessation test:** If the brand disappeared tomorrow, what would customers grieve?
  The answer must be specific enough that no competitor fills the gap.
- **Durability:** Can a competitor copy this combined position in 30 days? If yes,
  it's not differentiated enough.

If the Strategic Memo already has a swap-tested Onliness Statement, carry it forward.
Only rewrite if brand work surfaces a sharper framing.

---

**Section 2: NORTH STAR**

One sentence. The thing the company exists to make true in the world. Not a mission
statement — those are corporate. This is the internal compass.

Format: "[Verb] [for whom] [what outcome]."

---

**Section 3: IS / IS NOT**

Two columns. 5-7 items each. These are brand-level constraints, not product features.

**IS** items should be specific enough that they're actual constraints on decisions.
"Consumer-grade" means something. "Quality" means nothing.

**IS NOT** items should name the specific failure modes and adjacent-but-wrong territories
the brand must avoid. These are often more useful than the IS column.

---

**Section 4: FOR (THE HUMAN)**

Not demographics. Specific humans with specific situations, anxieties, and buying
contexts. If personas exist from business-strategy, reference them by name.

**Structure:**
- Primary audience (brand destination) — the person you're building toward
- Secondary audience (if applicable) — a different buying context or use case
- Beachhead audience (brand entry point) — who adopts first and creates social proof
- Not for — explicit exclusions. Who the brand is NOT trying to reach.

Each audience description should include: what they've already done (behavioral signal),
what they're anxious about, and how they'll find the product.

---

**Section 5: FOUNDING INSIGHT**

The thing the founders know that the market hasn't figured out yet. Not a feature — a
structural observation about why the current state of things is broken and why the timing
is right to fix it.

This should make the reader think "oh, obviously" — but it wasn't obvious until someone
said it.

---

**Section 6: THE ENEMY**

The enemy is never a competitor. It's a worldview, an assumption, or a structural condition
that the brand exists to fight.

**Structure:**
- The enemy statement (one sentence, bold)
- How the enemy manifests in specific competitors or market conditions (2-4 examples)
- What we're NOT fighting (explicit — avoids alienating adjacent communities)

---

**Section 7: VALUES REVEALED THROUGH CONSTRAINT**

Not aspirational values. Decisions the company has made or will make that cost something.
Each value should name: the constraint, what it forecloses (the revenue or opportunity
sacrificed), and why the company holds it anyway.

Format for each value:
- **The constraint** (bold, declarative)
- What it costs / what it forecloses
- Why we hold it anyway

5-6 values is the sweet spot. If a "value" doesn't cost the company anything, it's not
a value — it's a default. Cut it.

---

**Section 8: VOICE**

The most operationally useful section of the brief. Every person who writes copy for the
brand should be able to read this section and produce consistent output.

**Four subsections:**

**8a. Grammatical specification**
Specific, enforceable rules:
- Sentence length target (e.g., "<=8 words average")
- Contractions: yes or no
- Default POV (second person, first person plural, etc.)
- Numbers: numerals or spelled out
- Active vs passive voice
- Oxford comma
- Hedging language policy
- Opening sentence rules

**8b. Voice compass**
Four spectrums with position marked:
```
Formal  <---[X]---> Casual
Serious <---[X]---> Playful
Verbose <---[X]---> Terse
Technical <---[X]---> Human
```

**8c. "This NOT That" (5 pairs)**

The highest-leverage part of voice definition. Each pair shows the same message in the
right voice and the wrong voice. Drawn from actual copy if it exists, or written as
examples of key brand communications.

Format for each pair:
- Context label (what the message is about)
- YES: the sentence in the brand's actual voice
- NO: the same message written wrong — corporate, hedging, passive, or off-brand

The NO versions should be plausible — things a well-meaning copywriter might actually
write. That's what makes them useful.

**8d. Context by channel**
How the voice adapts across surfaces:
- Marketing headlines
- Onboarding / product copy
- Error messages
- Transactional email
- Community / social (founder voice vs brand voice)

**8e. Banned phrases**
Specific words and phrases the brand never uses. These should be the generic marketing
language that makes every brand sound the same.

---

**Section 9: NARRATIVE ANCHOR** (if applicable)

The emotional center of the brand's communication — a specific image, phrase, or moment
that all messaging orbits around. Not every brand has one. When one exists, it's the
most powerful single element in the brief.

**What makes a good narrative anchor:**
- Specific enough to visualize
- Emotional enough to feel
- Simple enough to repeat
- Connected to the product's actual moment of value

**What it means in practice:**
- How it shapes campaign language
- How it shapes product demos
- How it shapes the emotional register (e.g., "the antidote to anxiety, not another
  alarm bell")

---

**Section 10: VISUAL DIRECTION**

Not a design system — a strategic direction for visual identity. Enough for a designer
to start work; not so specific that it constrains execution.

**Structure:**
- Aesthetic mood (3-5 words)
- Visual NOT (specific failure modes to avoid — competitor aesthetics, adjacent-but-wrong
  territories)
- 3-4 references (existing brands, products, or design approaches that capture part of
  the territory, with WHY each resonates)
- "Aim for" list (5-7 specific visual attributes)

References should span different dimensions (typography, photography, interface design,
packaging) rather than all pointing at the same aesthetic.

---

**Section 11: NAMING TERRITORY**

Handoff block for brand-naming work. Contains the inputs the naming process needs:

- Emotional territory (3-4 words)
- Anti-territory (what naming must avoid)
- Category context (competitor names and why they're wrong/right)
- Cultural vocabulary (words the audience actually uses)
- Naming archetype (Evocative, Descriptive, Invented, etc.)
- Hard constraints (legal, phonetic, domain, cultural)

---

**Section 12: AI-READABLE LAYER**

A machine-parseable summary of the entire brief. One field per line, KEY: value format.
Any AI tool that needs to write in the brand's voice reads this section.

**Required fields:**
```
BRAND: [name]
NORTH_STAR: [north star statement]
ONLINESS: [onliness statement]
IS: [comma-separated IS items]
IS_NOT: [comma-separated IS NOT items]
FOR_PRIMARY: [primary audience, one sentence]
FOR_SECONDARY: [secondary audience, if applicable]
FOR_BEACHHEAD: [beachhead audience, if applicable]
ENEMY: [enemy statement]
NARRATIVE_ANCHOR: [anchor phrase and context, if applicable]
EMOTIONAL_REGISTER: [how the brand should make people feel]
VOICE_DO: [comma-separated voice rules]
VOICE_DONT: [comma-separated voice anti-patterns]
NEVER_SAY: [banned phrases, comma-separated]
SOUNDS_LIKE: [reference voices] — NOT [anti-reference voices]
NAMING_TERRITORY: [emotional territory] / NOT: [anti-territory]
VISUAL_REGISTER: [visual direction summary]
VISUAL_NOT: [visual anti-patterns]
```

**Why this exists:** Downstream AI tools (copy generators, chatbots, campaign builders)
can parse this section without reading the full brief. It's the brief's API.

---

**Section 13: BRAND CARD**

150-word orientation artifact. Written IN the brand's voice. A new team member reads
this and knows who the brand is in 60 seconds.

**Structure:**
- Onliness statement (bold, opening)
- North star (one sentence)
- For: (primary audience, one sentence)
- Is / Is Not (compressed)
- We're fighting: (enemy, one sentence)
- Narrative anchor (if applicable, compressed)
- Voice in 3 words
- One "This / Not That" pair
- Visual direction (one line)

The brand card is the swap test for the entire brief: if it doesn't feel like the brand,
something upstream is wrong.


---

## Phase 3: Review and Refine

After all 13 sections are drafted:

1. **Present the full brief** for review
2. **Run the swap test** on the Onliness Statement one more time
3. **Read the Brand Card aloud** — does it sound like the brand?
4. **Check internal consistency:**
   - Does the voice match the enemy? (fighting corporate complexity in corporate voice = broken)
   - Does the visual direction match the voice? (terse voice + decorative visuals = tension)
   - Do the "This NOT That" pairs actually demonstrate the voice rules?
   - Does the AI-readable layer accurately compress the full brief?
5. **Iterate** — AI names weak spots, asks targeted questions, pushes back when warranted


---

## Phase 4: Save

Save the completed brand brief as a bit:

`create_bit(type: note, project: [product-name], tags: brand-brief [product-name])`

**Content format:** Include version number and date in the header. Include a SOURCE
INPUTS section listing what informed the brief:

```
Version: 1.0
Date: [date]
Stage: [idea / prototype / early revenue / scaling]
Source inputs: [list of strategic memo, personas, GTM plan, conversations, etc.]
```

If the brief is later updated, create a new bit with incremented version and a
"Changes from vX.X" block at the top. Reference the prior version's bit ID.


---

## Quality Standards

**The Onliness Statement:** Must pass all three tests (swap, cessation, durability).
If it doesn't, the brief isn't done.

**Voice section:** Must be specific enough that two different copywriters, reading only
Section 8, would produce recognizably similar copy. If the voice spec is vague enough
to produce anything, it's not a spec.

**"This NOT That" pairs:** The NO versions must be plausible — things a real person
would write. If the NO version is obviously bad, the pair isn't useful.

**Values:** Every value must cost something. If it doesn't foreclose a revenue stream
or opportunity, delete it.

**Brand Card:** 150 words maximum. If it runs long, the brief is too diffuse.

**AI-Readable Layer:** Must be parseable by a downstream tool without reading the full
brief. Test: can you reconstruct the brand's voice from just the AI-readable layer?


---

## Key Behaviors Summary

**Work section by section.** Don't dump all 13 at once. Present in batches of 2-3,
get founder reaction, then continue.

**The founder's language is data.** How they naturally describe the product often IS
the voice. Pay attention to their word choices, sentence rhythms, and what they
emphasize.

**The enemy is never a competitor.** It's a worldview. If the enemy section reads like
a competitive analysis, rewrite it.

**Values must cost something.** If a value is free to hold, it's not a value.

**"This NOT That" is the proof.** If the voice section is the theory, the pairs are
the evidence. They should be the first thing a new copywriter reads.

**The AI-readable layer is the brief's API.** Downstream tools read it. Get it right.

**The Brand Card is the integration test.** If it doesn't feel like the brand, trace
back to find where the brief went wrong.

**This skill feeds downstream:**
- **brand-naming** — receives naming territory inputs (Section 11)
- **Visual design work** — receives visual direction (Section 10)
- **All copy and content** — references voice spec (Section 8) and AI-readable layer
  (Section 12)
