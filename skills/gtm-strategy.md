---
name: gtm-strategy
description: >
  Research-backed go-to-market co-pilot for early-stage startups (0–$1M ARR). Takes a
  Strategic Memo (or gathers inputs from scratch), runs parallel research agents across
  beachhead selection, competitive GTM, first-customer patterns, sales motion validation,
  and channel intelligence — then synthesizes into an opinionated GTM Plan with a specific
  motion, channel bets, and a sequenced first-100-customers plan.
  Triggers on: "how do we get first customers", "what's our go-to-market", "let's do GTM
  strategy", "who do we go after first", "how do we launch this", "what's our sales motion",
  "go to market strategy", "how do we find first customers", "let's figure out GTM",
  /gtm-strategy.
---

# GTM Strategy Skill

## What This Is

A research-backed GTM co-pilot for the question business-strategy doesn't answer: we've
made the strategic bet — now who do we go after first, through what motion, and how do we
get the first 100 customers?

This is not a launch checklist. It's a sequenced, opinionated plan with explicit bets on
beachhead, motion, and channels — grounded in how comparable companies actually acquired
their first customers, not generic GTM advice.

The AI does the research and brings the first draft. The founder provides context, challenges
conclusions, and validates the motion against what they know about the space.

**Distinct from business-strategy:** Strategy answers "is this a real opportunity and
what's the bet?" GTM strategy answers "we're making the bet — who do we call first and how?"
Don't run GTM strategy before the core strategic assumptions have been pressure-tested.

**Inputs from business-strategy:** If a Strategic Memo exists with a GTM Handoff block,
load it. This skill doesn't re-derive the Core Bet, ICP, or Onliness Statement — it builds
the execution layer on top.


## When to Invoke

**Auto-trigger on:**
- "how do we get first customers", "what's our go-to-market", "let's do GTM strategy"
- "who do we go after first", "what's our sales motion", "how do we launch this"
- After completing a business-strategy session (natural next step)

**Also useful when:**
- Existing GTM isn't working and needs a reset
- Pivoting the ICP or motion after early evidence
- About to hire a first salesperson and want to verify the playbook exists

**When NOT to invoke:**
- Quick tactical question — just answer it
- Established GTM already working above $2M ARR
- User explicitly says they have a GTM plan and want to execute, not redesign it

**Auto-trigger confirmation:**
> "Want me to run a full GTM strategy on this? I'll research how comparable companies
> acquired their first customers, map the right motion and channels, and produce a
> sequenced first-100-customers plan."

Wait for confirmation. If yes, proceed to Phase 1.


---

## The Phases

```
INTAKE → RESEARCH → MOTION DECISION → GTM PLAN → ITERATE
```

---

## Phase 1: Intake

**Goal:** Establish what we're working with and run a preliminary motion assessment.

**Step 1 — Load from Strategic Memo (preferred path):**

Search for a Strategic Memo: `search_bits(query: "strategic-memo [product]")`
- If found: load the GTM Handoff block — contains Lead Persona, beachhead hypothesis,
  sales motion hypothesis, primary channel bet, why now, and relevant Strategic Bets
- Search for persona bit: `search_bits(query: "persona [product]")`
- Search for brand brief: `search_bits(query: "brand-brief [product]")`
  - If found: load Voice section (VOICE_DO, VOICE_DONT, NEVER_SAY). Hold for outreach copy.
- Confirm: "I found the Strategic Memo. The beachhead hypothesis is [X] and the motion
  hypothesis is [Y]. Does this still reflect your thinking, or has anything changed?"

**Step 2 — Gather fresh (if no Strategic Memo):**

Ask these as a conversation, one at a time:
1. What's the product and who's the customer? (Core Bet in 1-2 sentences)
2. What stage are you at — idea, prototype, early revenue, or scaling?
3. What's the ACV hypothesis — what do you expect to charge annually per customer?
4. Who are the 2-3 competitors, and how are they going to market?
5. What have you already tried for GTM, even informally? What happened?

