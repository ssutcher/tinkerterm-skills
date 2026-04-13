---
name: pricing-strategy
description: >
  Research-backed pricing co-pilot for early-stage hardware and software products. Takes
  a Strategic Memo and/or persona bits as inputs, runs parallel research agents across
  competitive price maps, WTP signals, COGS benchmarks, and demand-side evidence — then
  synthesizes into a Pricing Plan with a recommended price, SKU architecture, margin model,
  and consumer-facing pricing narrative. Sits in the strategy stack between business-strategy
  and gtm-strategy.
  Triggers on: "what should we charge", "how do we price this", "what's our pricing strategy",
  "pricing model", "what price point", "how do we think about pricing", "what's the right
  price", "let's figure out pricing", /pricing-strategy.
---

# Pricing Strategy Skill

## What This Is

A research-backed pricing co-pilot that answers the question business-strategy doesn't
answer: the strategy is set — now what do we charge, why, and how do we talk about it?

Price is not chosen. It emerges from four interlocking inputs: the COGS floor (what you
must charge to survive), the margin gate (what you must charge to afford your GTM motion),
the competitive context (what the market has already trained buyers to expect), and the
brand signal (what the price communicates about who this is for). Get any of these wrong
and you either lose money or lose customers.

The AI does the research and brings the first draft. The founder provides context,
challenges the margin math, and validates the pricing narrative against what they know
about their customer.

**Distinct from business-strategy:** Strategy answers whether the opportunity is real
and what the Core Bet is. Pricing strategy answers what you charge, given the bet you've
made. Don't run pricing before the Onliness Statement is resolved.

**Distinct from gtm-strategy:** GTM answers who to go after first and through what motion.
Pricing feeds GTM — the price point determines which motion is economically viable.
Run pricing before GTM if possible.

**Inputs from upstream skills:**
- `business-strategy` — Onliness Statement, COGS hypothesis, competitive landscape
- `persona` — JTBD, switching cost, price reference points from the persona's reference
  field. Find with: `search_bits(query: "persona [product]")`


## When to Invoke

**Auto-trigger on:**
- "what should we charge", "how do we price this", "what's our pricing strategy"
- "what price point", "pricing model", "how do we think about pricing"
- "what's the right price", "let's figure out pricing", "pricing research"
- After completing a business-strategy session (natural next step)

**Also useful when:**
- Existing pricing isn't converting and needs a reset
- Entering a new market segment where prior pricing may not hold
- Considering a pricing model change (one-time → subscription, or vice versa)
- Building the financial model for fundraising

**When NOT to invoke:**
- Quick tactical question about a specific number — just answer it
- Established pricing working above $1M ARR — designed for pre-launch to $1M ARR
- User explicitly says pricing is decided and they want execution, not strategy

**Auto-trigger confirmation:**
When this skill auto-triggers, confirm scope before proceeding:
> "Want me to run a full pricing strategy on this? I'll research competitive prices,
> COGS ranges, and WTP signals — then pull it together into a Pricing Plan with a
> recommended price, SKU architecture, and pricing narrative."

Wait for confirmation. If yes, proceed to Phase 1.


---

## The Phases

```
INTAKE → RESEARCH → MARGIN MODEL → PRICING PLAN → ITERATE
```

---

## Phase 1: Intake

**Goal:** Establish the product, COGS hypothesis, and competitive context before research.

**Step 1 — Load from upstream skills (preferred path):**

Search for a Strategic Memo: `search_bits(query: "strategic-memo [product]")`
- If found: load the COGS hypothesis (if present), Onliness Statement, competitive landscape
- Search for persona bits: `search_bits(query: "persona [product]")`
  - From persona: JTBD Statement, Four Forces, price reference points
- Confirm: "I found the Strategic Memo. The COGS hypothesis is [X] and the competitive
  context is [Y]. Does this still reflect your thinking?"

**Step 2 — Gather fresh (if no Strategic Memo):**

Ask these as a conversation, one at a time:

1. What's the product, and what does it cost to make? (Even a rough estimate: materials,
   manufacturing, shipping, certification. "I don't know" is acceptable — that's what
   research is for.)
