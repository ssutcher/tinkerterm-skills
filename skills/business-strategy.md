---
name: business-strategy
description: >
  Research-backed strategic co-pilot for new startup ideas. Runs parallel research
  across market, competition, customer, business model, and GTM — synthesizes into
  an opinionated strategic memo with explicit bets and direction. Activate when the
  user shares a startup idea, says "what do you think about this idea", "I'm thinking
  of building X", "is there a market for X", "should I pursue this", or directly asks
  for a strategy: "create a business strategy", "build a strategy", "run a strategy
  on this", "I want a strategy for X", "let's do a strategy".
---

# Business Strategy Skill

## What This Is

A research-backed strategic co-pilot for startup ideas. Not a business plan generator.
The output is a strategic memo — a short, opinionated document that makes explicit bets,
names what's uncertain, and gives the team directional clarity.

The AI does the research. The founder provides the raw material and shapes the output.
Strategy is a collaborative product: AI brings the research, analysis, and first drafts;
user refines the framing, challenges the conclusions, and signs off.


## When to Invoke

**Auto-trigger on:**
- User shares a new startup idea or product concept
- "What do you think about this idea?", "I'm thinking of building X"
- "Is there a market for X?", "Should I pursue this?"
- "Create a business strategy", "build a strategy", "run a strategy on this"
- "We're considering X as a business", "I want a strategy for X"

**When NOT to invoke:**
- User is already mid-execution — they need a specific story, not a strategy
- Quick tactical question about an existing business — just answer it
- User explicitly says they don't want a strategy session right now

## Auto-Trigger Behavior

When this skill auto-triggers, confirm scope before diving in:

> "Want me to run a full strategy on this? I'll research the market, competition,
> and business model — then pull it together into a strategic memo we can work from."

Wait for confirmation. If yes, proceed to Phase 1.


---

## The Four Phases

```
FRAMING → RESEARCH → [PERSONAS] → MEMO → ITERATE
```

---

## Phase 1: Framing

**Goal:** Establish what question the strategy needs to answer. Wrong framing = wrong
research = useless document.

**Collect from the founder (conversationally, not as a form):**

1. **The idea** — what is it, for whom, in 1-3 sentences
2. **The customer** — who you think has this problem. Push for specificity: "Who exactly?
   What role, what context, what pain intensity?"
3. **Stage** — idea / prototype / early revenue / scaling
4. **What you already know** — anything validated, researched, or assumed about this market

**AI behavior:**
- Ask 1-2 questions at a time, not all at once
- Don't accept vague customer descriptions — push for specificity
- After collecting inputs, propose the strategic question: "Based on this, the question
  I'm going to answer is: [X]. Does that feel right?"
- Confirm before starting research. This is load-bearing.

**Strategic question types:**
- "Is this a real opportunity and how big?" — early-stage idea validation
- "How do we win in this market?" — idea is validated, strategy is the question
- "What's the strongest version of this business?" — pivoting or refining
- "Should we build this or is there a better path?" — build/buy/partner decisions


---

## Phase 2: Research

**Goal:** Gather real external knowledge across five strategic dimensions. AI runs these
autonomously — founder is not involved in this phase.

Research is not exploratory browsing. Each agent has a specific question.
Run Round 1 agents in parallel; synthesize in Round 2.

---

### Research Sources by Dimension

**Problem & Customer** — find evidence the problem is real, who has it worst

High-signal sources:
- **Reddit** — highest-signal free source for unfiltered pain. Search `site:reddit.com
  "[problem keywords]"`. Look for: "I wish there was", "anyone else dealing with", "we've
  been using spreadsheets". Real pain has specificity (names the workaround, quantifies
  the cost), frustration (upvotes + "same here"), and recurrence across multiple threads.
  GummySearch (gummysearch.com) aggregates Reddit pain signals by subreddit.
- **G2 / TrustRadius 1-3 star reviews** — TrustRadius is more reliable (52% review
  acceptance rate, no gift-card incentives). Disgruntled users are honest. Also look for
  what reviewers use as workarounds ("we export to Excel and...").
