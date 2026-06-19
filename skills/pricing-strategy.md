---
name: pricing-strategy
description: >
  Research-backed pricing co-pilot for early-stage hardware and software products. Runs
  parallel research across competitive price maps, willingness-to-pay signals, cost
  benchmarks, and demand-side evidence, then writes a pricing plan with a recommended
  price, tier structure, and customer-facing narrative. Use when figuring out what to
  charge, picking a pricing model, or answering "what's the right price."
---

# Pricing Strategy Skill

## What This Is

A research-backed pricing co-pilot that answers the question /business-strategy doesn't
answer: the strategy is set — now what do we charge, why, and how do we talk about it?

Price is not chosen. It emerges from four interlocking inputs: the COGS floor (what you
must charge to survive), the margin gate (what you must charge to afford your GTM motion),
the competitive context (what the market has already trained buyers to expect), and the
brand signal (what the price communicates about who this is for). Get any of these wrong
and you either lose money or lose customers.

The AI does the research and brings the first draft. The founder provides context,
challenges the margin math, and validates the pricing narrative against what they know
about their customer.

**Distinct from /business-strategy:** Strategy answers whether the opportunity is real
and what the Core Bet is. Pricing strategy answers what you charge, given the bet you've
made. Don't run pricing before the Onliness Statement is resolved — price without position
is just a number.

**Distinct from /gtm-strategy:** GTM answers who to go after first and through what
motion. Pricing feeds GTM — the price point determines which motion is economically viable
(a $99 product cannot support inside sales; a $5K product cannot survive on PLG alone).
Run pricing before GTM if possible; if GTM is already running, use the existing ACV as
a constraint.

**Inputs from upstream skills:**
- `/business-strategy` — Onliness Statement, COGS hypothesis, competitive landscape
- `/persona` — JTBD, switching cost from current solution, price reference points from
  persona's information diet and comparables they trust


## When to Invoke

**Auto-trigger on:**
- "what should we charge", "how do we price this", "what's our pricing strategy"
- "what price point", "pricing model", "price per unit", "how do we think about pricing"
- "what's the right price", "let's figure out pricing", "pricing research"
- "how much should this cost", "is this the right price"
- After completing a /business-strategy session (natural next step)
- /pricing-strategy

**Also useful when:**
- Existing pricing isn't converting and needs a reset
- Entering a new market segment where prior pricing may not hold
- Considering a pricing model change (one-time → subscription, or vice versa)
- Building the financial model for fundraising (price is the input to revenue projections)

**When NOT to invoke:**
- Quick tactical question about a specific number — just answer it
- Established pricing working above $1M ARR — this is designed for pre-launch to $1M ARR
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

**Goal:** Establish the product, COGS hypothesis, and competitive context before research
begins. The COGS hypothesis shapes what the research agents look for.

**Step 1 — Load from upstream skills (preferred path):**

Check if a Strategic Memo exists for this product:
- Look for bits with TYPE: memo, TAGS: strategic-memo, or ask the founder
- If found: load the COGS hypothesis (if present), Onliness Statement, competitive
  landscape, and GTM Handoff block
- Load persona files from docs/personas/[project]/ if they exist
  - From persona: JTBD Statement, Four Forces (Push/Pull/Anxiety/Habit), price reference
    points from the "Reference points" field
- Confirm: "I found the Strategic Memo. The COGS hypothesis is [X] and the competitive
  context is [Y]. Does this still reflect your thinking?"

**Step 2 — Gather fresh (if no Strategic Memo):**

Ask these as a conversation, one at a time:

1. What's the product, and what does it cost to make? (Even a rough estimate: materials,
   manufacturing, shipping, certification. "I don't know" is acceptable — that's what
   research is for.)
2. Who's the primary customer and what are they currently paying for the alternative?
   (The current solution, including "doing nothing," has a cost. That's the switching
   cost context.)
3. What are the 2-3 closest competitors, and what do they charge?
4. Is this a one-time purchase, subscription, or usage-based? Is that fixed, or open?
5. What volume do you expect to sell in year 1? Year 2?

