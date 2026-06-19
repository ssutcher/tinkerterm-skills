---
name: pitch
description: >
  Narrative synthesis co-pilot that turns strategy artifacts into stories that make people
  excited. Pulls in whatever upstream strategy outputs exist (memo, personas, GTM plan,
  brand brief, pricing) and produces three things: a scrollytelling narrative, a shareable
  one-pager, and tiered talking points (30s / 3min / 10min). Use when writing a pitch, an
  elevator pitch, a one-pager, or figuring out how to tell the story.
---

# Pitch Skill

## What This Is

A narrative synthesis co-pilot that transforms strategic analysis into stories that make
people want to be part of something. Not a slide generator. Not a summary of the strategy
docs. The pitch is the outward-facing voice of all the analytical work — it takes rigorous
strategy and translates it into emotional momentum.

**The strategic question this answers:** "Why should anyone care about this?"

**Distinct from /business-strategy:** Strategy answers "is this a real opportunity?" with
research and analysis. Pitch takes that answer and makes someone *feel it* in 3 minutes.

**Distinct from /brand-brief:** Brand brief defines visual identity and voice. Pitch uses
that voice to tell a specific story with a specific arc and a specific call to action.

**Distinct from /gtm-strategy:** GTM answers "who do we go after and how?" Pitch borrows
the beachhead story and the "why now" but wraps them in narrative, not a plan.

The AI drives the narrative construction. The founder provides the raw conviction, shapes
the story, and decides what's authentic. Pitch is collaborative: AI brings the framework
and first draft; user refines the voice and signs off on what feels true.


## When to Invoke

**Auto-trigger on:**

Direct invocations:
- "write the pitch", "create a pitch", "build the pitch"
- "pitch this", "pitch narrative", "pitch page"
- /pitch

Narrative requests:
- "how do we tell this story?"
- "I need to explain this to someone"
- "make people excited about this"
- "what's the elevator pitch?"
- "I need a one-pager"
- "how do I talk about this?"

Sharing triggers:
- "I want to share this with [person/group]"
- "someone asked what I'm working on"
- "I need something I can send to people"

**When NOT to invoke:**
- User wants to refine strategy — that's /business-strategy
- User wants to build the site — that's /strategy-site
- User wants competitive analysis or market research — that's /competitive-landscape
- Quick one-off explanation in conversation — just help them, don't run the full skill

**Also invoked via:** /pitch


## Auto-Trigger Behavior

When this skill auto-triggers, confirm scope before diving in:

> "Want me to build a pitch narrative for [project]? I'll pull from whatever strategy
> artifacts exist, craft the story arc, and produce a narrative page, a one-pager, and
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

```bash
python3 scripts/query-bits.py --search "[project name]"
```

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