2. Who's the primary customer and what are they currently paying for the alternative?
3. What are the 2-3 closest competitors, and what do they charge?
4. Is this a one-time purchase, subscription, or usage-based? Is that fixed, or open?
5. What volume do you expect to sell in year 1? Year 2?

Don't accept vague COGS estimates — push for the specific components:
"When you say $X to make, does that include tooling, certification, packaging, and shipping?
Or just materials?" COGS underestimation is the single most common pricing error.

**Step 3 — COGS pre-assessment:**

For hardware products, apply the three-tier manufacturing model:
- Option A (source existing certified hardware): fastest to market, highest COGS, no
  tooling cost. COGS = (retail price of nearest comparable) × 0.6-0.7 (wholesale).
- Option B (custom PCB with pre-certified RF/wireless modules): 6-12 month lead time,
  lower COGS at volume. Break-even vs. A at ~2,000-3,000 units.
- Option C (full custom chip-down): 18-24 month cycle, lowest COGS at 25K+ units.
  Not appropriate pre-PMF.

For software products:
- Below 60% gross margin: SaaS health is at risk
- 75-80%: healthy SaaS margin

State a preliminary COGS range and price floor before research begins.

**Step 4 — Confirm the pricing question:**

Pricing question types:
- "What's the right launch price and why?" — pre-launch
- "Is our current price working, and if not, why not?" — launched products
- "What does a price increase require to execute?" — underpriced products
- "How do we structure the SKU architecture?" — multi-SKU


---

## Phase 2: Research

**Goal:** Gather real external evidence across four pricing dimensions. AI runs these
autonomously. Come back with findings, not requests for input.

---

### Research Methods & Sources

**For Competitive Price Map**

Map every price point in the landscape — direct, indirect, and substitutes.

- Competitor pricing pages (public) + Wayback Machine history (when did they raise prices?)
- G2/Capterra review text — users mention actual prices in complaints
- Vendr buyer guides (vendr.com) — verified enterprise contract price ranges
- OTE method for B2B: standard quota = OTE × 5. A $150K OTE AE has ~$750K quota.
  Divide by deals/quarter to estimate ACV.
- Amazon/eBay completed listings for consumer hardware: what buyers actually paid
- Substitutes: what does the current workaround cost in time, money, and risk?
- G2 reviews mentioning "worth it" vs. "overpriced" — reveals price-value mismatch

---

**For WTP Signals**

Find evidence of what this customer will actually pay — behavior, not stated preference.

- Reddit: search "[category] worth it", "[category] too expensive", "[category] cheap alternative"
  Filter for high-engagement comments (upvotes = lurker signal)
- 1-3 star reviews mentioning price: reveals price-value mismatch and perceived comparables
- 4-5 star reviews mentioning price: reveals price-value resonance frames
- No-subscription premium: 20-40% upfront premium documented for consumers avoiding
  subscriptions (2024-2025 research; 41% subscription fatigue rate). Only accessible
  when trust exists — new brands can't command the full premium without editorial validation.
- Find 2-3 brands that made a distinctive pricing decision and the market response.

---

**For COGS Benchmarks**

Ground the COGS estimate with manufacturer data and comparable product teardowns.

- BOM teardowns: iFixit, Teardown.com, or "[product] teardown BOM" searches
- Component pricing: Digi-Key, Mouser, LCSC (LCSC = closest to Chinese ODM pricing)
- PCBWay / JLCPCB / Seeed Fusion public quotes for PCBA cost at volume
- Common ratios: DTC premium 3-4x COGS, mass retail 2-2.5x COGS.
  If you know retail price of a comparable: COGS ≈ retail × 0.3-0.4 (DTC) or × 0.25-0.35 (mass)
- FCC certification: modular approval $7-18K; full Part 15C $13-39K; CE $5-15K; IC $3-8K
- SaaS COGS: infrastructure = 5-15% of revenue; support = 8-12% of revenue
- SaaS Capital benchmarks: median gross margin 72% (all SaaS), 78% (pure SaaS)
- Volume crossover for hardware: Option A → B at ~1,000-3,000 units; B → C at 20K-100K/yr

---

**For Demand-Side Evidence**

Separate early adopter WTP from primary market WTP. These are almost always different.