Don't accept vague COGS estimates — push for the specific components:
"When you say $X to make, does that include tooling, certification, packaging, and shipping?
Or just materials?" COGS underestimation is the single most common pricing error.

**Step 3 — COGS pre-assessment:**

Before research, run a rough COGS pre-assessment and state a preliminary floor.

For hardware products, apply the three-tier manufacturing model:
- Option A (source existing certified hardware): fastest to market, highest COGS, no
  tooling cost. COGS = (retail price of nearest comparable) × 0.6-0.7 (wholesale).
- Option B (custom PCB with pre-certified RF/wireless modules): 6-12 month lead time,
  lower COGS at volume, FCC modular approval path ($7-18K). Break-even vs. A at ~2,000-3,000 units.
- Option C (full custom chip-down): 18-24 month cycle, lowest COGS at 25K+ units,
  full certification ($13-39K). Not appropriate pre-PMF.

For software products, apply the SaaS margin standard:
- Infrastructure + support + compliance = the true COGS (not just compute)
- Below 60% gross margin: SaaS health is at risk
- Below 70%: losing room for S&M investment
- 75-80%: healthy SaaS margin

State a preliminary COGS range and price floor:
"Based on [inputs], the COGS range is approximately [X-Y] per unit. At industry-standard
hardware margin of 50-60%, that implies a price floor of [X-Y]. I'll research comparable
manufacturers to pressure-test this."

**Step 4 — Confirm the pricing question:**

After intake, state the question research will answer:
"The question I'm going to answer is: [specific pricing question for this business]."

Pricing question types:
- "What's the right launch price and why?" — for pre-launch products
- "Is our current price working, and if not, why not?" — for launched products with data
- "What does a price increase require to execute?" — for underpriced established products
- "How do we structure the SKU architecture for this family of products?" — for multi-SKU


---

## Phase 2: Research

**Goal:** Gather real external evidence across four pricing dimensions. AI runs these
autonomously. Come back with findings, not requests for input.

Use Agent tool to run Round 1 agents in parallel, then Round 2 after all return.

---

### Research Methods & Sources

---

**For Competitive Price Map**

Goal: Map every price point in the competitive landscape — direct competitors, indirect
competitors, and substitutes (including "do nothing"). This establishes what the market
has already trained buyers to expect.

*Direct competitor pricing:*
- Competitor pricing pages (public) + Wayback Machine history (when did they raise prices?
  when did they add tiers?)
- G2/Capterra review text — users mention actual prices, especially in complaints
  ("we were paying $X and then they raised it to $Y")
- Vendr buyer guides (vendr.com) — verified enterprise contract price ranges
- OTE method for B2B: standard quota = OTE × 5. A $150K OTE AE has ~$750K quota.
  Divide by deals/quarter to estimate ACV.
- Amazon/direct retail for consumer hardware: look for completed/sold listings on eBay
  for secondary market data (what buyers actually paid)

*Substitute pricing (the real competitive set):*
- What does the customer currently do instead? What does that cost?
  - Time cost: how many hours/week does the current workaround take?
  - Money cost: what do they pay for the status quo?
  - Risk cost: what's the cost if the current solution fails at the critical moment?
- The substitute's price is often more load-bearing than direct competitor prices —
  it defines the switching cost the product must clear

