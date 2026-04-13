---
name: competitive-landscape
description: >
  Research-backed competitive landscape analysis. Runs parallel research agents across
  market players, positioning, product intelligence, momentum signals, and customer voice —
  synthesizes into a Competitive Landscape Brief with positioning maps, threat scorecards,
  open space analysis, and moat assessment. Three modes: discovery (new market), focused
  (specific product), refresh (update existing). Triggers on: "who are the competitors",
  "competitive landscape", "competitive analysis", "who else is doing this", "map the market",
  "who are we up against", "what does the competitive landscape look like".
---

# Competitive Landscape Skill

## What This Is

A research-backed competitive analysis co-pilot that goes deep on the question every
strategy skill depends on: who else is solving this problem, how are they positioned,
what's their trajectory, and where is the open space?

The AI does the research autonomously. The founder shapes the framing, validates the
positioning map, and challenges the open space analysis.

**Three modes:**
- **Discovery** — broad market map, no prior analysis
- **Focused** — starting from a specific product, find who else is in the space
- **Refresh** — load a prior brief, find what changed


## When to Invoke

**Auto-trigger on:**
- "who are the competitors", "who else is doing this", "what's the competition"
- "competitive landscape", "competitive analysis", "map the market"
- "who are we up against", "what does the landscape look like"
- Before starting a business-strategy session (natural precursor)

**When NOT to invoke:**
- Quick question about a single specific competitor — just answer it
- User wants a feature comparison spreadsheet — that's product work
- Already mid-execution on a validated strategy — this is analysis, not monitoring


## Auto-Trigger Behavior

When this skill auto-triggers, confirm scope and mode:

> "Want me to map the competitive landscape here? I'll research who's solving this problem,
> how they're positioned, and where the open space is. Are we doing **discovery** (broad
> market map), **focused** (starting from your product concept), or **refresh** (updating
> a prior analysis)?"

Wait for confirmation before proceeding.


---

## The Phases

```
FRAMING → RESEARCH → LANDSCAPE BRIEF → ITERATE
```

---

## Phase 1: Framing

**Goal:** Establish the competitive question, market boundaries, and known competitors
before any research runs.

**Step 1 — Determine the mode:**
- **Discovery:** Exploring a market. Start from the problem space, not the product.
- **Focused:** Has a product concept. Start from what they're building.
- **Refresh:** Prior brief exists. Load it, find what changed.

For Refresh mode, search for the prior brief:
`search_bits(tags: competitive-landscape [product-name])`

**Step 2 — Collect framing inputs (conversationally):**

For Discovery:
1. What problem space or market are we mapping?
2. Who has this problem?
3. What competitors are you already aware of?
4. What's driving this analysis?

For Focused:
1. What are you building, in 1-3 sentences?
2. Who's the target customer?
3. Who do you already consider competitors?
4. What strategic question does this analysis need to answer?

Push for specificity on market definitions — "When you say 'project management space,' what
specific job is the customer hiring for?"

**Step 3 — Define market boundaries:**
- The job to be done (JTBD framing)
- The buyer profile
- Geographic scope
- Market segment (SMB, mid-market, enterprise, consumer)

**Step 4 — Confirm the competitive question:**

State the specific question research will answer and get confirmation before proceeding.


---

## Phase 2: Research

**Goal:** Gather real external evidence across five competitive dimensions. AI runs these
autonomously.

### The Competitor Taxonomy

Every competitor gets classified into one of four types (JTBD-native):

**Direct** — Same core job, same target buyer, purpose-built product.

**Indirect** — Different product category, but hired for an overlapping job. Often more
dangerous because they can expand scope.

**Substitutes** — Including "do nothing," spreadsheets, email, manual processes. JTBD
analysis ALWAYS includes these. 40-60% of B2B deals are lost to "no decision."

**Emerging/Adjacent** — Not yet competing but positioned to enter. Signals: adjacent product,
recent funding, hiring in your domain, beta features that encroach.


### Research Sources & Methods

**For Market Players Discovery**
- Web search: `"[job]" software OR tool`, `"[job]" alternative to [competitor]`
- Reddit: `"[problem]" site:reddit.com "I use" OR "we switched to"`
- Hacker News, G2/Capterra comparison pages, AlternativeTo, Product Hunt
- Crunchbase for funded startups not yet visible in SEO
- Job posting signals for emerging competitors

**For Positioning & Messaging Analysis**
- Website analysis: headline, subheadline, social proof, navigation structure
- Wayback Machine: messaging evolution at 6-month intervals
- Meta Ad Library: active ads reveal value proposition and targeting
- Content strategy: blog topics, webinars, comparison pages
- LinkedIn company page positioning

**For Product & Business Model Intelligence**
- Pricing pages (current + historical via Wayback Machine)
- G2/TrustRadius reviews mentioning actual prices paid
- Vendr buyer guides for enterprise pricing
- OTE method: sales job OTE x 5 = quota, divide by deals = estimated ACV
- Changelog/release notes for product velocity
- Job postings for tech stack and roadmap signals