Don't accept vague answers on ACV — it's the first input to the motion decision.

**Step 3 — Motion pre-assessment:**

Run in order:

*ACV check (Tunguz thresholds):*
- Under $5K ACV: PLG only. Inside sales is economically irrational.
- $5K–$50K ACV: Inside sales or PLG-assisted motion viable.
- $50K–$100K ACV: Field sales becoming required.
- Over $100K ACV: Enterprise sales required.

*Product characteristics check:*
- Can a new user get to clear value in under 15 minutes without help? (PLG signal)
- Does adoption require coordination across a team? (Sales signal)
- Is the buyer also the end user? (PLG = same, Sales = different)
- Does it require IT involvement to implement? (Sales signal)

*Buyer profile check:*
- Can the buyer authorize without procurement involvement? (PLG signal)
- Multiple stakeholders required? (Sales signal)

*Sacks' Difficulty Ratio:*
Low ACV + long sales cycle = economically non-viable. Must shorten cycle or raise ACV.

State a preliminary motion recommendation before research begins.

**Step 4 — Confirm the GTM question:**

GTM question types:
- "Who is the beachhead and how do we win them?" — ICP uncertain
- "Which motion and channel will acquire the first 100 customers fastest?" — motion uncertain
- "Why isn't our current GTM working, and what's the reset?" — stalled GTM
- "When are we ready to hire sales, and what should that person do?" — pre-hire validation


---

## Phase 2: Research

**Goal:** Gather real external evidence across five GTM dimensions. AI runs autonomously.
Come back with findings, not requests for input.

---

### Research Sources by Dimension

**Beachhead & Early Adopter**
- Reddit and GummySearch (gummysearch.com): find where the segment self-organizes. A
  subreddit with 10K+ members discussing this problem = confirmed early adopter community.
- LinkedIn Ads Audience Builder: create a draft campaign targeting by industry + company
  size + job title to get estimated audience size. Free, real-time. Validate beachhead size.
- Job posting trigger signals: "Head of [X] Operations" posted for first time = outgrown
  tooling. Multiple "Coordinator" roles = manual unautomated work.
- G2/Capterra 1-3 star reviews of competitors: what made customers switch? Trigger events
  are usually explicit ("after our team grew past X", "when we started needing Y").
- Moore's beachhead prerequisites: same product for all in segment? Same sales cycle?
  Word-of-mouth community exists? If no WOM path, bowling pin strategy doesn't work here.

**Competitive GTM Intelligence**
- SimilarWeb (free, 3 lookups/day): traffic breakdown by organic/paid/social/referral/direct.
  80% organic = content/SEO primary. 20%+ paid = economics support paid acquisition.
- Facebook Ad Library: search any company for active ads. 90+ day-running ads = working.
  Ad creative reveals messaging and audience targeting.
- LinkedIn headcount: competitor "People" tab → filter by Sales. SDR/BDR = outbound motion.
  Zero salespeople at 20-person company = PLG or community-led.
- Wayback Machine on pricing pages: when did competitors move to "contact sales"?
  When did tiers appear? Shows motion transitions.
- The motion signal matrix: freemium + no salespeople = PLG. "Contact sales" + SDRs = inside
  sales. "Request demo" + Sales Engineers + enterprise case studies = field sales.

**First Customer Patterns**
- First Round Review (review.firstround.com): highest-quality narrative GTM case studies.
  Long-form, named founders, specific tactics. Skews 0–$1M ARR.
- Lenny Rachitsky: "How fastest-growing B2B found their first 10 customers." Pattern from
  30+ companies: personal network dominated, community worked for developer tools,
  cold outbound worked for 3-4 companies with founder iteration on positioning.
- Paul Graham's "Do Things That Don't Scale" — canonical essay on Collison Installation
  and manual early acquisition tactics.
- Autopsy (getautopsy.com): 2,000+ startup failure post-mortems, searchable by sector.
- The 10-unaffiliated-customer test (Aaron Ross): can you get 10 paying customers with
  no prior connection through outreach alone? Warm leads don't validate market viability.