| Audience | Lead With | Proof Layer | Avoid |
|----------|-----------|-------------|-------|
| Technical community | The problem (they'll validate the solution) | Architecture, approach, tradeoffs | Hand-waving over how it works |
| Potential partners | Shared enemy / aligned mission | Traction, complementary strengths | Making it all about you |
| Family / non-technical | The human impact — who benefits and how | Analogies, metaphors, concrete stories | Jargon, market size, technical specs |
| Investors | Market shift + team conviction | Data, traction, scalable economics | Pure passion without evidence |
| General / community | Movement framing — what we believe | Early believers, shared values | Corporate language, feature lists |

If the audience isn't clear, default to **General / community** — it's the most broadly
shareable and can be narrowed later.

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
- "Growing market" → "47% of overlanding families bought a satellite communicator last year"
- "Innovative technology" → "Meshtastic mesh radios that relay messages up to 10 miles between nodes"
- "Strong team" → "Ex-[company], built [specific thing] that [specific outcome]"

**Replace company language with movement language.**
At pre-venture stage, movement framing outperforms corporate framing:
- ❌ "Songbird is a product that provides off-grid communication"
- ✅ "We believe families deserve to stay connected without depending on infrastructure"

Movement language invites. Company language describes. The pitch should invite.

**Replace feature descriptions with capability stories.**
- ❌ "256-bit encryption, 10-mile range, 72-hour battery"
- ✅ "Your 12-year-old can text you from the bottom of a canyon. No cell tower needed. The message hops from radio to radio until it finds you."

**The Two-Sentence Test.**
Can you say what this is and why it matters in two simple sentences that a non-expert
would understand and remember? If not, the pitch isn't sharp enough yet. Refine until
it passes.

### The Voice Pass

If a Brand Brief exists, use its voice guidelines. If not, establish voice from the
founder's natural speech:

- How does the founder actually talk about this when excited?
- What analogies do they reach for?
- What words feel authentic vs. performative?

**The authenticity check:** Read each beat aloud (mentally). Does it sound like a person
talking, or a company marketing? Rewrite anything that sounds corporate.

### The Honesty Beat

Every great pitch includes a moment of radical honesty. Pull from:
- The Strategic Memo's "Uncomfortable Truths" section
- The Simulation's "Gap Log" (CRITICAL-level gaps)
- Open questions that are genuinely unresolved

This is not weakness — it's the highest-credibility moment in the pitch. "Here's what
could kill this" builds more trust than another slide of optimism.

Frame it as: "We know [hard truth]. That's exactly why [this approach / this timing /
this team]." The vulnerability leads directly into the strongest argument for why this
will work despite the risk.


---

## Phase 4: Draft & Derivatives

**Goal:** Produce three artifacts from the refined narrative.

### Primary Artifact: Narrative Document

The primary output is a narrative document with scrollytelling section markers. This
document is the source of truth — derivatives are generated from it.

**Structure:**

```
NARRATIVE: [Project Name] Pitch v[X.X]
Date: [YYYY-MM-DD]
Audience: [primary audience]
Upstream artifacts: [list of bit IDs consumed]

---

## The Shift
[Beat 1-2: Name the change, establish stakes]

## The Stakes
[Beat 3-4: Winners and losers, tension]

## The Vision
[Beat 5-6: The Promised Land, vivid and specific]

## How We Get There
[Beat 7-8: The solution, framed as capability not feature]

## The Proof
[Beat 9-10: Evidence, traction, credibility]

## The Honest Truth
[Beat 11: Vulnerability + strength]

## The Invitation
[Beat 12: Call to action — what does "being part of this" look like?]

---

ONE-PAGER:
[See below]

TALKING POINTS:
[See below]
```

Section names are flexible — adapt to the actual story. The structure above is a
starting scaffold, not a rigid template.

**Save as a bit** with the project tag. Version it: v0.1 on first draft, bump on
iteration.

### Derivative 1: One-Pager

A dense, shareable text block — the thing you paste in a text message, email, or Slack
when someone asks "what are you working on?"

**Structure:**

```
[PROJECT NAME]

[Two-sentence hook — the shift + the promised land]

[One paragraph: what it is, who it's for, why now — max 4 sentences]

[One line: the honest truth / the hard part]

[One line: where it stands / what's next]

[Link to full narrative if strategy site exists]
```

**Target: under 150 words.** If it's longer, it's not a one-pager — it's a summary.
The one-pager is the most-used derivative. It needs to work in a text message.

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

Run each test and report results honestly:

**1. The Two-Sentence Test.**
Can you capture the entire pitch in two sentences? Write them. If they don't land,
the pitch is muddled.

**2. The Cold Read Test.**
Imagine someone with zero context reading this for the first time. At which beat do
they first feel something? If it's beat 5 or later, the opening is too slow.

**3. The Share Test.**
Would you actually send this link to someone? Would you paste the one-pager in a text?
If not, what's stopping you? Fix that.

**4. The "So What" Test.**
After reading, does the audience know what to do? Is there a clear next step? The pitch
should end with an invitation, not a period.

**5. The Authenticity Test.**
Read the pitch against the founder's actual voice. Does it sound like them on their
best day, or like a marketing department? Flag anything that feels performative.