**For Momentum & Trajectory**
- Funding history (Crunchbase)
- LinkedIn headcount: 6-month and 2-year growth
- Hiring patterns: what roles (engineering = product investment, sales = scaling motion)
- Recent launches, partnerships, acquisitions (last 12 months)
- Inferred next moves from job posts, patents, conference talks

**For Customer Voice**
- G2, TrustRadius, Capterra — focus on 1-3 star reviews
- "Switched from" data — which competitors lose users to which alternatives
- Reddit/HN threads: "Why I left [competitor]", "Moving from [X] to [Y]"
- Sentiment patterns by segment (SMB vs. enterprise, technical vs. non-technical)


### Confidence Labeling

Every finding must carry a label:
- **Verified** — Direct evidence from primary source. Citable.
- **Inferred** — Derived from converging signals. Reasonable but not confirmed.
- **Estimated** — Based on limited data or analogies. Needs validation.


### Round 1 — All Parallel

**Agent: Market Players Discovery**
Question: Who is in this space across all four competitor types?
Find: Every player, classified by taxonomy, with one-line description, target segment,
and estimated stage.

**Agent: Positioning & Messaging Analysis**
Question: How does each competitor position themselves, and what do the patterns reveal?
Find: Core promise, target audience language, positioning evolution, messaging gaps.

**Agent: Product & Business Model Intelligence**
Question: What does each competitor sell, how do they price it?
Find: Pricing model and tiers, revenue model, pricing history, tech stack signals.

**Agent: Momentum & Trajectory**
Question: Where is each competitor headed?
Find: Funding, headcount trajectory, recent moves, hiring patterns, likely next moves.

**Agent: Customer Voice**
Question: What do actual users say — what works, what's broken, why do people switch?
Find: Top strengths and complaints per competitor, switching patterns, unmet needs.


### Saving Research (Between Round 1 and Round 2)

After each Round 1 agent completes, save its full output as a bit before passing to
synthesis:

`create_bit(type: insight, project: [product-name], tags: source-research competitive-landscape [product-name])`

Start each bit's content with `## [Agent Name] — [Project] Research` so the agent is
identifiable in search results. Record the bit IDs and pass them to the Round 2 agent.


### Round 2 — After Round 1 Complete

**Agent: Competitive Synthesis**

Does NOT do additional external research. Reads all five Round 1 outputs and produces
structured analysis using these frameworks:

**Positioning Map:**
- 2x2 map with buyer-centric axes (not feature axes)
- Axes must represent real tradeoffs, not "good vs. bad"
- Test: "Would a buyer describe their choice in these terms?"
- Plot all competitors, note clusters and empty quadrants
- If 8+ competitors, produce a Strategy Canvas (Blue Ocean) instead/in addition

**Threat Assessment:**
Score each Direct/Indirect competitor (1-5) on:
1. Market Overlap (30%) — same buyer, same job?
2. Momentum (25%) — growth trajectory
3. Strategic Intent (20%) — evidence they're moving toward your space
4. Resources (15%) — funding, team, distribution
5. Capability Match (10%) — can they replicate your offering?

**Open Space Analysis:**
Identify gaps across: underserved segments, unmet jobs, pricing gaps, positioning angles.
For each: assess WHY it's empty (genuinely underserved vs. structurally unattractive).