- **Job postings as pain signals** — a company posting "Head of [function] Operations"
  for the first time = they've outgrown their current process. Multiple "Coordinator"
  roles = manual, unautomated work. Underused and highly specific.
- **Hacker News** (hn.algolia.com) — high quality for developer tools and technical B2B.
  Filter to comments on relevant threads — often more valuable than the posts.

**Competitive Landscape** — map who's solving this and where the open space is

Key tactics:
- For each competitor: website positioning, G2/TrustRadius reviews (weaknesses), LinkedIn
  headcount 6-month change (40% growth > any press release), job posting content (engineer
  JDs = tech stack, product JDs = roadmap, sales JDs reveal their ICP).
- **Wayback Machine** — check competitor pricing pages from 2-3 years ago. Many had
  public pricing before moving to "contact sales." Shows how pricing and positioning evolved.
- **Job posting OTE pricing method** — standard B2B SaaS quota = OTE × 5. A $200K OTE
  AE → ~$1M quota. Divide by deals/quarter to estimate ACV. SMB AEs ($110-150K OTE) →
  $5-25K ACV. Mid-market ($140-200K OTE) → $25-100K. Enterprise ($250K+) → $100K+.
- **Vendr buyer guides** (vendr.com) — actual enterprise contract price ranges from
  verified spend. Better than pricing page scraping for real enterprise pricing.
- **Facebook Ad Library** — search any company name for active ads. Free. Shows paid
  acquisition signal.
- Map four competitor types: Direct / Indirect / Substitutes (including spreadsheets and
  "do nothing") / Aspirational. The substitute category is where most analysis fails —
  if the real competition is "doing it manually," that matters more than any startup.

**Market & Timing** — size the market, find the inflection point

