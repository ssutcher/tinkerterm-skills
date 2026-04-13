---
name: pitch
description: >
  Narrative synthesis co-pilot that transforms strategy artifacts into compelling stories
  that make people excited about an idea. Consumes whatever upstream strategy outputs exist
  (Strategic Memo, Personas, GTM Plan, Brand Brief, Pricing, Simulations) and synthesizes
  a pitch narrative using Raskin's strategic narrative framework and Duarte's sparkline
  emotional pacing. Produces three artifacts: a primary narrative document (with section
  markers), a shareable one-pager, and tiered talking points (30s / 3min / 10min). Works
  with whatever exists — a pitch from just a Strategic Memo is still a pitch. The skill's
  job is to answer "why should anyone care about this?" Triggers on: "write the pitch",
  "pitch this", "make people excited about this", "create a pitch", "write the narrative",
  "how do we tell this story", "elevator pitch", "one-pager", /pitch.
---

# Pitch Skill

## What This Is

A narrative synthesis co-pilot that transforms strategic analysis into stories that make
people want to be part of something. Not a slide generator. Not a summary of the strategy
docs. The pitch takes rigorous strategy and translates it into emotional momentum.

**The strategic question this answers:** "Why should anyone care about this?"

**Distinct from other skills:** /business-strategy answers "is this a real opportunity?"
with research. /brand-brief defines visual identity and voice. /gtm-strategy answers
"who do we go after and how?" Pitch takes all of that and makes someone *feel it*.

The AI drives the narrative construction. The founder provides the raw conviction, shapes
the story, and decides what's authentic. AI brings the framework and first draft; user
refines the voice and signs off on what feels true.


## When to Invoke

**Auto-trigger on:** "write the pitch", "pitch this", "create a pitch", "how do we tell
this story?", "make people excited about this", "elevator pitch", "I need a one-pager",
"I need something I can send to people", /pitch

**When NOT to invoke:**
- User wants to refine strategy — that's /business-strategy
- User wants competitive analysis — that's /competitive-landscape
- Quick one-off explanation — just help them, don't run the full skill

## Auto-Trigger Behavior

When this skill auto-triggers, confirm scope before diving in:

> "Want me to build a pitch narrative for [project]? I'll pull from whatever strategy
> artifacts exist, craft the story arc, and produce a narrative, a one-pager, and
> talking points. Who's the primary audience — investors, partners, community, or
> general excitement?"

Wait for confirmation. If yes, proceed to Phase 1.


---

## The Five Phases

```
INTAKE → NARRATIVE ARCHITECTURE → VOICE & SPECIFICITY → DRAFT & DERIVATIVES → STRESS TEST
```

---

## Phase 1: Intake

**Goal:** Understand what raw material exists, who the audience is, and what's already
compelling vs. what needs work.

### Load Available Artifacts

Search for the project's strategy artifacts:

`search_bits("[project name]")`