**Sales Motion Validation**
- ACV estimation: competitor pricing pages, OTE method (quota = OTE × 5), G2 review text,
  Vendr buyer guides for verified enterprise contract ranges.
- PLG fit criteria (6 factors from Stage 2 Capital / OpenView): (1) time-to-value < 15 min,
  (2) value communicable via digital ad, (3) end user = decision maker, (4) no IT required,
  (5) large TAM at user level, (6) low gross margin burden from free users.
  Score competitors 0-6. If 3+ score 4+, PLG is proven in the category.
- OpenView PLG benchmarks: 5% free-to-paid conversion (freemium), 17% (free trial).
  Activation rate 25-40% = healthy. Month-3 retention above 20% = strong PMF.
- Leslie's Compass (7 factors): price, market size, complexity, fit & finish, customer
  type, LTV, touch level — each rates as sales-intensive or marketing-intensive.
  All pointing same direction = strong motion signal. Split = Danger Zone.
- Kazanjy stage gate (when to hire first salesperson): 30-50 founder demos, 10-20 paying
  customers, win rate >15%, documented motion. 70% of premature VP Sales hires don't
  make 12 months (SaaStr).

**Channel Intelligence (Balfour's Four Fits)**
- Market-Product Fit, Product-Channel Fit, Channel-Model Fit, Model-Market Fit.
  Channel choice is wrong if any fit is broken.
- Content/SEO: if 3+ competitors rank on category terms, content is proven. Timeline:
  6-12 months to meaningful inbound. Single-channel dependency risk: Tutorspree lost 80%
  of traffic overnight when Google algorithm changed. Company closed 3 months later.
- Community: retention/expansion channel, not a first-customer channel. 12-18 months to
  meaningful impact. Don't build community as your first GTM channel.
- Paid: B2B organic CAC ~$840; paid CAC ~$1,701. Paid is amplifier, not foundation.
  Don't use paid before PMF. Premature scalers spend 2.3x above stage peers on CAC;
  93% never reach $100K monthly revenue.
- Cold outbound: works at ACV $1,000+/month with founder doing it personally.
  Retool's pattern: Crunchbase Pro filter for recently-funded companies + target CTOs.
  First round failed (wrong positioning). Repositioned. Rappi CTO replied in 15 minutes.
  DoorDash was customer #5. $2M ARR before public launch.
  Warm outreach response rates: 10-34%. Cold email: 2-10%.

---

### Round 1 — All Parallel

**Agent: Beachhead & Early Adopter**
Question: In this specific market, who are the early adopters, where do they concentrate,
and what event triggers their active search?
Find:
- Where early adopters self-organize (communities, forums, newsletters)
- Specific trigger events that activate the struggling moment (situational, not demographic)
- Evidence that a word-of-mouth network exists within the target segment
- LinkedIn audience size estimate for the primary beachhead hypothesis
- Moore's criteria assessment: funded buyer, compelling reason, whole product possible,
  no entrenched competition, bowling pin potential?

**Agent: Competitive GTM Intelligence**
Question: How are existing players going to market, and where is the distribution white space?
Find:
- Channel mix for top 3-5 competitors (SimilarWeb traffic breakdown where possible)
- Sales team composition (LinkedIn headcount: SDRs, AEs, SEs)
- Pricing page structures (self-serve vs. contact sales vs. hybrid)
- Active paid advertising (Facebook Ad Library)
- What channels appear consistently (saturated) vs. no competitor using (white space)
- When each competitor moved from PLG to sales-led (pricing page history)

**Agent: First Customer Patterns**
Question: How did companies in this specific space acquire their first 10-100 customers?
Find:
- Named companies with documented first-customer stories in this category or close analogs
- Which acquisition channels appeared in the 0–$1M ARR window
- What the founder's personal role was in early acquisition
- What failed before what worked
- Any "Collison Installation" equivalents — what removed friction between interest and adoption

**Agent: Sales Motion Validation**
Question: What motion dominates in this category, and what does ACV data suggest?
Find:
- ACV estimation for top 3-5 competitors
- PLG fit criteria assessment for competitors (6-criteria checklist)
- Leslie's Compass factors for this category
- Evidence of motion transitions (PLG → enterprise, founder-led → inside sales)
- Any category-specific exceptions to the standard ACV-to-motion mapping

**Agent: Channel Intelligence**
Question: Applying Balfour's Four Fits — what channels have the strongest fit?
Find:
- Content/SEO signal: competitor organic presence, high-intent keyword ranking
- Community signal: active forums, Slack groups, newsletters for target persona
- Outbound signal: competitor SDR presence, evidence of outbound in the space
- Paid signal: competitor paid ads, estimated ACV vs. paid CAC viability
- Viral/PLG signal: freemium presence, shareability, network effects
- Which 3-4 channels have the strongest product-channel fit for this product at this ACV?

---

### Round 2 — After Round 1 Complete

**Agent: GTM Synthesis**
Does NOT do additional research. Reads all five Round 1 outputs and intake findings.

Produce:
- Confirmed or revised motion recommendation (challenge the pre-assessment if warranted)
- The beachhead segment — Moore's criteria applied, sized, with word-of-mouth map
- The channel architecture — primary bet with reasoning, secondary, explicit never
- The first 10 customers — who specifically, how to reach them, what to say
- The first 100 customers — sequencing from 10 to 100, what changes at each threshold
- The 3 biggest risks in this GTM plan
- The founder-led stage gate — when the Kazanjy criteria are likely to be met

---

### Research Standards

- Cite sources or note the basis for claims.
- If motion analysis is split (some signals say PLG, some say sales-led), say so explicitly
  and state which signals you're weighting more heavily and why.
- If comparable-company data is thin, say so.
- If research contradicts the intake hypothesis, flag it directly.


---

## Phase 3: The GTM Plan

**Goal:** Produce an opinionated GTM Plan with explicit bets, names what's uncertain,
and gives a specific sequenced plan for the first 100 customers.

Not a list of options. A bet, with reasoning, that the founder can confirm or push back on.

---

### Plan Structure

```
[Business Name] — GTM Plan
Version: 0.1 (Draft)
Date: [date]
Stage: [idea / prototype / early revenue / scaling]
Beachhead: [one sentence — who, why them first]
Primary Motion: [PLG / founder-led / inside sales / hybrid]
Primary Channel: [the bet]
```

---

**THE BEACHHEAD**

- The segment: [specific — not a demographic, a behavioral/situational profile]
- Why them first: [Moore's criteria applied — compelling reason, whole product achievable,
  no entrenched competitor, bowling pin potential]
- Size: [estimated count × ACV] = beachhead TAM
- Word-of-mouth map: [where this segment talks to each other — conferences, communities,
  peer networks. This is where beachhead dominance propagates]
- The trigger event: [what happens in this segment's world that creates active search]
- The segment we're NOT targeting first: [adjacent segment and explicit reason why not]

The beachhead is won when: 30%+ of new customers are referred by existing customers
within the segment, organic inbound from adjacent segments appears unprompted, and the
sales motion is fully repeatable without founder involvement in positioning.

---

**THE MOTION**

- The motion: [PLG / founder-led / inside sales / hybrid]
- The ACV check: [$X ACV puts this in the [range], maps to [motion]]
- The product check: [self-serve capable? time-to-value? IT involvement?]
- The buyer check: [end user = buyer? procurement involved? multiple stakeholders?]
- Competitive evidence: [what motion are the top competitors using?]
- Leslie's Compass verdict: [do all 7 factors point the same direction?]
- The Danger Zone check: [is ACV aligned with the motion's economics?]

Note: Founder-led sales is not a motion — it's the mandatory starting stage for every
non-PLG product. The motion above is what founder-led transitions into once the playbook
is documented.

---

**THE CHANNEL BETS**

Primary channel:
> We're betting on [channel] as the primary acquisition channel, not [alternative],
> because [specific reasoning grounded in product-channel fit and competitive evidence].

Secondary channel:
> [Channel] as secondary, with the goal of [specific objective].

Explicitly not doing:
> We're not doing [channel] because [reason — economics, no product-channel fit,
> saturated by competitors without our resources].

The single-channel dependency warning: if the primary channel is owned by a third party
(Google, Facebook, App Store), name this risk and state the backup channel.

---

**THE FIRST 100**

*0 → 10: The Validation Phase*

Who to call first — the "Collison Installation" list:
- [5-10 specific companies or roles to approach first]
- Selection criteria: [strongest struggling moment? Known word-of-mouth influence?
  Founder connection that gets a reply?]

How to reach them:
- [Specific approach — LinkedIn + warm intro? Cold email with specific framing?
  Show up at specific event?]
- The message frame: [lead with the push (their struggling moment) or the pull?]
  If a brand brief bit exists: apply Voice section. Outreach copy is the brand voice's
  first real test. If no brief exists, note voice choices here as inputs for a future brief.
- The ask: [demo? 20-minute call? pilot? free trial with goal?]

The Collison Installation equivalent for this product:
- [What can we do to eliminate friction between "interested" and "using it"?]

The 10-unaffiliated-customer test: after the first warm contacts, can we get 10 paying
customers with no relationship to us through outreach alone? Until this passes, we don't
have a GTM motion — we have a warm network.

*10 → 50: The Motion Building Phase*

What changes at this stage:
- Founder still closing but documenting the pattern
- ICP gets tighter with each deal
- Win/loss analysis mandatory: why did we win? Why did we lose?
- Kazanjy stage gate is the milestone: can someone else replicate without founder on call?

Who to target next: [beachhead expansion within the same segment — second-ring targets]

*50 → 100: The Repeatability Phase*

What changes at this stage:
- Motion documented and repeatable without founder
- ICP validated: we know who wins, who churns, who expands
- Channel is compounding or scaling
- First sales hire appropriate if Kazanjy criteria met

The bowling pin decision: at ~100 customers, has the beachhead been won (30%+ referral
rate, organic adjacent inbound, market leadership perception)? If yes: name the next pin.
If no: stay in the beachhead.

---

**THE METRICS**

3-5 leading indicators that tell you if GTM is working before revenue makes it obvious.

- **Qualified conversations per week** — top-of-funnel health
- **Demo-to-qualified-close rate** — is the motion working? (Target: 15-20%+)
- **Time-to-close consistency** — is the motion repeatable?
- **Churn rate from channel-acquired customers** — are you acquiring the right customers?

PLG-specific (if applicable):
- **Activation rate** — Target: 25-40%; below 15% = onboarding problem
- **Free-to-paid conversion** — Target: 17%+ free trial, 5%+ freemium
- **Month-3 retention** — Target: 20%+ for strong PMF

The leading-revenue signal: when referral rate within the beachhead approaches 30%,
the beachhead is compounding. That's the inflection point.

---

**THE STAGE GATE**

Kazanjy criteria (Founding Sales — the standard for sales hire readiness):
- [ ] 30-50 demos run personally by the founder
- [ ] 10-20 paying customers who reached value
- [ ] Win rate >15% on qualified pipeline (>25% = capacity constraint, hire now)
- [ ] Sales motion documented: ICP → engagement → presentation → close → onboard
- [ ] Can answer all four: ICP in one sentence? 3 differentiators? Top 5 objections?

If any criterion fails: do not hire. Fix the underlying problem.

The first hire configuration (after criteria met):
- ACV > $25K + bottleneck is closing capacity → AE first
- ACV < $25K + high inbound needing qualification → SDR first
- ACV < $5K + no repeatable motion yet → growth/PLG hire first

---

**THE EXPANSION PATH**

Beachhead won when:
- 30%+ of new customers referred by existing beachhead customers
- Organic inbound from adjacent segments appearing without outreach
- 5+ referenceable customers who will speak publicly for the brand
- Repeatable motion: predicting conversion rates, consistent close patterns

The next bowling pin:
- Candidate: [adjacent segment with highest Moore adjacency score]
- Why this adjacency: [same product OR same customers; WOM path exists between segments]
- What we carry forward: [credibility, case studies, pricing data, channel learnings]
- What we must rebuild: [messaging, whole product components, channel that don't transfer]

The diagonal move warning: never move to a segment requiring both a new product AND new
customers simultaneously. You lose all leverage.

---

### Plan Tone Standards

- Answer first, evidence second.
- Opinionated. "Use inside sales, not PLG, because [reasons]" not "inside sales or PLG
  depending on your priorities."
- Honest about timing. "This stage gate will likely take 3-4 months" is useful.
- Specific enough to execute. "Target [type] via [channel] with [framing]" is a plan.
- No channel lists. One primary. The rest are secondary or explicitly never.


---

## Phase 4: Iteration

**After presenting the plan:**

1. **Name the weak spots.** "Two things I'm least confident about: [X] and [Y]."

2. **Ask the questions only the founder can answer:**
   - "Who do you know personally in the beachhead who could be customer 1-3? Not 'do you
     know anyone' — who specifically?"
   - "What's your best guess at why the first 3 people you call will say no?"
   - "What does the first version of the product need to do for the customer to succeed
     by their own standards?"

3. **Push back when warranted.** If founder input contradicts research, name the tension.

4. **Test the beachhead against Moore's prerequisites:**
   Same product for all in segment? Same sales cycle? WOM network exists?
   If any fails, beachhead selection needs revision.

5. **Run the 10-unaffiliated-customer test:** "If you couldn't call anyone who knows you,
   what would the approach be? If you don't have a clear answer, we need to work on that."

6. **End when:** Beachhead has a clear WOM map, motion is validated by comparable evidence,
   First 100 plan has specific targets for the first 10, and the founder can state the
   trigger event that activates the struggling moment.

---

## Output Standards

The final GTM Plan should:
- Name a beachhead specific enough to build a list from — not an industry, a situational profile
- Have a motion recommendation grounded in ACV data, not preference
- Have a channel architecture with one primary bet and explicit reasoning for what's excluded
- Have a First 100 plan specific enough the founder knows who to call in the next 72 hours
- Have metrics checkable weekly, not quarterly
- Have a stage gate telling the founder exactly when they're ready to hire sales

**Saving the plan:** `create_bit(type: note, tags: gtm-plan [product-name])`
Include version number and date. Bump version with each substantive revision.


---

## Key Behaviors Summary

**Load the Strategic Memo first.** Don't re-derive the Core Bet or ICP. Start from there.

**ACV is the first input to the motion decision.** Before product characteristics, before
competitive analysis. Low ACV + sales team = Danger Zone. State the economics first.

**Founder-led sales is not a motion — it's a stage.** The GTM plan specifies what it
transitions into once the playbook is documented.

**Name the beachhead specifically enough to pass Moore's three prerequisites.** If the
segment doesn't have a word-of-mouth community, the bowling pin strategy doesn't work.

**One primary channel bet.** Rank one channel as primary, name the second, state what
you're not doing and why. 70%+ of growth comes from one channel when product-channel fit
is found.

**Name the failure modes.** For this specific plan: premature scaling, single-channel
dependency, wrong motion, ICP too broad, premature sales hire — which risk is highest here?

**The First 100 plan must be specific enough to execute tomorrow.** "Target mid-market
SaaS" is not a plan. "Call these 5 companies via [channel] with [framing]" is a plan.

**This skill builds on business-strategy, persona, and brand-brief.** Load the Strategic
Memo, lead persona bit, and brand brief bit before starting. GTM builds on those — it
doesn't re-derive strategy, customer profile, or brand voice.