**Moat Assessment (Helmer's 7 Powers):**
For top 3 competitors and user's position:
1. Scale Economies
2. Network Effects
3. Counter-Positioning
4. Switching Costs
5. Brand
6. Cornered Resource
7. Process Power

Rate: None / Weak / Moderate / Strong. Trajectory: Building / Stable / Eroding.


---

## Phase 3: The Competitive Landscape Brief

### Brief Structure

```
[Market/Product] — Competitive Landscape Brief
Version: 0.1 (Draft)
Date: [date]
Mode: [Discovery / Focused / Refresh]
Competitive Question: [from Phase 1]
Market Boundary: [JTBD-defined boundary]
```

**THE LANDSCAPE NARRATIVE**
One paragraph with a point of view: "This market is [consolidating / fragmenting / nascent].
The dominant pattern is [X]. The biggest shift is [Y]. The open space is [Z]."

**THE COMPETITIVE FIELD**
All competitors by taxonomy type. For each:
> **[Name]** — [Type] | [Threat Tier: 1/2]
> One-line description. Target segment. Stage. Key differentiator.

Always include "do nothing" / manual workaround as a named substitute.

**TIER 1 COMPETITOR PROFILES**
For top 3-5 (highest threat scores):
> Positioning, Target, Product, Pricing (with confidence label), GTM Motion,
> Momentum, Strengths (top 3), Weaknesses (top 3), Moat, Likely Next Move,
> Why They Matter

**POSITIONING MAP**
2x2 map (or Strategy Canvas) with axis rationale, all competitors plotted, clusters
named, empty quadrants assessed.

**THREAT SCORECARD**

| Competitor | Overlap | Resources | Intent | Momentum | Capability | Composite | Tier |
|------------|---------|-----------|--------|----------|------------|-----------|------|

**OPEN SPACE ANALYSIS**
For each gap:
> Gap name, type, evidence, why it's empty, attractiveness (High/Medium/Low),
> what it would take to own it.

**MOAT ASSESSMENT**
Top 3 competitors + user's position. Primary moat, trajectory, durability.

**STRATEGIC IMPLICATIONS**
> For positioning: [what the landscape implies]
> For product: [what to build/not build]
> For pricing: [competitive pricing context]
> For GTM: [viable motions and channels]
> The single biggest insight: [the one finding that matters most]

**OPEN QUESTIONS**
What couldn't be determined from desk research. Required:
- Tier 1 competitor with Estimated pricing
- "Likely next move" that would change the landscape
- High-attractiveness open space not yet validated with customers

**HANDOFF BLOCKS**
Pre-formatted inputs for downstream skills:
- For business-strategy: landscape summary, top threats, open space, moat hypothesis
- For persona: competitor user segments, JTBD language from reviews, switching triggers
- For pricing-strategy: price points, pricing models, premium/discount patterns, gaps
- For gtm-strategy: competitor motions, channel signals, messaging angles


### Battlecard Output (Optional)

If requested, produce a one-page battlecard per Tier 1 competitor:
Quick Facts, Why We Win, Why We Might Lose, When You Encounter Them, Talk Track,
What's Changing. Use FIA framework: Fact → Impact → Action.


---

## Phase 4: Iteration

1. **Name the weak spots** — don't wait for the founder to find them
2. **Challenge the positioning map** — validate axis selection with the founder
3. **Ask founder-only questions:** Which competitors do you actually encounter? Any
   competitors invisible to desk research? Does the open space match your instinct?
4. **Push back on blind spots** — if founder dismisses a competitor, ask for evidence
5. **Validate the moat hypothesis**
6. **Test the narrative** — does the Landscape Narrative paragraph give the real answer?

**End when:**
- Founder can name the top 3 threats and why
- Positioning map reflects buyer decision criteria
- Open space analysis identifies a compelling gap (or honestly says there isn't one)
- Handoff blocks are populated


---

## Refresh Mode

**Triggers:** 3+ months since last brief, new competitor appeared, significant competitor
move, strategy shifted, preparing for fundraising or board meeting.

**Process:**
1. Load prior brief from bits
2. Run abbreviated agents scoped to "what changed since [date]"
3. Produce "What Changed" summary
4. Update the full brief to a new version

Refresh is not rewrite. Only update what changed.


---

## Output Standards

The final brief must have:
- Opinionated Landscape Narrative (not neutral)
- Every competitor classified by four-type taxonomy
- Tier 1 profiles with confidence-labeled findings
- Positioning map with axis rationale
- Scored threat scorecard
- Open space analysis with honest attractiveness assessment
- Moat assessment using Helmer's 7 Powers
- Strategic implications specific enough to inform decisions
- Populated handoff blocks
- Open questions with validation methods

**Saving the brief:**

`create_bit(type: note, project: [product-name], tags: competitive-landscape [product-name])`

Include version number and date in the content header. Include:

```
SOURCE RESEARCH
  Market Players: bit [ID]
  Positioning & Messaging: bit [ID]
  Product & Biz Model: bit [ID]
  Momentum & Trajectory: bit [ID]
  Customer Voice: bit [ID]
```


---

## Key Behaviors Summary

**Competitors are defined by the job, not the category.** JTBD framing is non-negotiable.

**Always include substitutes and "do nothing."** The manual workaround is almost always
a competitor.

**Empty space is not automatically opportunity.** Assess WHY it's empty before calling
it an opportunity.

**Confidence labels are mandatory.** Verified, Inferred, and Estimated are different
grades of evidence.

**Positioning maps require buyer-centric axes.** "Would a buyer describe their choice
in these terms?" is the test.

**Momentum matters more than size.** Score trajectory, not just position.

**The Landscape Narrative is the capstone.** It must contain a point of view.

**Name the most important insight.** If you can't name one, the analysis isn't done.


---

## Connection to Other Skills

This skill feeds the strategy stack:
- **business-strategy** — Competition section of the Strategic Memo, Core Bet validation
- **persona** — Competitor user segments, JTBD vocabulary from reviews, switching triggers
- **pricing-strategy** — Competitive price map, pricing models, premium/discount patterns
- **gtm-strategy** — Competitor GTM motions, channel signals, battlecard-ready profiles
- **simulate** — Competitor profiles for market response modeling, threat trajectories