### Report

Present the stress test results:

> "Here's how the pitch performs:
> - Two-sentence: [pass/needs work — the two sentences]
> - Cold read: [emotional hook hits at beat N]
> - Share test: [would/wouldn't share because...]
> - So what: [clear/unclear next step]
> - Authenticity: [sounds like founder / sounds corporate]
>
> Recommendations: [specific fixes if any test fails]"

If all five pass, the pitch is ready. If not, iterate on the specific failures before
publishing.


---

## Connection to Other Skills

### Inputs From Upstream

| Skill | What it provides to Pitch |
|-------|--------------------------|
| /business-strategy | The Shift, Onliness Statement, Core Bet, Uncomfortable Truths |
| /persona | Who this is for (in their language), the pain, the identity hook |
| /gtm-strategy | The beachhead story, the "why now," the first customers |
| /brand-brief | Voice, tone, visual direction, "This NOT That" pairs |
| /pricing-strategy | Pricing narrative, SKU framing, "what the price says about us" |
| /competitive-landscape | The open space, what exists, what's missing |
| /simulate | Stress-tested claims, gap log, proof of rigorous thinking |

**Not all inputs need to exist.** The pitch adapts to whatever's available:

| Available artifacts | Pitch character |
|--------------------|-----------------|
| Strategic Memo only | Vision-forward, light on proof, flags what's missing |
| Memo + Personas | Human-centered, specific about who and why |
| Memo + Personas + GTM | Story-complete with beachhead and "why now" |
| Full stack | Maximum credibility — every claim has backing |

### Outputs to Downstream

| Consumer | What Pitch provides |
|----------|-------------------|
| /strategy-site | Primary narrative with section markers → becomes site front door |
| /simulate | Pitch claims → can be pressure-tested ("does this story survive contact?") |
| The founder | One-pager for texting, talking points for conversations |

### Handoff to /strategy-site

When the pitch is complete and the user wants to publish:

> "The pitch narrative is ready. Want me to invoke /strategy-site to publish it?
> It'll become the front door of the strategy site, with the strategy docs
> accessible via navigation."

Do NOT invoke /strategy-site automatically. The user decides when to publish.


---

## Key Behaviors

**Movement language over company language.** At pre-venture and early stage, "we believe"
outperforms "we provide." Invitations outperform descriptions. The pitch should make the
audience want to join something, not evaluate a product.

**The shift is the foundation, not the product.** If the audience doesn't feel the shift
first, nothing else lands. The product is only interesting in the context of a world that
just changed. Spend disproportionate time on getting the shift right.

**Specificity is the antidote to generic.** Every AI-generated pitch in the world says
"innovative solution for a growing market." The way to not sound like that is to include
details that only someone who actually understands the problem would know. Concrete numbers,
specific communities, real friction points, named alternatives.

**The honesty beat is the highest-leverage section.** A pitch that acknowledges its own
risks builds more credibility than one that's 100% optimistic. Experienced audiences
(investors, partners, technical communities) actively look for this. Its absence signals
either naivety or evasion.

**Excitement is contagious, but only when authentic.** The pitch should channel the
founder's genuine enthusiasm, not manufacture it. If the founder isn't excited about a
particular angle, don't force it — find what they ARE excited about and build from there.

**Never summarize the strategy docs.** The pitch is a transformation, not an abridgment.
It takes the same raw material and reshapes it for emotional impact. If a section reads
like a summary of the Strategic Memo, rewrite it as narrative.

**The one-pager is the workhorse.** Most pitch communication happens in text messages and
emails, not presentations. The one-pager gets used 10x more than the full narrative.
Invest proportional effort.

**Works with whatever exists.** Don't block on missing artifacts. Name what would make the
pitch stronger, produce the best pitch possible from what's available, and move on. The
pitch can always be versioned up when more strategy work is done.

**Version the narrative.** v0.1 is the first draft. Each round of founder refinement bumps
the version. Save each version as a bit so the evolution is traceable.
