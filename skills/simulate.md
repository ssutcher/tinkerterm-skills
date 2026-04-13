---
name: simulate
description: >
  GTM and business simulation engine. Takes a GTM plan, persona bits, and brand brief
  and runs a time-horizon simulation — making plan actions concrete, modeling realistic
  market responses, tracing persona journeys, surfacing gaps and broken assumptions.
  Runs two branches at key dependencies (e.g., disaster event / no disaster event).
  Outputs a Simulation Brief (pre-run inputs), saves full narrative to bit, then
  delivers a Findings Report (TLDR, branch comparison, metric scorecard, gap log,
  assumption tracker, recommendations). Findings lead. Narrative is reference.
  Triggers on: "simulate the GTM plan", "run a simulation", "stress test the plan",
  "play this out", "what would actually happen if", "simulate year 1", /simulate.
---

# Simulate Skill

## What This Is

A pressure-testing engine for GTM plans, business strategies, and go-to-market hypotheses.
Not prediction. A structured stress test that makes vague plan steps concrete enough to
reveal gaps, forces realistic friction, and traces the actual experience of each persona
through the plan's touchpoints.

**The output isn't "this will work."**
The output is: here's where the plan is underspecified, here's where the assumptions
held, here's where they broke, here's what to fix.

**Distinct from gtm-strategy:** GTM strategy writes the plan. Simulate executes it
against reality and finds what the plan missed. Simulation is what you do after the plan
is written, before you commit resources.

**Distinct from business-strategy:** Strategy answers "is this a real opportunity?"
Simulation answers "if we actually execute this plan, what happens week by week?"

**The value is in the gap log, not the narrative.** The narrative is reference material.
The Findings Report is what changes the plan.

---

## When to Invoke

**Auto-trigger on:**
- "simulate the GTM plan"
- "run a simulation"
- "stress test the plan"
- "play this out"
- "what would actually happen if we..."
- "simulate year 1", "what does year 1 look like"
- After completing gtm-strategy when the user wants to pressure-test before executing

**Also useful when:**
- A plan has a key dependency (disaster trigger, editorial endorsement, network effect)
  that needs stress testing before committing
- A plan is running and you want to compare actual results against simulated trajectory
- A pivot is being considered — simulate the new path before committing

**When NOT to invoke:**
- Quick "what if" questions — just answer them directly
- Plans without a first-customer path — need that first (gtm-strategy)
- When the user explicitly wants research, not simulation

---

## The Simulation Model

### Agents

The simulation runs multiple agents simultaneously:

**The Founder** — the protagonist. Takes actions from the plan in concrete sequence.
Not "pitch press" — writes the actual pitch email. Not "reach HOAs" — contacts a
specific person with a specific ask.

**The Market** — press, organizational buyers, podcast hosts, platform algorithms.
Responds realistically, including friction, silence, partial responses, and competing
priorities. Does not reply to every email. Has its own timeline.

**Named Persona Agents** — each target persona runs as an independent journey thread:
- Where they are at T=0 (no awareness, partial awareness, or considering)
- How the plan's actions reach them (or don't)
- What their discovery, consideration, and purchase journey looks like
- When they encounter friction, and what resolves it

**Competitor / External agents** — if relevant: what competitors are doing during the
simulation window, what external events affect the plan.

### Time Model

Discrete phases aligned to the GTM plan's stage gates. Within each phase, time is
tracked at week-level resolution where relevant (pitch emails, decision cycles, press lead
times) and month-level where appropriate (revenue trajectory, channel trends).

### Uncertainty Model

Two branches at each major dependency:
- The simulation identifies the 1-2 highest-risk dependencies in the plan
- Runs Base case (things work roughly as planned) and Stress case (dependency fails
  or is delayed)
- Findings Report compares Year 1 state across both scenarios

---

## The Three Layers

Simulation output has three distinct layers with different purposes and audiences.

```
LAYER 1: SIMULATION BRIEF
  What: Structured inputs table presented before the simulation runs
  Purpose: Confirm what the simulation will model before committing
  Format: Structured table (scannable, not prose)
  When: Before Layer 2 begins — user confirms or adjusts
  Inline: YES

LAYER 2: SIMULATION RUN
  What: Full narrative — founder takes actions, market responds, personas journey
  Purpose: Generate the evidence base for the Findings Report
  Format: Action block format (full detail, concrete, week-level resolution)
  When: After Layer 1 confirmation
  Inline: NO — saved to bit only. Not printed in the conversation.
          Print: "Simulation complete. Saved as bit [ID]. Running Findings Report..."

LAYER 3: FINDINGS REPORT
  What: Structured analysis derived from the narrative
  Purpose: Primary deliverable — surfaces the gaps, broken assumptions, and fixes
  Format: TLDR → Branch Comparison → Metric Scorecard → Gap Log → Assumption
          Tracker → Recommendations → Document Update List
  When: Immediately after Layer 2 completes
  Inline: YES — this is what the conversation shows
```

