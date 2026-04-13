---
name: persona
description: >
  Build synthetic personas for business strategy using the JTBD-native persona framework.
  Guides segment mapping, community grounding, and collaborative template construction.
  Produces a complete persona artifact (Sketch, Grounded, or Full tier) for use in
  positioning, messaging, JTBD analysis, UX, and GTM strategy.
  Triggers on: "build a persona", "create personas", "let's do personas", "synthetic persona",
  "who is our customer", "define our audience", "persona for [project]", "let's build personas".
---

# Persona Skill

## Purpose

Guide the collaborative construction of synthetic personas using the JTBD-native framework.
AI brings first drafts of each section, user refines, and we produce a complete persona file
that's actually usable for strategic work — not just an impressive artifact that sits unread.

## When to Invoke

- Building personas for a new or existing project
- Validating or refining existing audience hypotheses
- Before positioning, messaging, or GTM strategy work
- When "who are we building this for?" is the open question

## When NOT to Invoke

- Just reading or referencing existing personas — search bits for prior personas
- Pure market research without persona construction — use the `research` skill
- Already mid-activation (running VPC, Dunford, etc.) — load the persona and proceed

---

## Outputs

**Save with:** `create_bit(type: persona, project: [project-slug])` — use the persona name
and archetype label as the bit title.
**Tier label:** Every persona opens with its tier (Sketch / Grounded / Full).

---

## The Five Stages

Walk through these in order. Each stage has a checkpoint before moving on.

---

### Stage 1: Context (orient before building)

**Goal:** Understand what we're building, for whom, and why.

**AI behavior:**
1. Ask:
   - What project/product is this for?
   - What strategic decision does this persona need to support?
     (Early exploration? Positioning? Messaging? GTM launch?)
   - Is there an existing segment hypothesis, or are we starting fresh?

2. Check bits for prior knowledge:
   - `search_bits(query: "[project name] audience")`
   - `search_bits(query: "[project name] persona")`

3. Check if personas already exist for this project:
   - `search_bits(query: "[project name] persona")`

4. Surface what we know and what we don't. Be explicit about confidence.

**Checkpoint:** "Here's what we know, here's what we don't. Ready to map segments?"

---

### Stage 2: Segment Map

**Goal:** Identify 3-5 distinct buying patterns before building any persona.

The most common mistake is jumping straight to persona construction without agreeing on
which segments actually matter. Segments first, portraits second.