Key sources:
- **Bottom-up sizing** (preferred over top-down reports): (# potential customers) ×
  (annual revenue per customer). For US business counts by industry: Census County
  Business Patterns (data.census.gov, search by NAICS code). For buyer counts by job
  title: BLS OEWS (bls.gov/oes, covers 830 occupations).
- **LinkedIn Ads audience estimator** — create a draft campaign, set targeting by
  industry + company size + job title, audience size appears in the builder. Free,
  real-time market count. Underused for market sizing.
- **Google Trends** — directional only. Rising trend on problem keywords corroborates
  "this is getting worse." Flat or declining = warning for the "why now" thesis.
- **Crunchbase free tier** — count funded companies in the category. Proxy for
  competitive intensity and VC conviction about the market.
- Avoid Gartner/IDC reports as primary source — applied growth rates to prior estimates,
  18-24 months old, opaque methodology. Never use "1% of the market" framing.

**Business Model** — understand revenue models and unit economics

Key sources:
- **Meritech Analytics** (meritechcapital.com/benchmarking) — every public SaaS company:
  valuation multiples, gross margins, NRR, payback periods. Best free tool for public
  comparable analysis.
- **High Alpha / OpenView SaaS Benchmarks** — 800+ private SaaS companies. CAC payback
  (~10-15 months median), NRR (106% median venture-backed), LTV:CAC targets. Free.
- **SaaS Capital** (saas-capital.com/research) — 1,000+ private B2B SaaS, including
  bootstrapped benchmarks. Free.
- Stage mismatch trap: benchmarks are dominated by $5-50M ARR companies. Under $1M ARR,
  100-200% YoY growth is normal. Apply mid-market benchmarks to a $500K ARR company
  and the comparison is noise.

**GTM Patterns** — how have companies in similar spaces gotten first customers?

Key sources:
- **First Round Review** (review.firstround.com/go-to-market/) — best narrative GTM
  case studies. Long-form, named founders, specific tactics. Skews 0-$1M ARR.
- **Lenny Rachitsky** — "How the fastest-growing B2B businesses found their first 10
  customers" (Figma, Slack, Stripe, Airtable, Gusto). Free.
- **YC Library** — ycombinator.com/library → "how did you get your first customer" —
  50+ founders from a recent batch answering the same question.
- **Autopsy** (getautopsy.com) — 2,000+ startup failure post-mortems, searchable by sector.
- Channel signals from competition: Content-driven = competitors rank on SEO keywords;
  Community-driven = active Discord/Slack/subreddit; PLG signal = 3+ competitors have
  free tiers; Outbound = competitors hiring SDRs/BDRs early.

---

### Round 1 — All Parallel

**Agent: Problem & Customer**
Question: Is this problem real, who suffers most acutely, and what do they currently do?
Find: Evidence the problem is real; who has it worst (specific roles, industries, contexts);
current solutions and their failure modes; pain intensity signals.

**Agent: Competitive Landscape**
Question: Who else is solving this, how are they positioned, and where is the open space?
Find: All four competitor types; how each is positioned; weaknesses; recent moves; where
the gaps are — segments underserved, jobs unmet, price points uncovered.

**Agent: Market & Timing**
Question: How big is this, is it growing, and what inflection point makes now the right time?
Find: Bottom-up market size estimate; growth rate and direction; key trends; "why now"
signal — what changed in the last 2-3 years that makes this solvable or urgent. Mandatory.

**Agent: Business Model**
Question: What are the credible ways to make money here, and what do the economics look like?
Find: Revenue model patterns from comparable companies; pricing benchmarks; unit economics
ranges (CAC, LTV, payback); what model has worked vs. failed in this space and why.

**Agent: GTM Patterns**
Question: How have companies in similar spaces actually acquired their first customers?
Find: GTM playbooks from analogous companies; which channels worked; typical sales motion;
time-to-close benchmarks; common GTM mistakes in this space.

---

### Round 2 — After Round 1 Complete

**Agent: Opportunity Assessment (Synthesis)**
Does NOT do additional external research. Reads all five Round 1 outputs and forms an
opinion.

Produce:
- Point of view on whether the opportunity is real and compelling (honest, not cheerful)
- The strongest version of the business — what positioning, customer, and model makes
  this most defensible
- The 2-3 things that have to be true for this to work (load-bearing assumptions)
- The 2-3 biggest risks — specifically what could kill this
- Initial view on competitive moat: what type, at what stage
- The open questions only the founder can answer

---

### Research Standards

- Label all market size numbers as estimates
- Cite sources or note the basis for claims ("based on 3 competitor pricing pages")
- If a dimension has thin data, say so — don't fill gaps with confident guesses
- If something contradicts founder assumptions, flag it directly


---

## Phase 2.5: Strategic Personas (Optional)

**Goal:** Sharpen the ICP before writing the memo.

**When to run:** If Round 2 synthesis reveals multiple distinct customer segments, or if
the ICP still feels demographic rather than behavioral. If the customer is clearly defined
and singular, skip to Phase 3.

**How:** Invoke the `persona` skill at Sketch tier. Pass as context: Round 1 Problem &
Customer findings, Round 2 synthesis, founder's customer description from Phase 1.

Sketch tier: hypothesis-only, no community research, 2 personas maximum.

**Check in after:** "Research surfaced [N] distinct customer types. My read is [Persona A]
is the strongest beachhead because [reason]. Does this match what you're seeing?"

---

## Phase 3: First Draft — The Strategic Memo

**Goal:** Produce a structured memo that synthesizes research into an opinionated document
with a point of view, explicit bets, and clear direction.

The memo is NOT a business plan. Short on description, long on implication and decision.

---

### Memo Structure

```
[Business Name] — Strategic Memo
Version: 0.1 (Draft)
Date: [date]
Stage: [idea / prototype / early revenue / scaling]
Strategic Question: [the question framed in Phase 1]
```

**THE CORE BET**

One paragraph: "We're betting that [specific customer] has [specific problem] that
[existing solutions] can't solve well because [structural reason]. [Our approach] wins
because [key insight]. If this is true, the business looks like [business model sketch]
and the path to win is [strategic direction]."

This paragraph is the document. Everything else supports or challenges it.

---

**WHY WE BELIEVE THIS**

- The problem is real: [specific evidence, not assertion]
- The timing is right: [the inflection point — what changed]
- The customer will pay: [evidence of WTP, even proxy signals]
- We can win: [the moat hypothesis — honest about now vs. what we build toward]

If any is weak, say so. "We don't have strong evidence on WTP yet" is the right answer.

---

**WHAT THE RESEARCH FOUND**

*Market* — key facts about size, growth, dynamics. Bottom-up estimate + confidence level.
The one trend that matters most.

*Competition* — positioning map in plain language. Where the open space is. The 1-2
competitors that are actually dangerous and why.

*Customer* — if Phase 2.5 ran: lead persona name, JTBD statement, persona bit reference.
If not: specific ICP, the job they're hiring for, how acute the pain is, what they
currently do and why that fails them.

*Business Model* — what the economics look like in comparable companies. What revenue
model is standard and why. Rough unit economics range.

---

**THE OPEN QUESTIONS**

Format: > **[Assumption]** — [why uncertain] → [how to validate]

Aim for 3-5. This section is more valuable when it's uncomfortable.

---

**THE STRATEGIC BETS**

Format: > We're [doing X], not [alternative Y], because [specific reasoning].

Real decisions with tradeoffs, not default assumptions.

---

**DIRECTION**

*Validate first:* The single riskiest load-bearing assumption.

*Build toward:* The long-term defensible position. Near-term decisions must be consistent.

*Don't do:* Explicit tradeoffs — things that seem adjacent but are out of scope, and why.

---

**THE ONLINESS STATEMENT**

Only write this after competitive landscape, JTBD, and Strategic Bets are resolved.

Format: > "[Brand] is the only [category] that [differentiated benefit] for [specific
customer] who [specific context / emotional state]."