*Premium decoding:*
- What features/attributes command the highest prices in this category?
- What attributes are "table stakes" (everyone has them, no price premium)?
- What attributes are priced at a discount (buyers don't value them)?
- G2/Capterra reviews mentioning "worth it" vs. "overpriced" — what drives each verdict?

---

**For WTP Signals**

Goal: Find external evidence of what this specific customer will pay — not what they
say they'll pay, but what their behavior reveals.

*Community research (stated preferences):*
- Reddit: search "[product category] worth it", "[product category] too expensive",
  "[product category] price", "[product category] cheap alternative"
- Filter for comments with high engagement (upvotes = lurker signal)
- Look for: explicit price mentions, price-to-value comparisons, what they switched from
  and at what price, what stopped them from buying
- Van Westendorp language patterns: "I almost bought it but...", "I'd pay up to...",
  "if it were under..."

*Review sentiment mining:*
- 1-3 star reviews mentioning price: "too expensive for what it is", "overpriced compared
  to X" — reveals the price-value mismatch and what the perceived comparable is
- 4-5 star reviews mentioning price: "worth every penny", "surprisingly affordable",
  "saves me $X/year" — reveals the price-value resonance frame

*The no-subscription premium (for subscription vs. one-time pricing decisions):*
- Search: "hate subscription", "subscription fatigue", "one-time purchase prefer"
- Quantifiable: 20-40% upfront premium documented for consumers avoiding subscriptions
  (2024-2025 research; 41% subscription fatigue rate)
- Conditional: the premium is only accessible when trust exists. New brands can't
  command the full premium until they have editorial validation.

*Comparable brand pricing cases:*
- Find 2-3 brands that made a counterintuitive pricing decision and succeeded or failed.
  What did they charge? What did the market do?
- Framework Laptop ($1,049-1,399 for a laptop that can be repaired) — premium for values
- Notion (free personal, paid team) — PLG at a specific price point unlocked a segment
- What analogous brands in adjacent categories have done

---

**For COGS Benchmarks**

Goal: Ground the COGS estimate with real manufacturer data and comparable product teardowns.

*Hardware COGS methods:*
- Bill of Materials (BOM) teardowns: iFixit, Teardown.com, or searching "[product]
  teardown BOM" — reveals component cost structure for comparable products
- Maker community component pricing: component costs for LoRa modules, MCUs, GPS modules,
  batteries from Digi-Key, Mouser, LCSC (LCSC = closest to Chinese ODM pricing)
- PCBWay / JLCPCB / Seeed Fusion public quotes for assembly: gives PCBA cost at volume
- Common COGS ratios for consumer electronics:
  - Typical retail markup: 2-2.5x COGS for mass market, 3-4x for premium DTC
  - If you know the retail price of a comparable product: COGS ≈ retail × 0.3-0.4
    (for DTC premium) or × 0.25-0.35 (for mass retail)
- FCC certification cost ranges: modular approval = $7-18K; full Part 15C = $13-39K;
  CE marking (EU) = $5-15K; IC certification (Canada) = $3-8K

*Software/SaaS COGS methods:*
- Infrastructure cost benchmarks: typical SaaS infrastructure = 5-15% of revenue
  (compute, CDN, storage, third-party APIs)
- SaaS Capital benchmarks: median gross margin 72% (all SaaS), 78% (pure SaaS)
- Support cost benchmarks: 8-12% of revenue for standard B2B SaaS
- ChartMogul reports: COGS by company stage and ACV range

*Volume crossover thresholds:*
- Hardware: when does volume reduce COGS meaningfully?
  - Option A → B crossover: typically 1,000-3,000 units total (amortize tooling)
  - Option B → C crossover: typically 20,000-100,000 units/year
- Software: volume reduces per-unit COGS (infrastructure + support economies of scale)
  - Meaningful improvement typically starts at $1M ARR+ for SaaS

---

**For Demand-Side Evidence**

Goal: Separate Jordan Vale (beachhead early adopter) WTP from Marcus & Priya (primary
market) WTP. These are almost always different — and the primary market WTP is almost
always higher than early adopter WTP.

*The early adopter WTP trap:*
- Early adopters are the most price-tolerant segment for new products — they tolerate
  complexity, incomplete products, and uncertainty for the privilege of being first
- ALSO the most vocal in communities — their price signals dominate online discussion
- BUT: they understate what the mainstream market will pay, because mainstream buyers
  are paying for a complete solution, not a bet on the future
- Community price sweet spot almost always undershoots viable margin. Name this explicitly.

*Separating the two segments:*
- Beachhead (Jordan Vale) WTP: found in tech enthusiast communities, Meshtastic forums,
  r/preppers, Hacker News, Product Hunt
- Primary market (Marcus & Priya) WTP: NOT in those communities. Requires survey
  (Van Westendorp) in non-specialist spaces: r/personalfinance, parenting groups,
  Nextdoor, emergency preparedness subreddits without technical bent

*Van Westendorp Price Sensitivity Meter:*
The four questions to deploy in a survey for the primary market:
1. "At what price would [product] seem so cheap you'd question the quality?"
2. "At what price would [product] seem like a good value?"
3. "At what price would [product] start to feel expensive but you'd still consider it?"
4. "At what price would [product] be too expensive for you to consider?"

Results map to: Acceptable Price Range (between Q1 and Q4), Optimal Price Point (Q2/Q3
intersection), Point of Marginal Cheapness (Q1), Point of Marginal Expensiveness (Q4).

*Smoke test method (behavioral, not stated):*
- Two landing page variants at different price points, identical otherwise
- Measure: "join waitlist" conversion rate, not click-through
- Statistical significance: 30+ signups per variant minimum
- This reveals revealed preference, not stated preference

*Survey framing for non-specialist audiences:*
- Do NOT use technical terms ("LoRa", "mesh network", "Meshtastic-compatible")
- Frame in problem language: "a walkie-talkie that works without cell towers or
  satellites, no monthly fee"
- The frame used in the survey becomes evidence for the pricing narrative

---

### Round 1 — All Parallel

**Agent: Competitive Price Map**
Question: What does every relevant price point in this competitive landscape look like,
per unit and per family/team package?
Find:
- Retail price for every direct competitor (per unit + bundle pricing)
- Pricing for indirect competitors and substitutes (including the cost of "do nothing")
- Pricing history: when did competitors raise prices? what triggered it?
- What features are table stakes vs. premium at each price tier?
- What price points have failed (products that launched and repriced significantly)?
- The "ceiling" — what's the most expensive comparable product, and what justifies it?

**Agent: WTP Signals**
Question: What does external evidence reveal about willingness to pay for this product
and for products like it?
Find:
- Community price signals (explicit price mentions in reviews/forums)
- "Worth it" vs. "overpriced" sentiment patterns and what triggers each
- The no-subscription premium: how much more will customers pay upfront to avoid fees?
  Find quantified evidence, not just assertion.
- Comparable brand pricing cases: 2-3 brands that made a distinctive pricing decision
  and the market response
- Any Van Westendorp-style data published for comparable products

**Agent: COGS Benchmarks**
Question: What is the realistic COGS range for this product at different volume tiers,
and what does the crossover math look like?
Find:
- Component costs for key hardware elements (search LCSC/Digi-Key for comparable specs)
- BOM teardowns or COGS estimates for comparable products
- FCC/CE/IC certification cost ranges for the relevant radio category
- Manufacturing option crossover math: at what volume does Option A → B → C make sense?
- Packaging, enclosure, and logistics cost ranges for comparable DTC hardware
- For SaaS: infrastructure, support, and compliance cost benchmarks by ARR stage

**Agent: Demand-Side Evidence**
Question: What separates early adopter WTP from primary market WTP, and what evidence
exists for the primary market's price tolerance?
Find:
- Early adopter community price signals (beachhead segment forums/communities)
- Primary market proxies: r/personalfinance discussions of comparable purchases,
  consumer preparedness spending patterns, comparable product reviews from non-enthusiast
  buyers
- Any published Van Westendorp results for comparable consumer hardware categories
- Behavioral evidence: price-related conversion patterns (if available)
- What framing maximizes perceived value in non-specialist audiences

---

### Saving Research (Between Round 1 and Round 2)

After each Round 1 agent completes, save its full output as a bit before passing to
synthesis. Use `write_bit()` from `scripts/lib/create_bit.py`:

- **TYPE:** `insight`
- **ORIGIN:** `ai-extracted`
- **SOURCE TYPE:** `synthetic`
- **SOURCE GROUP:** `ai`
- **CLUSTER:** The project being researched (e.g., "Songbird")
- **TAGS:** `source-research, pricing-strategy, [project-name]`
- **Content header:** Start each bit with `## [Agent Name] — [Project] Research` so
  the agent is identifiable in search results

Record the bit IDs. Pass both the content and bit IDs to the Round 2 synthesis agent.

---

### Round 2 — After Round 1 Complete

**Agent: Pricing Synthesis**
This agent does NOT do additional external research. It reads all four Round 1 outputs,
the intake findings, and any upstream persona/strategy data — and forms a pricing opinion.

Question: Given everything found, what is the specific recommended price, the derived
price floor, the SKU architecture, and the pricing narrative?

Produce:
- A confirmed or revised COGS range (with confidence level: low/medium/high)
- The margin gate analysis: which GTM motion does the recommended price enable?
- The recommended price with explicit reasoning for why not lower and why not higher
- The price floor (margin-derived, not competition-derived)
- The SKU architecture recommendation (what to sell, how to package it, which is primary)
- The pricing narrative: how to talk about this price in copy (3 "This NOT That" pairs)
- The validation sequence: what happens to price when which milestones are hit
- The 2-3 biggest risks in this pricing plan

This agent produces the pricing opinion. Everything else is inputs.

---

### Research Standards

- Cite sources or note the basis for claims ("based on 3 competitor retail prices").
- If COGS confidence is low (retail-derived proxy, not manufacturing quote), say so.
- If community WTP and primary market WTP diverge, say so explicitly and note which is
  being used for the recommendation.
- If something contradicts the intake hypothesis, flag it directly.


---

## Phase 3: The Pricing Plan

**Goal:** Produce an opinionated Pricing Plan that makes explicit bets, names what's
uncertain, and gives the founder a specific price to test and a reasoning trail to defend.

Not a range. Not "it depends on your goals." A number, with reasoning, that the founder
can confirm or push back on.

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

What it actually costs to make this, at which volume, with which confidence.

- Option and volume: [Option A/B/C at X units]
- Hardware/variable cost: [$X per unit]
- Fixed costs amortized: [$X per unit at volume]
- All-in COGS: [$X-Y per unit]
- Confidence level: [low / medium / high] — state the basis (quote vs. retail-derived proxy)
- The one assumption that most affects this number: [specific variable — e.g., enclosure
  tooling, FCC certification path, chip pricing at volume]

If COGS confidence is low, say so prominently. A pricing plan built on a bad COGS estimate
is a plan with a hidden flaw. The recommendation should hold even if COGS comes in 20%
higher than estimated — or flag that it doesn't.

---

**THE MARGIN GATE**

The price floor is derived from margin requirements, not from competition.

Format:
> At COGS midpoint of $[X], the margin gates are:
> - Below $[Y]: Below 40% margin. No paid acquisition. Organic-only GTM.
> - $[Y]–$[Z]: 40-50% margin. Limited organic GTM. Can test small paid.
> - $[Z]–$[W]: 50-60% margin. Healthy DTC hardware. Standard marketing mix.
> - Above $[W]: 60%+ margin. Premium tier. Full marketing mix viable.

DTC hardware margin standards (for reference):
- Below 40%: Non-viable at scale. CAC eats margin.
- 40-50%: Workable with organic-only GTM (editorial, word-of-mouth, community).
- 50-60%: Healthy. Standard DTC hardware. Allows limited paid acquisition.
- 60%+: Premium tier. Full marketing mix. Requires strong brand justification.

SaaS margin standards:
- Below 60%: Health at risk. Infrastructure or support cost problem.
- 60-70%: Acceptable. Tight room for S&M investment.
- 70-80%: Healthy. Standard B2B SaaS.
- 80%+: Excellent. Pricing power or low COGS. Can invest heavily in growth.

The price floor is the bottom of the GTM motion the business needs. State it explicitly:
"The price floor is $[X]. Below this, [the motion required] becomes economically irrational."

---

**THE PRICE SIGNAL**

Price is a message. Before the customer reads a word of copy, the price has already
communicated something about who this is for.

Format:
> At $[recommended price], the product signals: [what it communicates — category, quality
> tier, intended user]
> At $[lower price], the product signals: [what that price communicates instead]
> At $[higher price], the product would signal: [what that price communicates — and why
> that's currently not credible for this brand]

The price signal analysis is why "what does the competition charge" is the wrong first
question. The right first question is "what do I want the price to communicate, and is
that consistent with the Onliness Statement?"

---

**THE RECOMMENDED PRICE**

The number. With explicit reasoning for why not lower and why not higher.

Format:
> We're recommending $[X per unit / Y per SKU].
>
> Why not lower: [specific reason — margin falls below gate / signals wrong quality tier /
> undercuts the no-subscription premium narrative]
>
> Why not higher: [specific reason — no brand credibility yet to support this price /
> requires editorial validation we don't have / exceeds primary market WTP without
> a switching cost narrative]
>
> What would change this: [specific validation events that unlock price movement —
> editorial review, volume milestone, beachhead adoption metrics]

---

**THE SKU ARCHITECTURE**

What you sell, how you package it, and which SKU is the product (not the accessory).

Required for every product with more than one SKU:
- The primary SKU: [what it is, who it's for, why it's primary and not secondary]
- Secondary SKUs: [what they are, what jobs they do, what price premium they carry]
- What you're explicitly NOT selling as a primary SKU: [and why — this is a values-revealed-
  through-constraint decision]

For hardware family products (like Songbird):
- If a single unit can't deliver the product's core promise (e.g., mesh requires multiple
  nodes), the bundle is the product — the single unit is the accessory
- Selling single units as primary SKU = selling a product that fails its core promise at
  first use → generates bad reviews → bad reviews in a trust-based brand = category-one
  emergency
- The bundle pricing should reflect the value of the network, not just the unit cost × N

SKU naming rules (from /brand-brief Section 10):
- Nothing ending in -Pro, -Plus, -Elite (commoditizes)
- No version numbers in product names (-2, v2 implies v1 is obsolete)
- Nothing that signals the product is a less-complete version of a better thing

---

**THE PRICING NARRATIVE**

How to talk about the price in copy. Three "This NOT That" pairs, written in the brand's
voice.

If a brand brief exists: load Section 8 (Voice) and Section 11 (AI-Readable Layer) before
writing these. The pricing narrative must be consistent with the brand voice — same register,
same banned phrases, same sentence length pattern.

Required pairs:
1. The primary value comparison (what does this price replace? how does it compare?)
2. The "why this price is fair" statement (the cost-of-ownership or savings frame)
3. The category signal (what does this price position the product as, vs. what it's not)

Format per pair:
> This: "[exact copy — in brand voice]"
> Not That: "[wrong version — what a generic brand would say]"

For products with a "no subscription" architectural promise: the pricing narrative must
make the total cost of ownership comparison explicit. "Own it once" vs. "pay forever"
is not a marketing claim — it's an arithmetic statement. Show the math.

---

**THE VALIDATION SEQUENCE**

Pricing is not static. The right launch price is not the right post-validation price.
Name what changes and when.

Format:
> Launch price: $[X]
> Enabled by: [COGS estimate at Option A/B, organic-only GTM, pre-validation brand]
>
> After [milestone 1 — e.g., Wirecutter/editorial validation]:
> Can raise to: $[Y]
> Because: editorial validation provides the credibility premium that justifies the increase
>
> After [milestone 2 — e.g., 5,000 units sold, Option B tooling amortized]:
> COGS improves to: $[Z]
> Which expands margin at current price to: [X%]
> Or enables price reduction to: $[W] (if market position warrants it)
>
> The price ceiling: $[max] — above this, brand credibility required that doesn't yet exist.
> This becomes achievable when: [specific brand trust signal]

---

**THE OPEN QUESTIONS**

What we don't know yet that most affects the pricing recommendation.

For each:
> **[Assumption]** — [Why uncertain] → [How to resolve: Van Westendorp survey / smoke
> test / manufacturer quote / customer interview]

Required open questions for hardware:
- COGS validation: has a manufacturer quote been received? If not, state confidence level.
- Primary market WTP: has the primary market (not the beachhead) been surveyed?
- FCC certification path: confirmed modular vs. full certification?

Required open questions for SaaS:
- Infrastructure cost at scale: has the COGS model been validated against actual usage?
- Support cost: what's the support load per customer? Has it been measured?

---

### Plan Tone Standards

- Answer first, evidence second. The recommended price comes before the analysis.
- Opinionated. "At current COGS, $150-180 is the defensible range" is not a recommendation.
  "$180 is the recommendation" is. State the number.
- Honest about COGS confidence. Retail-derived proxy is not a manufacturing quote. Name
  the difference.
- Specific enough to test. "Charge more" is not actionable. "$180/unit, tested against
  $150 via landing page split at 30 signups per variant" is actionable.
- No range as the final answer. A range is useful for exploration. The plan must commit
  to a number, even if the number is provisional.


---

## Phase 4: Iteration

**Goal:** Refine the plan from first draft into something the founder can defend to an
investor, a reviewer, or a skeptical customer.

**After presenting the plan:**

1. **Name the weak spots.** "Two things I'm least confident about: [COGS confidence] and
   [primary market WTP]. Let's work through those."

2. **Ask the questions only the founder can answer:**
   - "What does your target customer currently pay for the alternative? Not just the product
     — the full cost: time, money, risk of failure."
   - "What's your gut reaction to the recommended price — too high, too low, or right?
     If wrong, what feels wrong about it?"
   - "Have you heard any price signals from potential customers — not what they said they'd
     pay, but what they do pay for comparable things?"

3. **Push back on anchor bias.** If the founder names a round number ($100, $200, $500)
   as the target: "Where did that number come from? Let me run the margin math and see if
   it actually works, or if we should adjust."

4. **Validate the pricing narrative.** Read the "This NOT That" pairs aloud and ask:
   "Does this sound like the brand we've described? If a competitor could say this exact
   thing, it's not specific enough."

5. **Test the SKU architecture.** "If someone hands a single unit to a family member and
   the family member has nobody to talk to on it — is that a bad first experience? Does
   the SKU architecture reflect that?"

6. **End when:** The price has a clear floor (margin-derived), a defensible recommendation
   (with reasoning), and the founder can answer "why that price" in two sentences without
   referring to notes.

**What good iteration looks like:**
- Founder has a manufacturer quote → COGS model gets more precise, floor moves
- Founder has a community response at a specific price → pricing narrative sharpens
- Research found an unexpected comparable → SKU architecture revisited
- Founder's gut reaction is "too high for launch, but right after Wirecutter" → validation
  sequence gets more specific

**What bad iteration looks like:**
- Softening to a range because the founder wants flexibility (a range is not a plan)
- Lowering the price to match community sweet spot without addressing the margin consequence
- Adding SKUs because the founder wants to serve more segments (more SKUs = more
  confusion for a pre-launch brand)


---

## Output Standards

The final Pricing Plan should:

- Have a single recommended price, not a range
- Have a derived price floor with explicit margin gate reasoning
- Have a COGS range with a confidence level (low/medium/high)
- Have a SKU architecture with a clear primary SKU
- Have a pricing narrative with 3 "This NOT That" pairs in the brand's voice
- Have a validation sequence showing what changes at which milestones
- Have open questions specific enough to action (what survey, what manufacturer, what test)

**File location:** Save as a bit with TAGS: pricing-plan, [product-name]. Include version
number and date in the header. Include a SOURCE RESEARCH section listing the bit IDs
of all Round 1 research bits:

```
SOURCE RESEARCH
  Competitive Price Map: bit [ID]
  WTP Signals: bit [ID]
  COGS Benchmarks: bit [ID]
  Demand-Side Evidence: bit [ID]
```

**Versioning:** Each substantive revision bumps version (0.1 → 0.2). Pricing evolves as
evidence comes in — version it.

---

## Connection to Other Skills

**Inputs from /business-strategy:**
- COGS hypothesis (if present in Strategic Memo)
- Competitive landscape (feeds Competitive Price Map agent)
- Onliness Statement (informs Price Signal analysis — price must be consistent with position)
- Brand Brief Handoff (Enemy = the pricing model being rejected; use in pricing narrative)

**Inputs from /persona:**
- Four Forces: Push (what's broken about current price) and Anxiety (what makes them
  hesitate at the new price) are especially relevant
- Reference points: what brands does this persona respect? What do those things cost?
- Moore archetype: Innovators buy on vision regardless of price; Early Majority need
  proof that this price is worth it. The price narrative differs by archetype.
- JTBD Statement: the job tells you what the substitute is; the substitute's cost
  defines the switching cost context

**Outputs to /gtm-strategy:**
- Recommended price → ACV hypothesis (feeds motion decision: PLG vs. inside sales)
- SKU architecture → primary SKU defines the "unit" for CAC/LTV calculation
- Pricing narrative → outreach copy frame (how the price is introduced in cold email)

**Outputs to /brand-brief:**
- Pricing narrative pairs → candidates for Section 8 "This NOT That" examples
- Price floor rationale → values-revealed-through-constraint entry (Section 7)
- SKU architecture decision → Is/Is Not entries (Section 3)

**When /pricing-strategy runs BEFORE /brand-brief:**
The pricing narrative IS the brand voice's first real-world expression. The register,
sentence length, and framing choices made here become the template for the brand brief.
Note this explicitly: "The pricing narrative we're writing here will be the first real
test of the brand voice. It should be written in the register we want to lock into the
brand brief."

**When /pricing-strategy runs AFTER /brand-brief:**
Load the AI-Readable Layer (Section 11) before writing the pricing narrative. Every
"This NOT That" pair must pass the brand brief voice filter: correct sentence length,
no banned phrases, active voice, second person.

---

## Key Behaviors Summary

**Price is derived, not chosen.** Never accept a founder's target price as the starting
point. Always derive from COGS + margin gate first, then check against competition and WTP.

**Name the COGS confidence level.** Retail-derived proxy, manufacturer quote, and
reverse-engineered teardown are three different confidence levels. A plan built on
a retail proxy with low COGS confidence should say so.

**The community sweet spot almost always undershots viable margin.** Early adopter price
signals dominate online discussion and almost always point below where mainstream buyers
will actually pay. Name this explicitly. Don't let the founder anchor on beachhead WTP.

**The margin gate determines the GTM motion.** Below 40% = no paid acquisition. This is
not a preference — it's math. The GTM motion the business needs must be economically
possible at the recommended price.

**The bundle is the product, not the accessory.** For any product whose core promise
requires multiple units (mesh networks, family communication, multi-player games), the
bundle is primary. Single-unit sales at primary SKU positioning sells a product that
fails its core promise on first use.

**The pricing narrative is brand voice applied to numbers.** Write it in the brand's
register. If a brand brief exists, check every sentence against VOICE_DO, VOICE_DONT,
NEVER_SAY. The copy that explains the price is as load-bearing as the price itself.

**The validation sequence is not a hedge — it's a plan.** "We'll raise prices later" is
a hedge. "We'll raise from $150 to $200 after the first Wirecutter review, which we're
targeting via [specific outreach plan]" is a plan. Make the sequence specific.

**This skill feeds /gtm-strategy and /brand-brief.** The recommended price is the ACV
input to the GTM motion decision. The pricing narrative pairs are candidates for the brand
brief's "This NOT That" section. Design both outputs with those consumers in mind.

---

## Saving the Plan

Save as a bit with:
- `TYPE: note`
- `CLUSTER:` [relevant cluster for this product]
- `TAGS: pricing-plan, [product-name], pricing-strategy`
- Version field in content: `Version: 0.1 | [date]`

The Pricing Plan is a living document — version it as COGS, validation, and market
evidence comes in.