- Early adopter WTP trap: early adopters are the most price-tolerant and most vocal in
  communities. Their signals dominate online discussion and almost always undershoot
  viable margin. Name this explicitly. Community sweet spot ≠ mainstream market price.
- Beachhead WTP: found in tech enthusiast communities, Hacker News, Product Hunt
- Primary market WTP: NOT in those communities. Requires survey in non-specialist spaces.
- Van Westendorp Price Sensitivity Meter (four questions for primary market survey):
  1. "At what price would this seem so cheap you'd question the quality?"
  2. "At what price would this seem like a good value?"
  3. "At what price would this start to feel expensive but you'd still consider it?"
  4. "At what price would this be too expensive to consider?"
- Smoke test method: two landing page variants at different price points, measure
  "join waitlist" conversion. 30+ signups per variant minimum for statistical significance.
- Frame in problem language, not technical terms — the framing becomes evidence for the
  pricing narrative.

---

### Round 1 — All Parallel

**Agent: Competitive Price Map**
Question: What does every relevant price point look like — per unit, per family/package?
Find:
- Retail price for every direct competitor (per unit + bundle pricing)
- Pricing for indirect competitors and substitutes (including cost of "do nothing")
- Pricing history: when did competitors raise prices? What triggered it?
- What features are table stakes vs. premium at each price tier?
- The "ceiling" — most expensive comparable product and what justifies it?

**Agent: WTP Signals**
Question: What does external evidence reveal about willingness to pay for this product?
Find:
- Community price signals (explicit price mentions in reviews/forums)
- "Worth it" vs. "overpriced" sentiment patterns and what triggers each
- The no-subscription premium: how much more will customers pay upfront to avoid fees?
  Find quantified evidence, not just assertion.
- Comparable brand pricing cases: 2-3 brands with distinctive pricing decisions

**Agent: COGS Benchmarks**
Question: What is the realistic COGS range at different volume tiers?
Find:
- Component costs for key hardware elements
- BOM teardowns or COGS estimates for comparable products
- Certification cost ranges for the relevant category
- Manufacturing option crossover math: at what volume does each option make sense?
- For SaaS: infrastructure, support, and compliance cost benchmarks by ARR stage

**Agent: Demand-Side Evidence**
Question: What separates early adopter WTP from primary market WTP?
Find:
- Early adopter community price signals (beachhead forums/communities)
- Primary market proxies: non-enthusiast buyer discussions and reviews
- Any published Van Westendorp results for comparable consumer categories
- What framing maximizes perceived value in non-specialist audiences

---

### Saving Research (Between Round 1 and Round 2)

After each Round 1 agent completes, save its full output as a bit before passing to
synthesis:

`create_bit(type: insight, project: [product-name], tags: source-research pricing-strategy [product-name])`

Start each bit's content with `## [Agent Name] — [Project] Research` so the agent is
identifiable in search results. Record the bit IDs and pass them to the Round 2 agent.

---

### Round 2 — After Round 1 Complete

**Agent: Pricing Synthesis**
Does NOT do additional research. Reads all four Round 1 outputs and intake findings.

Produce:
- Confirmed or revised COGS range (with confidence: low/medium/high)
- Margin gate analysis: which GTM motion does the recommended price enable?
- The recommended price with explicit reasoning for why not lower and why not higher
- The price floor (margin-derived, not competition-derived)
- SKU architecture recommendation
- Pricing narrative: how to talk about this price in copy (3 "This NOT That" pairs)
- The validation sequence: what happens to price when which milestones are hit
- The 2-3 biggest risks in this pricing plan

---

### Research Standards

- Cite sources or note the basis for claims.
- If COGS confidence is low (retail-derived proxy, not manufacturing quote), say so.
- If community WTP and primary market WTP diverge, say so explicitly.
- If something contradicts the intake hypothesis, flag it directly.


---

## Phase 3: The Pricing Plan

**Goal:** Produce an opinionated Pricing Plan. Not a range. Not "it depends on your goals."
A number, with reasoning, that the founder can confirm or push back on.

---

### Plan Structure