**AI behavior:**
1. Draft a hypothesis segment map based on project knowledge + bits.
   For each proposed segment, specify:
   - Name (memorable label for the buying pattern)
   - One-sentence description
   - Hypothesis struggling moment
   - Hypothesis current hire (what they're using today, including non-consumption)
   - Why this is a distinct segment (what makes it strategically different from the others)

2. Apply the load-bearing test to each segment:
   - Distinct struggling moment? (not just different demographics)
   - Distinct current hire? (different competitive set)
   - Distinct blocking forces? (different anxieties and habits)
   - Does designing for this segment drive different product/messaging decisions?

3. Flag any segments that fail the test and propose collapsing them.

4. Name the key open question: "The segment we're least sure about is X because..."

**Present as a table for easy review and editing.**

**Checkpoint:** "Does this segment map match your intuition? What would you change?"

**Do NOT start building personas until the user approves the segment map.**

---

### Stage 3: Tier Selection

**Goal:** Choose the right depth for the current decision.

**AI behavior:**
Present the three tiers and recommend one based on what we've established in Stage 1:

```
SKETCH (1-2 hours)
  All claims: Hypothesis
  No community research
  Good for: early brainstorming, investor conversations, team alignment
  Not for: load-bearing strategic decisions

GROUNDED (4-6 hours)
  MVG community pass: 2 subreddits + 1 review site, 15-20 quotes
  5+ claims upgraded to Observed or Inferred
  Evidence log with 15-20 quotes
  Good for: early positioning decisions, segment validation, fundraising

FULL (12-20 hours)
  Complete community ethnography
  All fields populated, backstory 300-500 words
  Evidence log 50+ quotes
  Pre-computed activation fields
  Good for: durable strategic asset, launch decisions, full activation sequence
```

State the recommendation and why. User decides.

**Checkpoint:** "Tier confirmed. How many personas are we building this session?"

---

### Stage 4: Community Ethnography

**Skip for Sketch tier.** For Grounded and Full tiers:

**Goal:** Ground persona claims in observed community behavior before constructing.

**AI behavior:**

1. Define the research target for this project's audience. Propose:
   - 2-3 primary subreddits
   - 1-2 review platforms (G2, Capterra, Amazon, app stores)
   - Any niche forums or Discord communities

2. Run the research (use WebSearch and WebFetch):
   - Reddit: sort Top / All Time, read top 20 posts + top comments per subreddit
   - Reviews: 20 reviews filtered by relevant role/use case, including competitor reviews
   - Weight posts by engagement (upvotes = lurker signal)

3. Extract signal across the seven types:
   - Language patterns (exact words real people use)
   - Struggling moment signal ("I finally reached a breaking point when...")
   - Objections and skepticism ("I looked at X but didn't buy because...")
   - Social context (who do they ask? who validates them?)
   - Reference points (what do they compare to?)
   - Emotional language (how they want to feel)
   - Workarounds (cobbled-together solutions in use today)

4. Run the disconfirmation pass:
   - For every pattern found, actively search for contradicting evidence
   - Note where patterns hold and where they break down
   - This is mandatory, not optional

5. Collect 15-20 quotes (MVG) or 50+ (Full) into an evidence log draft.
   Tag each quote: source, engagement level, signal type, which persona it supports.

6. Write 5+ grounded claims with confidence labels:
   - OBSERVED: multiple sources, explicit, high-engagement validation
   - INFERRED: pattern-implied, requires reasoning step
   - HYPOTHESIS: theory-based, no community evidence found

**Output:** Evidence log draft + list of grounded claims with confidence labels.

**Checkpoint:** "Here's what the community data shows. Does this change or confirm our segment map?"

---

### Stage 5: Template Construction (per persona)

**Goal:** Build each persona collaboratively, one section at a time.

**Walk through 5 sections. Each section: AI drafts → user refines → approve before moving on.**

For each persona, open with:
```
--- Building: [PERSONA NAME] ---
Segment: [Which buying pattern this represents]
Tier: [Sketch / Grounded / Full]
Evidence basis: [X grounded claims from community research / Hypothesis-only]
```

---

#### Section 1: The Job Core

Draft these fields:

**Name:** Fictional but demographically grounded. Not "Alex the Privacy Advocate" —
a real-sounding name that reflects who actually shows up in this buying pattern.

**Archetype label:** Memorable 2-4 word label for this buying pattern.
(e.g., "The Reluctant Prepper", "The Ideological Sovereign", "The Worried Parent")

**One-line:** Who they are + what they need, in plain English.

**JTBD Statement:**
"When [struggling moment / triggering circumstance], I want [desired progress],
so I can [expected outcome / underlying motivation]."
This should be specific and causal. "When [specific situation]" not "when I feel like..."

**Job Dimensions:**
- Functional: what they're trying to accomplish (task level)
- Emotional-personal: how they want to feel / avoid feeling
- Social: how they want to be perceived

**Current hire:** What are they using today? Be specific. Include non-consumption
and workarounds. This is the real competitive set.

**Confidence label per field.**

**Checkpoint:** "Does this feel like a real person with a real problem?"

---

#### Section 2: The Four Forces

Draft these fields:

**Push:** Specific dissatisfactions with the current situation.
Concrete and time-stamped where possible. What makes their current life feel unbearable?
(Verbatim language from community research preferred)

**Pull:** Specific vision of progress. What does the better future look like in their mind?
What are they imagining when they think about solving this?

**Anxiety:** What's blocking the switch? Fear of failure, learning curve, wrong choice,
switching cost, fear of looking foolish. Be specific — "fear of wasted money on something
that won't work when I actually need it" is better than "risk aversion."

**Habit:** What they'd have to give up or unlearn. What inertia is keeping them in place?
The more elaborate their current workaround, the harder the behavior change being asked.

**Purchase formula note:**
The purchase happens when (Push + Pull) > (Anxiety + Habit).
Name the current balance: "Right now, anxiety is probably winning because..."

**Confidence label per force.**

**Checkpoint:** "Does the force balance feel right? Which force is most underappreciated?"

---

#### Section 3: The Switch Timeline

Draft these fields:

**First thought:** The earliest moment dissatisfaction registered. Often mundane.
"Again. This happened again." This seed may have been planted months before active search.

**Passive looking:** What triggers them to start noticing alternatives without shopping?
What information are they now more receptive to?

**Active looking trigger:** The specific event that tips from passive to active search.
This is the content/outreach trigger moment — the signal to intercept.

**Decision criteria:** What are they actually comparing when they evaluate?
(Often different from what they say they're comparing)

**Post-purchase anxiety:** What makes them doubt the switch was right?
This directly informs onboarding design.

**Confidence label per stage.**

**Checkpoint:** "Does the timeline feel coherent? What would accelerate someone through it?"

---

#### Section 4: The World

This section makes the persona human and stable.

**Narrative backstory (300-500 words for Full, 150-200 for Grounded, 75-100 for Sketch):**
A real story. Not bullet points. What happened in this person's life that makes
this problem real to them? What are they trying to build or protect?
This is the most important field in the entire template — it's what makes the
persona behave consistently when you ask strategic questions of it.
Write it in third person, present tense.

**Day in the life:**
Where does this problem show up in their actual week? What's happening around it?
What else is competing for their attention? (IDEO activation method)

**Reference points:**
What brands, products, or categories do they respect?
What's their price reference point?
What do they use as mental comparison?

**Social context:**
Who do they ask when making decisions like this?
Who validates them? Who influences them?
(This IS the distribution strategy)

**Information diet:**
Where do they learn about things in this category?
(YouTube channels, subreddits, newsletters, word of mouth, trade shows?)

**Moore archetype:** [Innovator / Early Adopter / Early Majority / Late Majority]
State which one and why. This is non-negotiable — it determines messaging register,
channel, whole product requirements, and evidence needed to close.

  Innovator:      Excited by tech itself. No ROI justification needed.
  Early Adopter:  Motivated by competitive advantage. Buys on vision.
  Early Majority: Risk-averse. Needs case studies, complete solution, peer validation.
  Late Majority:  Buys only when it's an established standard.

**Checkpoint:** "Does this feel like someone you could imagine? Would you recognize them
if you met them?"

---

#### Section 5: Pre-Computed Activation Fields

**Skip for Sketch tier. Include for Grounded and Full.**

Draft these fields so the persona is immediately usable for strategy work:

**Messaging lead:** What should lead the message for this persona?
(a) The push — lead with the named problem ("Tired of X?")
(b) The pull — lead with the vision ("Imagine Y")
(c) The proof — lead with evidence ("Teams like yours...")
State which and why, based on their current switch timeline position.

**Trust triggers:**
What specifically builds trust for this persona? What instantly destroys it?
(Specific — "no subscription fees, ever" is better than "transparency")

**Objection inventory:**
3-5 specific objections they'll raise + the underlying reason for each.
(The reason determines the response — anxiety-based objections need different handling
than habit-based objections)

**Anti-signals:**
What messaging or product choices would repel this persona even if not obviously harmful?
(e.g., "enterprise language", "app required", "community-dependent value prop")

**Positioning hook:**
How the Dunford competitive-alternative framing lands for this persona specifically.
What are they comparing against, and what makes the differentiated value land?

**Hire / fire model:**
What would make them hire us: [specific conditions]
What would make them fire us: [specific conditions]
What we replaced: [the current hire / what they fired]

**Checkpoint:** "Are the activation fields specific enough to be useful?
Could you write a headline from the messaging lead right now?"

---

### Saving the Persona

After all 5 sections are approved:

1. **Save with:** `create_bit(type: persona, project: [project-slug])`
   - Bit title: "[Full Name] — [Archetype Label]"

2. **Bit content structure:**
   ```
   PERSONA: [Full Name] — [Archetype Label]
   PROJECT: [Project name]
   TIER: [Sketch / Grounded / Full]
   LAST GROUNDED: [date of community research, or "Hypothesis-only" if Sketch]
   VERSION: 1.0
   CREATED: [date]

   [All five sections in order, with confidence labels inline]

   ---
   EVIDENCE LOG
   [Quotes organized by theme, with source and confidence label]

   ---
   RESEARCH GAPS
   [Hypothesis-level claims that need validation]
   [Specific interviews or surveys that would upgrade these claims]

   ---
   ACTIVATION NOTES
   Recommended starting stage: [Stage 1-5 from the activation sequence]
   Next activation step: [specific framework to run next]
   ```

3. **Open** the saved bit with the `open_in_sidekick` tool.

4. **Confirm:**
   ```
   ✅ Persona created: [Name] — [Archetype]
   Tier: [Tier]
   Grounded claims: [N]
   Hypothesis claims: [N]
   Activation fields: [included / not included]

   Next: [what to do with this persona — which activation stage fits the current need]
   ```

---

## Key Behaviors

**Segment map before persona construction. Always.**
Don't start building Section 1 until Stage 2 is complete and approved.
If you skip segment mapping, you build convincing portraits of the wrong people.

**Confidence labels are non-negotiable.**
Every non-trivial claim gets Observed / Inferred / Hypothesis.
A beautifully written persona with no confidence labels is confident fiction.

**The backstory is the most important field.**
Don't phone it in. It's what stabilizes the persona when you ask strategic questions of it.
A bullet list is not a backstory. A story is a story.

**Don't over-build before grounding.**
For Sketch tier, resist the urge to fill in rich detail. Mark it Hypothesis and move on.
Depth without evidence is just elaborate assumption.

**The disconfirmation pass is mandatory.**
If community research was done, actively search for contradicting evidence before writing
Observed claims. "I didn't notice any contradictions" is not the pass.

**Honor the collaborative model.**
AI brings first drafts. User might rewrite entirely — that's the point.
Never present a completed persona section as final. Always: "What would you change?"

**Moore archetype is non-negotiable.**
If the user doesn't know which archetype fits, work through the diagnostic:
- What evidence do they need before buying?
- Are they trying to get ahead of peers or avoid falling behind?
- Do they ask "what can this do?" or "what do others do with this?"
This one field determines messaging register, channel, and whole product requirements.

---

## Common Failure Modes to Avoid

**Starting with Section 1 before the segment map is done.**
You'll build a persona without knowing if you picked the right person.

**Treating a well-written hypothesis as a confirmed finding.**
Confidence labels exist for this reason. If it's Hypothesis, it's Hypothesis.

**Generic backstory.**
"Sarah is a 35-year-old marketing manager who values efficiency." That's a demographic
label, not a backstory. A backstory answers: what happened? What does she want to protect?
What keeps her up at night and why?

**Forgetting the disconfirmation pass.**
This is where most persona research fails. Build the habit of searching for evidence
against every pattern you find.

**Building more personas than will get used.**
Five personas means none of them get used. Start with the 1-2 most strategically
load-bearing segments and build those well. Add more as needed.