Swap test: replace the brand name with a competitor's. If it still works, the
differentiation isn't real yet.

---

**BRAND BRIEF HANDOFF** *(optional — include if brand work is next)*

- Onliness Statement, Category, JTBD (functional/emotional/social), Founding insight,
  Why now, The enemy (the worldview being rejected, not a competitor list)

**GTM HANDOFF** *(optional — include if GTM strategy work is next)*

- Lead Persona: [name + archetype] (persona bit title: [name], or "not yet built")
- Beachhead hypothesis, Sales motion hypothesis, Primary channel bet, Why now,
  Relevant Strategic Bets

---

### Memo Tone Standards

- Answer first, support second. Opinionated, not neutral. Honest about uncertainty.
- No filler — every sentence is a finding, implication, or decision.
- Short — readable in 10-15 minutes.


---

## Phase 4: Iteration

AI drives this — not passive "do you have changes?" but active resolution of the
highest-uncertainty areas.

1. **Name the weak spots explicitly.** Don't wait for the founder to find them.
2. **Ask targeted questions** from the Open Questions — one at a time: proprietary insight,
   unfair advantage, GTM hypothesis.
3. **Push back when warranted.** If founder input contradicts research, name the tension.
4. **Update and version the memo.** Each substantive revision bumps the version (0.1 → 0.2).
5. **Run the swap test** on the Onliness Statement.
6. **End when:** Open Questions resolved, Onliness Statement fails the swap test, founder
   confirms the Core Bet reflects their actual thesis.


---

## Output Standards

- Readable in 10-15 minutes
- Pass the "Core Bet test": new team member reads first paragraph, knows the bet
- Every Open Question resolved or marked as known risk
- Direction specific enough to act on

**Saving the memo:** `create_bit(type: strategy-memo, project: [product-name])`
Include the version number and date in the content header.

---

## Key Behaviors Summary

**Frame before researching.** Confirm the strategic question before any agent runs.

**Research is autonomous.** Come back with findings, not requests for more input.

**Form an opinion.** The Opportunity Assessment agent must have a point of view.

**The memo is a decision document.** If you read it and don't know what the company is
betting on, what it's not doing, and what to do first — it's not done.

**Iteration is AI-driven.** Name the weak spots. Ask the hard questions. Push back.

**The Onliness Statement is the capstone.** Only writable after the research is done.

**This skill feeds three downstream skills:**
- **persona** — Phase 2.5 invokes it at Sketch tier. Output saved as bits (type: persona).
- **brand-brief** — receives Onliness Statement and Brand Brief Handoff block.
- **gtm-strategy** — receives GTM Handoff block. Builds the first-customer plan.