```
[Business Name] — Pricing Plan
Version: 0.1 (Draft)
Date: [date]
Stage: [idea / prototype / early revenue / scaling]
Recommended Price: [X per unit / Y per SKU]
Price Floor: [X — derived from COGS + margin gate]
Margin at Recommended Price: [X%]
GTM Motion Enabled: [organic-only / limited paid / full marketing mix]
```

---

**THE COGS RANGE**

- Option and volume: [Option A/B/C at X units]
- Hardware/variable cost: [$X per unit]
- Fixed costs amortized: [$X per unit at volume]
- All-in COGS: [$X-Y per unit]
- Confidence level: [low / medium / high] — state the basis
- The one assumption that most affects this number

If COGS confidence is low, say so prominently. The recommendation should hold even if
COGS comes in 20% higher — or flag that it doesn't.

---

**THE MARGIN GATE**

The price floor is derived from margin requirements, not from competition.

> At COGS midpoint of $[X], the margin gates are:
> - Below $[Y]: Below 40% margin. No paid acquisition. Organic-only GTM.
> - $[Y]–$[Z]: 40-50% margin. Limited organic GTM. Can test small paid.
> - $[Z]–$[W]: 50-60% margin. Healthy DTC hardware. Standard marketing mix.
> - Above $[W]: 60%+ margin. Premium tier. Full marketing mix viable.

DTC hardware margin standards:
- Below 40%: Non-viable at scale. CAC eats margin.
- 40-50%: Workable with organic-only GTM (editorial, word-of-mouth, community).
- 50-60%: Healthy. Standard DTC hardware.
- 60%+: Premium tier. Full marketing mix.

SaaS margin standards:
- Below 60%: Health at risk.
- 70-80%: Healthy.
- 80%+: Excellent.

---

**THE PRICE SIGNAL**

Price is a message before the customer reads a word of copy.