**Why this order matters:** Findings lead. The narrative is rich but long — 50+ action
blocks for a Year 1 simulation. Printing it inline buries the findings. The Findings
Report is what changes the plan. The narrative is what you read when you want to
understand *why* a gap appeared.

---

## Layer 1: Simulation Brief

**Load inputs using search_bits or ask the user for bit references:**
- GTM plan: `search_bits(query: "gtm-plan [product]")`
- Lead persona: `search_bits(query: "persona [product]")`
- Brand brief: `search_bits(query: "brand-brief [product]")`
- Strategic memo: `search_bits(query: "strategic-memo [product]")`

**Extract and state explicitly:**
- Key actions (in order)
- Key dependencies (what the plan requires to be true)
- Stage gates (the plan's own success criteria)
- Metric targets (what the plan commits to measuring)
- Branch points (where a single variable changes the outcome significantly)

**Build the agent roster:**
Name each agent. State their T=0 condition in 2-3 sentences (who they are, what they
know, what they're doing instead of buying). T=0 conditions are the starting point
for persona threads — if they're wrong, the simulation is wrong.

**Present the Simulation Brief in structured table format:**

```
SIMULATION BRIEF — [Product]
────────────────────────────────────────────────────────────
INPUTS
────────────────────────────────────────────────────────────
Product:           [name, SKUs, prices]
Time horizon:      Month 0 through Month N
Plan version:      GTM Plan vX.X (bit [ID])
Persona bits:      [bit IDs or titles]
Brand brief:       bit [ID]
Strategic memo:    bit [ID]
────────────────────────────────────────────────────────────
AGENTS
────────────────────────────────────────────────────────────
[Name]             [T=0 condition in 1 sentence]
[Name]             [T=0 condition in 1 sentence]
────────────────────────────────────────────────────────────
KEY DEPENDENCIES
1. [What the plan requires to be true]
2. [What the plan requires to be true]
────────────────────────────────────────────────────────────
STAGE GATES
Gate 1:  [criteria] — target Month N
Gate 2:  [criteria] — target Month N
────────────────────────────────────────────────────────────
METRIC TARGETS
[metric]:          [target]
[metric]:          [target]
────────────────────────────────────────────────────────────
BRANCH POINT (Month N)
Scenario A:        [dependency holds — specific description]
Scenario B:        [dependency fails — specific description]
────────────────────────────────────────────────────────────
SIMULATION ASSUMPTIONS
1. [held assumption — explicit about what's taken as given]
2. [held assumption]
...
────────────────────────────────────────────────────────────

Confirm to run, or adjust any inputs before I proceed.
```

Wait for confirmation before running Layer 2.

---

## Layer 2: Simulation Run

**Execute internally.** Do not print the narrative inline. The conversation should show:
"Running simulation... [brief status notes on major events as they occur]... Simulation
complete. Saved as bit [ID]. Running Findings Report..."

The narrative runs fully — month by month, action block by action block — but is
captured as output, not conversation.

**Action block format (internal; saved to bit):**

```
[T+N] — [Action Name]

FOUNDER DOES:
[Specific, concrete action. Include actual copy if the action is outreach or messaging.]

MARKET RESPONDS:
[Realistic response including friction, timing, and partial commitment. Not binary
yes/no. Includes what doesn't happen (silence, non-response, "let's revisit").]

PERSONA THREAD:
[Where each relevant persona is at this moment — what they know about the product,
whether the plan's actions have reached them yet, what they're doing instead.]

METRICS:
[Units sold: X | [relevant metric]: X | Revenue: $X]

GAP FLAGGED (if any):
[What the plan left unspecified that became load-bearing at this step.]
```

**Stage gate checkpoints (internal; saved to bit):**

```
[STAGE GATE — Month N]

Required by plan:
  □ [Criterion 1]: [status]
  □ [Criterion 2]: [status]

Actual state:
  [Metric]: [actual vs. target]

Gate: MET / NOT MET / PARTIAL
If not met: [what's the gap and what does the founder decide?]
```

**Branch execution (internal; saved to bit):**

At the major branch point, explicitly state the fork and run both paths. Save both to
the same bit under clearly labeled sections.

**Save the narrative as a bit:**
- `create_bit(type: simulation, project: [product], tags: simulation gtm-simulation [product] [horizon])`
- Title: "[Product] Simulation — [Horizon] — Narrative"
- Version in content: `Simulation v0.1 | [date]`
- Include both branches in full

Print the bit ID when saved.

---

## Layer 3: Findings Report

The primary inline output. Print immediately after "Simulation complete."

**Format:**

```
FINDINGS REPORT — [Product] [Horizon] Simulation
Simulation v0.1 | [date]
Full narrative: bit [ID]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

TLDR
──────────────────────────────────────────────────
• [The most important finding in 1 sentence]
• [What held / what broke, in aggregate]
• [Branch delta — what the key dependency was worth]
• [Top gap in 1 sentence]
• [The plan's core verdict — directionally correct? fundamentally flawed?]

BRANCH COMPARISON
──────────────────────────────────────────────────
                        SCENARIO A       SCENARIO B
Units sold              [X]              [X]
Revenue                 [X]              [X]
[Key metric]            [X]              [X]
[Key metric]            [X]              [X]
Stage gate met          Month N          Month N
Year 2 setup            [state]          [state]

Delta: [what the key dependency was worth in concrete terms]

METRIC SCORECARD
──────────────────────────────────────────────────
METRIC              TARGET      SCEN A      SCEN B      STATUS
[metric]            [target]    [actual]    [actual]    PASS/MISS
[metric]            [target]    [actual]    [actual]    PASS/MISS

[Note any metrics the plan did not specify — these are gaps in themselves]

GAP LOG (priority-ordered)
──────────────────────────────────────────────────
CRITICAL — fix before launch
  #N: [Gap name]
      Plan said:   [assumption]
      Reality:     [what simulation revealed]
      Fix:         [specific, actionable edit to the plan]

HIGH — fix before Month 1
  #N: [Gap name]
      Plan said:   [assumption]
      Reality:     [what simulation revealed]
      Fix:         [specific, actionable edit to the plan]

MEDIUM — fix before Month 3
  #N: [Gap name]
      Plan said:   [assumption]
      Reality:     [what simulation revealed]
      Fix:         [specific, actionable edit to the plan]

ASSUMPTION TRACKER
──────────────────────────────────────────────────
HELD ([N] assumptions confirmed):
  • [assumption] — [evidence from simulation]
  • [assumption] — [evidence from simulation]

BROKE ([N] assumptions contradicted):
  • [assumption] — [what happened instead]
  • [assumption] — [what happened instead]

NEVER TESTED ([N] assumptions not reached):
  • [assumption] — [why the simulation didn't reach this]
  • [assumption] — [why the simulation didn't reach this]

RECOMMENDATIONS
──────────────────────────────────────────────────
1. [Priority: Critical] [Title]
   [2-3 sentences: what to do and why it matters]

2. [Priority: High] [Title]
   [2-3 sentences: what to do and why it matters]

3. [Priority: High] [Title]
   [2-3 sentences]

DOCUMENTS TO UPDATE
──────────────────────────────────────────────────
• [Document name] (bit [ID]): [specific edit — which section, what to add/change]
• [Document name]: [specific edit]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Full narrative → bit [ID]
Re-run after plan updates: /simulate v0.2
```

**Save the Findings Report as a separate bit:**
- `create_bit(type: simulation, project: [product], tags: simulation findings-report [product] [horizon])`
- Title: "[Product] Simulation — [Horizon] — Findings Report"
- This is the bit to share — it contains all findings without the full narrative.

When re-running, create new bits for both layers. Don't overwrite. The version trail matters.

---

## Key Behaviors

**Findings lead, narrative is reference.** The Findings Report is the primary output.
The narrative is what you read when you want to understand *why* a gap appeared, not what
you read first. Printing the narrative inline buries the findings. Never do this.

**Concrete over abstract.** Simulations that stay abstract reveal nothing. If the plan
says "pitch press," the simulation writes the pitch — specific journalist, specific hook,
specific ask. The fiction is the method. Making the action concrete forces the question:
"can we actually do this?" and "is this the right ask?"

**Realistic friction, not pessimism.** The goal isn't to kill the plan. PR pitches have
a 10-30% response rate in this category — simulate that, not guaranteed failure. Not
everyone says yes, not everyone says no. The market is busy, not hostile.

**Persona threads are non-negotiable.** If the simulation can't trace how the lead
persona actually discovers and purchases the product, the GTM plan isn't concrete enough
to simulate. Surface that as Gap #1 and force the question before running further.

**Gap log priority order matters.** CRITICAL gaps block the plan. HIGH gaps cause
meaningful delay or revenue loss. MEDIUM gaps reduce efficiency but don't threaten
the outcome. The distinction tells the founder where to spend the next 48 hours.

**Assumptions that break go in the Findings Report, not just the narrative.** If an
assumption breaks in Month 2, it should appear in both the Month 2 action block (as a
gap flag) and the Findings Report assumption tracker (as BROKE). The Findings Report is
the synthesis; the narrative is the evidence.

**Two inputs define simulation quality:** The precision of the GTM plan's "first 10"
section and the depth of the persona bits. Sketch-tier personas produce thin simulations.
If persona depth is insufficient, note it and either proceed with flagged assumptions or
invoke the persona skill to deepen before running.

**Feed back upstream — specifically.** Don't just output findings. The Findings Report
ends with a "Documents to Update" block that names which bits need edits, which
section, and what the specific change is. "Update the GTM plan" is not a recommendation.
"Add a Year 1 unit target to the GTM plan's Metrics section — suggest: 250 = survived,
500 = on track, 800+ = ahead of plan" is a recommendation.

**Re-runnable by design.** Simulation → gap found → plan updated → re-simulate.
Each re-run bumps the version (v0.1 → v0.2) and saves a new bit. The thinking trail
is preserved. The Findings Report header references the previous version so changes are
visible across runs.

---

## Time Horizon Parameters

**Default:** Through the GTM plan's defined scope (usually first 100 customers or first
stage gate).

**Extended options:**
- "Year 1" — T=0 through Month 12, including post-stage-gate scaling
- "Year 2" — through Month 24, including bowling pin expansion
- "To $1M ARR" — runs until the revenue milestone is reached or the simulation reveals
  it can't be reached on the current plan

When the horizon extends beyond the GTM plan's defined scope, the simulation flags what
the plan leaves underspecified in the extended window before proceeding.

---

## Ecosystem Position

```
business-strategy  → Strategic Memo + Onliness Statement
persona            → Persona bits with JTBD + Four Forces
brand-brief        → Brand Brief bit with AI-Readable Layer
gtm-strategy       → GTM Plan with First 100 + Stage Gates
        ↓
simulate           ← Pressure test: concrete execution, realistic friction,
                      persona journeys, gap surfacing
        ↓
        Layer 1: Simulation Brief (confirm inputs)
        Layer 2: Simulation Run → saved to bit
        Layer 3: Findings Report → inline (TLDR, gaps, assumptions, recs)
        ↓
Updated GTM plan / amended strategy bets / persona refinements
```

**Inputs from:** gtm-strategy (plan), persona (journey agents), brand-brief
(voice/positioning constraints for outreach copy), business-strategy (uncomfortable
truths, structural risks)

**Feeds back to:** Specific plan edits (gaps surfaced → GTM plan updated), persona
upgrades (simulation reveals shallow persona understanding → persona skill at Grounded tier),
strategy memo (assumptions that break in simulation → Strategic Bets section updated)

---

## Anti-Patterns

**Printing the narrative inline.** This buries the findings in 50+ action blocks. The
Findings Report exists to fix this. If the narrative is in the conversation, the skill
is being used wrong.

**The optimistic simulation.** Everything works, all pitches get replies, all buyers
convert in Month 1. This produces a confidence document, not a stress test. Explicitly model
the realistic failure rates.

**The death-spiral simulation.** Everything fails, nothing works, the plan is
hopeless. Also not useful. Model realistic friction — some things work, some don't,
the founder has to make decisions.

**Simulating to the plan's level of specificity.** If the plan says "pitch press," the
simulation should go one level more concrete. The point is to surface what the plan
didn't say.

**Stopping at the stage gate.** A 1-year simulation doesn't stop when the first 100
customers are reached. What happens in Month 9 is as important as what happens in
Month 2.

**Forgetting the persona threads.** The simulation is about the founder AND the customer.
The persona's first encounter with the product is the simulation's most important
thread. Don't let it get crowded out by operational detail.

**Gap log without priority.** A flat list of 13 gaps is overwhelming. Priority-ordering
(CRITICAL / HIGH / MEDIUM) tells the founder what to fix in the next 48 hours vs. the
next month. Always prioritize.

**Vague "documents to update" section.** "Update the GTM plan" is not actionable.
"GTM plan Section 5 (Stage Gates): add Year 1 unit target — suggest 250/500/800+ tiers"
is actionable. Every document update should include the specific section and the specific
change.