Look for:
- Strategic Memo (the core bet, Onliness Statement, open questions)
- Personas (who this is for, their pain, their language)
- GTM Plan (beachhead, why now, the first customers)
- Brand Brief (voice, visual tone, "this not that" pairs)
- Pricing Plan (the pricing narrative, SKU architecture)
- Simulations (proof of thinking, stress-tested claims)
- Competitive Landscape (what exists, what's missing, the open space)

**Not all of these need to exist.** The pitch works with whatever's available. A pitch
from just a Strategic Memo is thinner on proof points but still valid. Name what's
missing so the founder knows what would strengthen the narrative later.

### Identify the Audience

The same core story flexes for different audiences. Ask (or infer from context):

- **Technical community** — lead with the problem, prove with architecture. Avoid hand-waving.
- **Potential partners** — lead with shared enemy / aligned mission. Avoid making it all about you.
- **Family / non-technical** — lead with human impact. Use analogies. Avoid jargon.
- **Investors** — lead with market shift + team conviction. Prove with data and traction.
- **General / community** — lead with movement framing. Prove with shared values.

Default to **General / community** if unclear — most broadly shareable.

### Assess What's Compelling

Before constructing the narrative, name:
1. **The single strongest thing about this idea** — What makes someone lean forward?
2. **The honest vulnerability** — What makes this hard? (This builds credibility.)
3. **The "why now" trigger** — What changed in the world that makes this timely?
4. **The identity hook** — Who does this make the audience want to be?

Present these four elements to the founder for validation before proceeding.

> "Here's what I think the story hinges on:
> - Strongest hook: [X]
> - Honest vulnerability: [Y]
> - Why now: [Z]
> - Identity hook: [W]
>
> Does this feel right? What am I missing?"


---

## Phase 2: Narrative Architecture

**Goal:** Build the story skeleton. Two frameworks combined: Raskin gives structure,
Duarte gives emotional pacing.

### The Raskin Skeleton (5 Elements)

Build the narrative around Andy Raskin's strategic narrative framework:

**1. Name an undeniable shift in the world.**
Not "the market is big." A real, observable change that the audience can verify
independently. Technology shift, cultural shift, regulatory shift, demographic shift.
The shift must be TRUE whether or not your product exists.

**2. Show there will be winners and losers.**
The shift creates stakes. People/companies/families who adapt will thrive. Those who
don't will fall behind or suffer. This is where tension enters the narrative.

**3. Paint the Promised Land.**
What does the future look like for the winners? Be specific and vivid. This is NOT
a product description — it's a world description. The audience should want to live
in this future.

**4. Introduce magic gifts that help reach the Promised Land.**
NOW you can talk about your product/solution. Position it as the thing that gets the
audience from the shift to the Promised Land. Features become capabilities that serve
the larger narrative.

**5. Show evidence that you can make it real.**
Proof: traction, prototypes, early users, simulations, team credibility, anything that
moves this from "nice story" to "this is actually happening."

### The Duarte Sparkline (Emotional Pacing)

Layer Nancy Duarte's sparkline on top of the Raskin skeleton. The sparkline alternates
between:

- **"What is"** — the current painful reality, the broken status quo, friction and loss
- **"What could be"** — the better future, the possibility, the vision

This alternation creates emotional rhythm. Tension (what is) → release (what could be)
→ tension → release, building toward a crescendo. The final beat should be the most
vivid "what could be" — the Promised Land at full resolution.

**Map the sparkline onto the Raskin elements:**
```
THE SHIFT (what is — the world changed)
  → WINNERS/LOSERS (what could be / what is — stakes revealed)
    → PROMISED LAND (what could be — full vision)
      → MAGIC GIFTS (what is → what could be — how we get there)
        → EVIDENCE (what is — proof it's real, not just a dream)
          → CALL (what could be — the invitation)
```

### Structure the Arc

Draft the narrative arc as a sequence of beats, not slides. Each beat is:
- **Headline** (one sentence that carries the point)
- **Emotional register** (tension or release)
- **Content** (2-3 sentences or a single vivid image)

Target: 8-12 beats for the full narrative. Fewer is fine. More is a sign of overloading.

Present the arc to the founder before writing:

> "Here's the story arc I'm proposing — [number] beats:
> [Beat list with headlines and emotional register]
>
> Does this flow feel right? Any beats that feel wrong or missing?"


---

## Phase 3: Voice & Specificity

**Goal:** Kill everything generic. Force concrete details. Find the authentic voice.

### The Specificity Pass

Go through every beat and apply these filters:

**Replace abstractions with evidence.**
"Growing market" → "47% of overlanding families bought a satellite communicator last year."
"Strong team" → "Ex-[company], built [specific thing] that [specific outcome]."

**Replace company language with movement language.**
At pre-venture stage, movement framing outperforms corporate framing. "We believe families
deserve to stay connected without depending on infrastructure" beats "Songbird is a product
that provides off-grid communication." Movement language invites. Company language describes.

**Replace feature descriptions with capability stories.**
"Your 12-year-old can text you from the bottom of a canyon. No cell tower needed." beats
"256-bit encryption, 10-mile range, 72-hour battery."

**The Two-Sentence Test.** Can you say what this is and why it matters in two sentences
a non-expert would understand and remember? If not, the pitch isn't sharp enough yet.

### The Voice Pass

If a Brand Brief exists, use its voice guidelines. If not, establish voice from the
founder's natural speech:

- How does the founder actually talk about this when excited?
- What analogies do they reach for?
- What words feel authentic vs. performative?

**The authenticity check:** Read each beat aloud (mentally). Does it sound like a person
talking, or a company marketing? Rewrite anything that sounds corporate.

### The Honesty Beat

Every great pitch includes a moment of radical honesty. Pull from the Strategic Memo's
"Uncomfortable Truths," the Simulation's "Gap Log," or genuinely unresolved open questions.

This is not weakness — it's the highest-credibility moment in the pitch. Frame it as:
"We know [hard truth]. That's exactly why [this approach / this timing / this team]."
The vulnerability leads directly into the strongest argument for why this will work.

---

## Phase 4: Draft & Derivatives

**Goal:** Produce three artifacts from the refined narrative.

### Primary Artifact: Narrative Document

The primary output is a narrative document with section markers. This document is the
source of truth — derivatives are generated from it.

**Structure:** Header (title, date, audience, upstream artifact IDs), then sections:
The Shift → The Stakes → The Vision → How We Get There → The Proof → The Honest
Truth → The Invitation. Followed by ONE-PAGER and TALKING POINTS sections.

Section names are flexible — adapt to the actual story. This is a starting scaffold,
not a rigid template.

**Save as a bit.** Version it: v0.1 on first draft, bump on iteration.

`create_bit(type: note, project: [product-name], tags: pitch-narrative [product-name])`

### Derivative 1: One-Pager

A dense, shareable text block — the thing you paste in a text message or email when
someone asks "what are you working on?" Structure: project name, two-sentence hook
(the shift + promised land), one paragraph (what/who/why now, max 4 sentences), one
line on the hard part, one line on status/next steps.

**Target: under 150 words.** The one-pager gets used 10x more than the full narrative.

### Derivative 2: Talking Points (Tiered)

Scripts for verbal delivery at three lengths:

**30-second pitch (elevator):**
- One sentence: the shift
- One sentence: what we're building
- One sentence: why it matters
- One sentence: the invitation

**3-minute pitch (conversation):**
- The shift (30s)
- The stakes — who wins, who loses (30s)
- The vision — what the future looks like (30s)
- What we're building — capability story, not features (30s)
- The proof — what gives us the right to do this (30s)
- The ask / invitation (30s)

**10-minute pitch (presentation):**
- Full Raskin arc with Duarte sparkline pacing
- Include the honesty beat
- Include audience-specific proof layer
- End with the invitation, not a summary
- Note: this is NOT a slide-by-slide script. It's a narrative arc for spoken delivery.
  If slides are needed, they support the story — the story doesn't follow the slides.

Present all three derivatives to the founder for review.


---

## Phase 5: Stress Test

**Goal:** Verify the pitch actually works before publishing.

### The Five Tests

1. **Two-Sentence Test.** Can you capture the entire pitch in two sentences? If they don't land, the pitch is muddled.
2. **Cold Read Test.** Someone with zero context reads this. At which beat do they first feel something? If beat 5 or later, the opening is too slow.
3. **Share Test.** Would you actually paste the one-pager in a text? If not, what's stopping you? Fix that.
4. **"So What" Test.** Does the audience know what to do after reading? The pitch should end with an invitation, not a period.
5. **Authenticity Test.** Does it sound like the founder on their best day, or like a marketing department? Flag anything performative.

### Report

Present results for all five tests with pass/needs-work and specific recommendations.
If all five pass, the pitch is ready. If not, iterate on the failures before publishing.


---

## Connection to Other Skills

**Inputs from upstream:**
- /business-strategy → The Shift, Onliness Statement, Core Bet, Uncomfortable Truths
- /persona → Who this is for (in their language), the pain, the identity hook
- /gtm-strategy → The beachhead story, the "why now," the first customers
- /brand-brief → Voice, tone, visual direction, "This NOT That" pairs
- /pricing-strategy → Pricing narrative, SKU framing
- /competitive-landscape → The open space, what exists, what's missing
- /simulate → Stress-tested claims, gap log, proof of rigorous thinking

**Not all inputs need to exist.** Strategic Memo only = vision-forward, light on proof.
Add Personas = human-centered. Add GTM = story-complete. Full stack = maximum credibility.

**Outputs to downstream:** /simulate can pressure-test pitch claims. The founder gets
a one-pager for texting and talking points for conversations.


---

## Key Behaviors

- **Movement language over company language.** "We believe" outperforms "we provide." The pitch should make the audience want to join something, not evaluate a product.
- **The shift is the foundation, not the product.** If the audience doesn't feel the shift first, nothing else lands. Spend disproportionate time getting the shift right.
- **Specificity is the antidote to generic.** Include details only someone who understands the problem would know. Concrete numbers, specific communities, real friction points.
- **The honesty beat is the highest-leverage section.** Acknowledging risks builds more credibility than 100% optimism. Its absence signals naivety or evasion.
- **Excitement is contagious, but only when authentic.** Channel the founder's genuine enthusiasm. If they aren't excited about an angle, find what they ARE excited about.
- **Never summarize the strategy docs.** The pitch is a transformation, not an abridgment.
- **The one-pager is the workhorse.** Most pitch communication happens in texts and emails. Invest proportional effort.
- **Works with whatever exists.** Don't block on missing artifacts. Name what's missing, produce the best pitch from what's available, move on.
- **Version the narrative.** v0.1 on first draft. Each refinement round bumps the version.