> At $[recommended price], the product signals: [what it communicates]
> At $[lower price], the product signals: [what that price communicates instead]
> At $[higher price], the product would signal: [why that's not credible yet]

---

**THE RECOMMENDED PRICE**

> We're recommending $[X per unit / Y per SKU].
>
> Why not lower: [margin falls below gate / signals wrong quality tier / undercuts narrative]
>
> Why not higher: [no brand credibility yet / exceeds primary market WTP / requires
> editorial validation we don't have]
>
> What would change this: [specific validation events that unlock price movement]

---

**THE SKU ARCHITECTURE**

What you sell, how you package it, and which SKU is the product (not the accessory).

- The primary SKU: [what it is, who it's for, why it's primary]
- Secondary SKUs: [what they are, what jobs they do, what price premium they carry]
- What you're explicitly NOT selling as primary SKU: [and why]

For any product whose core promise requires multiple units (mesh networks, family
communication, multi-player games), the bundle is the product — single unit is the
accessory. Selling single units as primary SKU = selling a product that fails its core
promise at first use → generates bad reviews.

SKU naming rules:
- Nothing ending in -Pro, -Plus, -Elite (commoditizes)
- No version numbers in product names (-2, v2 implies v1 is obsolete)
- Nothing that signals the product is a less-complete version of a better thing

---

**THE PRICING NARRATIVE**

Three "This NOT That" pairs, written in the brand's voice.

If a brand brief exists as a bit: load the Voice section before writing these.
The pricing narrative must be consistent with the brand voice.

Required pairs:
1. The primary value comparison (what does this price replace?)
2. The "why this price is fair" statement (cost-of-ownership or savings frame)
3. The category signal (what does this price position the product as?)

> This: "[exact copy — in brand voice]"
> Not That: "[wrong version — what a generic brand would say]"

For products with a "no subscription" promise: make the total cost of ownership
comparison explicit. Show the math.

---

**THE VALIDATION SEQUENCE**

> Launch price: $[X]
> Enabled by: [COGS estimate at current option, organic-only GTM, pre-validation brand]
>
> After [milestone 1 — e.g., editorial validation]:
> Can raise to: $[Y]
> Because: [specific credibility signal]
>
> After [milestone 2 — e.g., volume threshold]:
> COGS improves to: $[Z]
> Which expands margin at current price to: [X%]

---

**THE OPEN QUESTIONS**

> **[Assumption]** — [Why uncertain] → [How to resolve: Van Westendorp / smoke test /
> manufacturer quote / customer interview]

Required open questions for hardware:
- COGS validation: has a manufacturer quote been received?
- Primary market WTP: has the primary market (not the beachhead) been surveyed?

Required open questions for SaaS:
- Infrastructure cost at scale: has the COGS model been validated?
- Support cost: what's the support load per customer?

---

### Plan Tone Standards

- Answer first, evidence second. Recommended price comes before the analysis.
- Opinionated. "$180 is the recommendation" not "the defensible range is $150-180."
- Honest about COGS confidence. Name the difference between proxy and manufacturing quote.
- Specific enough to test. "$180/unit, tested against $150 via landing page split at 30
  signups per variant" is actionable.
- No range as the final answer. Commit to a number, even if provisional.


---

## Phase 4: Iteration

**After presenting the plan:**

1. **Name the weak spots.** "Two things I'm least confident about: [COGS confidence] and
   [primary market WTP]. Let's work through those."

2. **Ask the questions only the founder can answer:**
   - "What does your target customer currently pay for the alternative — full cost: time,
     money, risk of failure?"
   - "What's your gut reaction to the recommended price?"
   - "Have you heard price signals from potential customers — what do they pay for comparable things?"

3. **Push back on anchor bias.** If the founder names a round number ($100, $200, $500):
   "Where did that number come from? Let me run the margin math first."

4. **Validate the pricing narrative.** Read the "This NOT That" pairs aloud: "Does this
   sound like the brand we've described? If a competitor could say this exact thing, it's
   not specific enough."

5. **End when:** The price has a clear floor (margin-derived), a defensible recommendation
   (with reasoning), and the founder can answer "why that price" in two sentences.

---

## Output Standards

The final Pricing Plan should:
- Have a single recommended price, not a range
- Have a derived price floor with explicit margin gate reasoning
- Have a COGS range with confidence level (low/medium/high)
- Have a SKU architecture with a clear primary SKU
- Have a pricing narrative with 3 "This NOT That" pairs in the brand's voice
- Have a validation sequence showing what changes at which milestones

**Saving the plan:** `create_bit(type: note, project: [product-name], tags: pricing-plan [product-name] pricing-strategy)`
Include version number and date in the header. Bump version with each substantive revision.
Include a SOURCE RESEARCH section listing the bit IDs of all Round 1 research bits:

```
SOURCE RESEARCH
  Competitive Price Map: bit [ID]
  WTP Signals: bit [ID]
  COGS Benchmarks: bit [ID]
  Demand-Side Evidence: bit [ID]
```

---

## Connection to Other Skills

**Inputs from business-strategy:**
- COGS hypothesis, competitive landscape, Onliness Statement, Brand Brief Handoff

**Inputs from persona:**
- Four Forces (Push and Anxiety are especially relevant)
- Reference points: what brands does this persona respect and what do those cost?
- Moore archetype: determines the pricing narrative register
- JTBD Statement: the substitute's cost defines the switching cost context

**Outputs to gtm-strategy:**
- Recommended price → ACV hypothesis (feeds motion decision)
- SKU architecture → primary SKU defines the "unit" for CAC/LTV
- Pricing narrative → outreach copy frame

**Outputs to brand-brief:**
- Pricing narrative pairs → candidates for "This NOT That" examples
- SKU architecture decision → Is/Is Not entries

---

## Key Behaviors Summary

**Price is derived, not chosen.** Never accept a founder's target price as the starting
point. Always derive from COGS + margin gate first.

**Name the COGS confidence level.** Retail proxy, manufacturer quote, and teardown are
three different confidence levels. Name which one you're using.

**The community sweet spot almost always undershoots viable margin.** Early adopter
signals dominate online discussion and almost always point below what the mainstream will
pay. Don't let the founder anchor on beachhead WTP.

**The margin gate determines the GTM motion.** Below 40% = no paid acquisition.
This is math, not preference.

**The bundle is the product, not the accessory.** For any product whose core promise
requires multiple units, the bundle is primary.

**The pricing narrative is brand voice applied to numbers.** If a brand brief exists,
check every "This NOT That" sentence against it.

**The validation sequence is not a hedge — it's a plan.** Make the milestones specific.
