---
name: gtm-strategy
description: >
  Research-backed go-to-market co-pilot for early-stage startups. Runs parallel research
  across beachhead selection, competitive GTM, first-customer patterns, and channel
  intelligence, then writes an opinionated GTM plan with a specific motion, channel bets,
  and a sequenced first-100-customers plan. Use when figuring out how to get first
  customers, picking a sales motion, or building a go-to-market from scratch.
---

# GTM Strategy Skill

## What This Is

A research-backed GTM co-pilot for the question business-strategy doesn't answer: we've
made the strategic bet — now who do we go after first, through what motion, and how do we
get the first 100 customers?

This is not a launch checklist. It's not a marketing plan. It's a sequenced, opinionated
plan with explicit bets on beachhead, motion, and channels — grounded in how comparable
companies actually acquired their first customers, not in generic GTM advice.

The AI does the research and brings the first draft. The founder provides context, challenges
conclusions, and validates the motion against what they know about the space.

**Distinct from /business-strategy:** Strategy answers "is this a real opportunity and
what's the bet?" GTM strategy answers "we're making the bet — who do we call first and how?"
These are different questions at different moments. Don't run GTM strategy before the core
strategic assumptions have been pressure-tested.

**Inputs from /business-strategy:** If a Strategic Memo exists with a GTM Handoff block,
load it. This skill doesn't re-derive the Core Bet, ICP, or Onliness Statement — it takes
them as given and builds the execution layer on top.


## When to Invoke

**Auto-trigger on:**
- "how do we get first customers", "how do we find customers"
- "what's our go-to-market", "let's do GTM strategy"
- "who do we go after first", "what's our sales motion"
- "how do we launch this", "let's figure out GTM"
- After completing a /business-strategy session (natural next step)
- /gtm-strategy

**Also useful when:**
- Existing GTM isn't working and needs a reset
- Pivoting the ICP or motion after early evidence
- About to hire a first salesperson and want to verify the playbook exists

**When NOT to invoke:**
- Quick tactical question (how to write a cold email) — just answer it
- Established GTM already working above $2M ARR — this is designed for 0–$1M ARR
- User explicitly says they have a GTM plan and want to execute, not redesign it


## Auto-Trigger Behavior

When this skill auto-triggers, confirm scope before proceeding:

> "Want me to run a full GTM strategy on this? I'll research how comparable companies
> acquired their first customers, map the right motion and channels for this space, and
> produce a sequenced first-100-customers plan."

Wait for confirmation. If they say yes, proceed to Phase 1.


---

## The Phases

```
INTAKE → RESEARCH → MOTION DECISION → GTM PLAN → ITERATE
```

---

## Phase 1: Intake

**Goal:** Establish what we're working with and run a preliminary motion assessment before
any research begins. The motion pre-assessment shapes what the research agents look for.

**Step 1 — Load from Strategic Memo (preferred path):**

Check if a Strategic Memo exists for this product:
- Look for bits with TYPE: memo or TAGS: strategic-memo, or ask the founder
- If found: load the GTM Handoff block — it contains Lead Persona, beachhead hypothesis,
  sales motion hypothesis, primary channel bet, why now, and relevant Strategic Bets
- If a persona file is referenced, load it from docs/personas/[project]/
- Confirm: "I found the Strategic Memo. The beachhead hypothesis is [X] and the motion
  hypothesis is [Y]. Does this still reflect your thinking, or has anything changed?"

**Also check for Brand Brief:**

Look for a bit with TYPE: brief or TAGS: brand-brief for this product.
- If found: load the AI-Readable Layer — specifically VOICE_DO, VOICE_DONT, NEVER_SAY,
  SOUNDS_LIKE. Hold these in context for the message framing in The First 100.
- The outreach copy written in this plan is often the brand voice's first real-world
  expression. It should be consistent with the brand brief, not independently invented.
- If no brief exists: note this. The outreach copy you help write becomes a de facto
  voice sample — the voice that converts is the voice worth documenting in a future brief.

**Step 2 — Gather fresh (if no Strategic Memo):**

Ask these as a conversation, one at a time:

1. What's the product and who's the customer? (Core Bet in 1-2 sentences)
2. What stage are you at — idea, prototype, early revenue, or scaling?
3. What's the ACV hypothesis — what do you expect to charge annually per customer?
4. Who are the 2-3 competitors, and how are they going to market?
5. What have you already tried for GTM, even informally? What happened?

Don't accept vague answers on ACV — it's the first input to the motion decision.
"We'll figure out pricing later" is not an answer. Estimate or model from comparable products.

**Step 3 — Motion pre-assessment:**

Before research, run the motion pre-assessment and state a preliminary hypothesis.
This hypothesis will be refined by research — its purpose is to focus the agents.

Run in order:

*ACV check (Tunguz thresholds — the most reliable prior):*
- Under $5K ACV: PLG only. Inside sales is economically irrational.
- $5K–$50K ACV: Inside sales or PLG-assisted motion viable.
- $50K–$100K ACV: Field sales becoming required; PLG as demand signal only.
- Over $100K ACV: Enterprise sales required.

*Product characteristics check:*
- Can a new user get to clear value in under 15 minutes without help? (PLG signal)
- Does adoption require coordination across a team or department? (Sales signal)
- Is the buyer also the end user, or does someone buy it for others? (PLG = same, Sales = different)
- Does the product require IT involvement to implement? (Sales signal)
- Can the value proposition be explained in a digital ad subject line? (PLG signal)

*Buyer profile check:*
- Can the buyer authorize the purchase without procurement involvement? (PLG signal)
- Multiple stakeholders required to decide? (Sales signal)
- Is the buyer a technical end user (developer, designer, RevOps)? (PLG signal)
- Is the buyer an executive authorizing for a team? (Sales signal)

*Sacks' Difficulty Ratio:*
Low ACV + long sales cycle = economically non-viable. Any business in this quadrant needs
to shorten the cycle or raise ACV before a sales motion works.

State a preliminary motion recommendation:
"Based on [ACV] and [product/buyer characteristics], my preliminary read is [motion].
I'll research what comparable companies in this space are actually doing to confirm or
challenge this."

**Step 4 — Confirm the GTM question:**

After intake, state the question research will answer:
"The question I'm going to answer is: [specific GTM question for this business].
Does that feel right before I start research?"

GTM question types:
- "Who is the beachhead and how do we win them?" — for early stage, ICP is uncertain
- "Which motion and channel will acquire the first 100 customers fastest?" — motion is uncertain
- "Why isn't our current GTM working, and what's the reset?" — for stalled GTM
- "When are we ready to hire sales, and what should that person do?" — for pre-hire validation


---

## Phase 2: Research

**Goal:** Gather real external evidence across five GTM dimensions. AI runs these
autonomously — founder is not involved. Come back with findings, not requests for input.

Use Agent tool to run Round 1 agents in parallel, then Round 2 after all return.

---

### Research Methods & Sources

Every agent should use targeted sources. What follows is the specific lookup hierarchy
for each GTM dimension — what each source is good for, what it can't tell you, and
search patterns that surface signal vs. noise.

---

**For Beachhead & Early Adopter Research**

Goal: Identify where the early adopters in this specific market concentrate, what triggers
their active search, and how to reach them.

*Community mapping — find where they gather:*
- Reddit: `[problem keyword] + "forum" OR "community" OR "slack"` — surfaces where the
  segment self-organizes. A subreddit with 10K+ members discussing this problem is a
  confirmed early adopter community.
- GummySearch (gummysearch.com) — aggregates Reddit pain by subreddit. Use it to find
  which communities have the highest density of the struggling moment.
- LinkedIn groups and newsletters — search `[job title or problem] newsletter` to find
  where this persona gets information.

*LinkedIn Ads Audience Builder — underused for segment sizing:*
- Create a draft campaign, set targeting by industry + company size + job title, and the
  estimated audience size appears in the campaign builder. Free, real-time, specific.
- Use this to validate the beachhead size. Moore's range: $20M–$100M TAM for beachhead.
  If the audience is 5,000 companies × estimated ACV → too small or too large?

*Job posting trigger signals — behavioral ICP signals:*
- Companies posting "Head of [X] Operations" for the first time = function just outgrew
  current tooling. Acute timing signal.
- Companies posting multiple "Coordinator" roles = manual, unautomated workflows. Pain
  is present and growing.
- "Build [X] from scratch" or "establish the [X] function" = no existing solution in place.
- Search: `site:linkedin.com/jobs "[role]" "first" OR "build" OR "0 to 1"`

*Event-based trigger mapping (Moesta's demand-side):*
- The real ICP is not a demographic — it's a struggling moment. Find what event triggers
  active search. Search: `"[problem]" "after" OR "when" OR "because"` in forums/reviews.
- G2/Capterra 1-3 star reviews of competitors — read what made customers switch. The
  trigger events are usually explicit ("after our team grew past X", "when we started
  needing Y").

*Moore's beachhead prerequisites — verify before committing to a segment:*
- Same product: Do all companies in this segment want the same product without variation?
- Same sales cycle: Is the buying process uniform across the segment?
- Word-of-mouth community: Do potential customers in this segment talk to each other?
  (Conferences, associations, Slack communities, peer networks.) If there's no WOM path,
  the bowling pin strategy doesn't work here.

---

**For Competitive GTM Intelligence**

Goal: Map how existing players are actually going to market, what channels they're using,
and where the white space in distribution is.

*Channel mix detection — SimilarWeb (free, 3 lookups/day):*
- Enter any competitor URL — shows traffic breakdown by organic/paid/social/referral/direct.
- A competitor with 80% organic traffic has chosen content/SEO as primary channel.
- A competitor with 40% direct traffic has strong brand recognition or word-of-mouth.
- A competitor with 20%+ paid is spending to acquire — their LTV/CAC math allows it.

*Paid advertising signals — Facebook Ad Library (free, unlimited):*
- facebook.com/ads/library — search any company name to see all active ads.
- Long-running ads (90+ days) = ads that are working and being scaled.
- Ad creative reveals messaging, target audience, and funnel stage being targeted.
- No active ads = not using paid acquisition, or testing hasn't worked.

*Sales motion detection — LinkedIn headcount analysis:*
- Search competitor on LinkedIn → "People" tab → filter by Sales.
- SDR/BDR presence = outbound motion. AE without SDR = founder-led transitioning.
- Sales:Engineering ratio: >1:3 = sales-heavy motion. <1:10 = PLG or founder-led.
- Sales Engineer / Solutions Consultant presence = mid-market ACV requiring demos.
- Zero salespeople at a 20-person company = PLG or community-led motion.

*Pricing page history — Wayback Machine (web.archive.org):*
- Check competitor pricing pages 2-3 years ago. When did they move from self-serve to
  "contact sales"? That transition signals when they moved from PLG to sales-led.
- When did tiers appear? What did they add when they did? (Usually: team features,
  SSO, admin controls = enterprise layer added to PLG base)

*Product Hunt launch history:*
- Search competitor on Product Hunt. Comments on day-1 launch reveal: what community
  they launched through, what worked/didn't in early messaging, who showed up first.
- Products with 500+ upvotes at launch = community-led early acquisition.

*The motion signal matrix — use all three together:*
Low price + freemium tier + no salespeople = PLG confirmed.
"Contact sales" pricing + SDRs + AEs = inside sales confirmed.
"Request a demo" + Sales Engineers + enterprise case studies = field sales confirmed.
Freemium + sales team + enterprise logos = PLG-to-enterprise hybrid in progress.

---

**For First Customer Patterns in This Space**

Goal: Find how companies in this specific category (or close analogs) actually got their
first customers — not generic GTM advice, but named companies with specific tactics.

*Targeted case study search:*
- `"how [named competitor or analog company] got first customers"` — named companies surface
  well in search
- `site:review.firstround.com "[category]" "first customer"` — First Round Review has the
  highest-quality narrative case studies
- `"0 to $1M ARR" [category]` — right stage window, often founder-written
- `"how we got our first 100 customers" [category]` — founder essays
- `site:indiehackers.com "first customers" "[category]"` — honest bootstrapped perspective

*Lenny Rachitsky's research — the most empirically rigorous source:*
- lennysnewsletter.com — "How today's fastest-growing B2B businesses found their first 10
  customers" — covers Stripe, Figma, Retool, Notion, Slack, Asana, Mercury, Gusto.
  Pattern from 30+ companies: personal network dominated (20+/30+), community worked for
  developer tools (HN, IRC, Rails community), cold outbound worked for 3-4 companies but
  required founder doing it personally + iteration on positioning.
- The three-channel hierarchy: personal network first → community second → press/outbound third.
  Channels that appear first aren't always best — they're fastest to first customer,
  not most scalable.

*YC Library and Paul Graham essays:*
- paulgraham.com/ds.html — "Do Things That Don't Scale" — the canonical essay on Collison
  Installation and manual early acquisition tactics
- ycombinator.com/library — filter by Sales + Growth topics for founder-specific advice

*Post-mortems for anti-patterns:*
- getautopsy.com — filter by sector for GTM failure post-mortems
- hn.algolia.com → "what didn't work" OR "failed" → filter type:comment — most honest
  GTM failure content available anywhere

*The 10-unaffiliated-customer test (Aaron Ross):*
Can you acquire 10 paying customers with no connection to you — no friends, colleagues,
family, YC cohort — through your outreach? Warm leads don't validate market viability.
10 cold, paying customers = minimum proof-of-concept for the niche. Search for whether
comparable companies had to pass this test or relied on warm networks indefinitely.

---

**For Sales Motion Validation**

Goal: Confirm or challenge the motion pre-assessment with evidence from comparable companies
in this specific space. Find the ACV-to-motion correlation and any category-specific exceptions.

*ACV estimation for comparable companies:*
- Competitor pricing pages (direct, if public)
- OTE method: standard B2B SaaS quota = OTE × 5. An AE at $150K OTE has ~$750K quota.
  Divide by deals/quarter to estimate ACV. SMB AEs ($110-150K OTE) → ACV $5-25K.
  Mid-market ($140-200K OTE) → $25-100K. Enterprise ($250K+) → $100K+.
- G2/Capterra review text — users mention actual prices in reviews, especially in complaints
- Vendr buyer guides (vendr.com) — actual verified contract ranges

*PLG fit criteria — apply to competitors and to your product:*
Six criteria from Stage 2 Capital / OpenView:
1. Low time-to-retainable value (value in < 15 minutes, ongoing not one-time)
2. Value communicable via digital ads (can explain value in a subject line)
3. End user = decision maker (person using = person buying)
4. Frictionless implementation (no IT involvement to get started)
5. Large TAM at user level (enough individual users to make self-serve scale)
6. Low gross margin burden from free users (infrastructure cost per free user is low)

Score competitors 0-6. If 3+ competitors score 4+, PLG is proven in the category.
If 0 competitors are doing PLG, PLG may not work here.

*OpenView PLG benchmarks (for PLG validation):*
- Freemium: 5% free-to-paid conversion is standard; 17% for free trial
- Month-3 retention below 9% = activation problem; above 20% = strong
- Activation rate of 25-40% = healthy PLG; below 15% = onboarding failure
If you're PLG-leaning and can't hit these with your current product, the motion is wrong.

*Leslie's Compass (First Round Review) — 7 factors:*
Rate each factor as more sales-intensive or marketing-intensive:
1. Price — large economic decision = sales-intensive
2. Market Size — buyers can find you easily = marketing-intensive
3. Complexity — self-serve capability = marketing-intensive
4. Fit and Finish — high post-sale setup = sales-intensive
5. Customer Type — enterprise = sales-intensive; consumer = marketing-intensive
6. Customer LTV — long-term relationship compounding = sales-intensive
7. Touch Level — ongoing relationship required = sales-intensive

If all 7 factors point the same direction: strong motion signal.
If factors are split between sales- and marketing-intensive: Danger Zone.
The Nebula failure case: $275K ACV (sales-intensive) targeting buyers who wanted
plug-and-play simplicity (marketing-intensive) — every factor pointed different directions.

---

**For Channel Intelligence**

Goal: Identify which channels have worked in comparable spaces, apply the Four Fits
framework to this specific business, and map the channel architecture.

*Balfour's Four Fits — the analytical structure:*
The channel decision isn't made independently — it's derived from four interlocking fits:
1. Market-Product Fit: Does the product address the market's actual problem?
2. Product-Channel Fit: Is the product architected for the channel?
   (Virality requires quick time-to-value + broad applicability. Paid requires rapid value
   realization + transactional model. SEO requires user motivation to generate searches.)
3. Channel-Model Fit: Do unit economics support acquisition costs?
4. Model-Market Fit: Does pricing match what the market wants to pay?

The channel choice is wrong if any fit is broken. The Danger Zone: ACV too low to support
sales-driven channels, too high to sustain viral/PLG economics at the stage you're at.

*Content/SEO signals:*
- Ahrefs or Semrush free tier — check if competitors rank on high-intent terms
- If 3+ competitors have active content programs and rank on category terms, content is
  proven as a channel. Time investment: 6-12 months to generate meaningful inbound.
- Content works when: you know who you're writing for (need 10+ paying customers first),
  the problem has search volume, and you can produce better content than existing resources.
- Single-channel dependency risk: if SEO is working, don't let it become the only channel.
  Tutorspree: Google algorithm update killed 80% of traffic overnight, company closed 3 months later.

*Community signals:*
- Community is a retention/expansion channel, not a first-customer channel.
- Best used after PMF to create sustainable growth loop.
- Evidence community works here: active subreddits, newsletters, Slack groups where
  potential customers already discuss the problem. If they exist, community strategy is viable.
- Time to meaningful impact: 12-18 months. Evidence: companies with strong communities
  show 2.1x faster revenue growth, 46% higher LTV, 29% lower churn (B2B community research).
- Don't build community as your first GTM channel.

*Paid acquisition signals:*
- Facebook Ad Library: competitors running paid ads for 90+ days = economics work for them.
  Their ad creative reveals positioning, funnel stage, and audience.
- B2B organic CAC ~$840; paid CAC ~$1,701 (2x). Paid is an amplifier, not a foundation.
- Paid works early for: message testing (small budget, kill what doesn't convert),
  retargeting an already-warm audience, ACV high enough that $1,700 CAC is acceptable.
- Do NOT use paid to fill the top of funnel before PMF. Startup Genome: premature scalers
  spend 2.3x above stage peers on customer acquisition. 93% never reach $100K monthly revenue.

*Cold outbound signals:*
- Works at ACV $1,000+/month with founder doing it personally and iterating on positioning.
- Retool's pattern: Crunchbase Pro + filter for companies that raised in last 6 months +
  target CTOs/VPs of Operations. First round failed (wrong positioning). Repositioned.
  Rappi CTO replied in 15 minutes. DoorDash was customer #5. $2M ARR before public launch.
- Outbound requires: founder doing initial outreach (not a hire), clear ICP, two positioning
  iterations minimum before declaring failure, response rate as signal not conversion rate.
- Warm outreach response rates: 10-34%. Cold email: 2-10%. The gap justifies investing in
  warm network first.

---

### Round 1 — All Parallel

**Agent: Beachhead & Early Adopter**
Question: In this specific market, who are the early adopters, where do they concentrate,
and what event triggers their active search for a solution?
Find:
- Where early adopters in this category self-organize (communities, forums, newsletters)
- What specific trigger events activate the struggling moment (not demographic signals —
  situational/event-based signals)
- Evidence that a word-of-mouth network exists within the target segment
- LinkedIn audience size estimate for the primary beachhead hypothesis
- Moore's criteria assessment: funded buyer, compelling reason, whole product possible,
  no entrenched competition, bowling pin potential?

**Agent: Competitive GTM Intelligence**
Question: How are existing players going to market, and where is the distribution white space?
Find:
- Channel mix for top 3-5 competitors (SimilarWeb traffic breakdown where possible)
- Sales team composition of key competitors (LinkedIn headcount: SDRs, AEs, SEs)
- Pricing page structures (self-serve vs. contact sales vs. hybrid)
- Active paid advertising (Facebook Ad Library)
- What channels appear consistently across competitors (saturated channels)
- What channels no competitor is using (potential white space)
- When each competitor moved from PLG to sales-led (pricing page history)

**Agent: First Customer Patterns**
Question: How did companies in this specific space (or close analogs) acquire their first
10-100 customers?
Find:
- Named companies with documented first-customer stories in this category or adjacent
- Which acquisition channels appeared in the 0–$1M ARR window
- What the founder's personal role was in early acquisition
- What failed before what worked (pre-failure attempts are often underdocumented but
  findable in post-mortems and honest founder essays)
- How long it took to get from 0 to first 10 paying customers in comparable companies
- Any "Collison Installation" equivalents — what did companies do to eliminate friction
  between interest and adoption?

**Agent: Sales Motion Validation**
Question: What motion dominates in this specific category, and what does ACV data suggest
about which motion is viable?
Find:
- ACV estimation for top 3-5 competitors (pricing pages, OTE method, G2 reviews)
- PLG fit criteria assessment for competitors (apply 6-criteria checklist)
- Leslie's Compass factors for this category (what do all competitors suggest about
  the natural sales intensity of this space?)
- Evidence of motion transitions (PLG → enterprise, founder-led → inside sales)
- Any category-specific exceptions to the standard ACV-to-motion mapping

**Agent: Channel Intelligence**
Question: Applying Balfour's Four Fits to this specific business — what channel(s) have the
strongest product-channel fit, channel-model fit, and evidence of working in this space?
Find:
- Content/SEO signal: competitor organic presence, high-intent keyword ranking
- Community signal: active forums, Slack groups, newsletters for target persona
- Outbound signal: competitor SDR presence, evidence of outbound acquisition in the space
- Paid signal: competitor paid ads, estimated ACV vs. paid CAC viability
- Viral/PLG signal: freemium presence, shareability mechanics, network effects
- The Bullseye assessment: which 3-4 channels have the strongest product-channel fit for
  this specific product at this ACV level?

---

### Saving Research (Between Round 1 and Round 2)

After each Round 1 agent completes, save its full output as a bit before passing to
synthesis. Use `write_bit()` from `scripts/lib/create_bit.py`:

- **TYPE:** `insight`
- **ORIGIN:** `ai-extracted`
- **SOURCE TYPE:** `synthetic`
- **SOURCE GROUP:** `ai`
- **CLUSTER:** The project being researched (e.g., "Songbird")
- **TAGS:** `source-research, gtm-strategy, [project-name]`
- **Content header:** Start each bit with `## [Agent Name] — [Project] Research` so
  the agent is identifiable in search results

Record the bit IDs. Pass both the content and bit IDs to the Round 2 synthesis agent.

---

### Round 2 — After Round 1 Complete

**Agent: GTM Synthesis**
This agent does NOT do additional research. It reads all five Round 1 outputs and the
intake findings, and produces a structured strategic recommendation.

Question: Given everything found, what is the specific beachhead, the right motion, the
channel architecture, and the sequenced first-100-customers plan?

Produce:
- A confirmed or revised motion recommendation (challenge the pre-assessment if evidence
  warrants it)
- The beachhead segment — applying Moore's criteria, sized against TAM, with word-of-mouth
  map
- The channel architecture — primary bet with reasoning, secondary, explicit never
- The first 10 customers — who specifically, how to reach them, what to say
- The first 100 customers — sequencing from 10 to 100, what changes at each threshold
- The 3 biggest risks in this GTM plan — specifically what could fail and why
- The founder-led stage gate — when the specific criteria are likely to be met here

This agent produces the GTM opinion. Everything else is inputs.

---

### Research Standards

- Cite sources or note the basis for claims ("based on 4 competitor pricing pages").
- If the motion analysis is split (some signals say PLG, some say sales-led), say so
  explicitly and state which signals you're weighting more heavily and why.
- If the space has thin comparable-company data, say so. Don't invent patterns.
- If research contradicts the intake hypothesis, flag it directly.


---

## Phase 3: The GTM Plan

**Goal:** Produce an opinionated GTM Plan that makes explicit bets, names what's uncertain,
and gives a specific sequenced plan for the first 100 customers.

Not a list of options. Not "PLG or sales-led depending on your priorities." A bet,
with reasoning, that the founder can confirm or push back on.

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

Who to go after first and why them specifically.

- The segment: [specific description — not a demographic, a behavioral/situational profile]
- Why them first: [Moore's criteria applied — compelling reason, whole product achievable,
  no entrenched competitor, bowling pin potential]
- Size: [estimated count from LinkedIn Ads builder or Census/BLS] × [ACV] = beachhead TAM
- Word-of-mouth map: [where this segment talks to each other — conferences, communities,
  peer networks. This is where beachhead dominance propagates]
- The trigger event: [what happens in this segment's world that creates active search]
- The segment we're NOT targeting first: [adjacent segment that's tempting but wrong —
  with explicit reason]

The beachhead is won when: 30%+ of new customers are referred by existing customers
within the segment, organic inbound from adjacent segments starts appearing unprompted,
and the sales motion is fully repeatable without founder involvement in positioning.

---

**THE MOTION**

Which sales motion and why — based on ACV, product characteristics, buyer profile,
and competitive evidence.

- The motion: [PLG / founder-led / inside sales / hybrid]
- The ACV check: [$X ACV puts this in the [range], which maps to [motion]]
- The product check: [self-serve capable? time-to-value? IT involvement?]
- The buyer check: [end user = buyer? procurement involved? multiple stakeholders?]
- Competitive evidence: [what motion are the 3 top competitors using?]
- Leslie's Compass verdict: [do all 7 factors point the same direction?]
- The Danger Zone check: [is ACV aligned with the motion's economics? CAC payback viable?]

If hybrid: specify which motion handles acquisition vs. expansion. Who does what.
If PLG: validate against the 6-criteria checklist. State which criteria are gaps.
If inside sales: state when to hire (Kazanjy stage gate) — not yet if founder hasn't
hit the criteria.

Note: Founder-led sales is not a motion — it's the mandatory starting stage for every
non-PLG product. The motion above is what founder-led transitions into once the playbook
is documented.

---

**THE CHANNEL BETS**

Where we're acquiring customers. Explicit about primary, secondary, and never.

Primary channel:
> We're betting on [channel] as the primary acquisition channel, not [alternative],
> because [specific reasoning grounded in product-channel fit and competitive evidence].

Secondary channel:
> [Channel] as secondary, with the goal of [specific objective — amplification, different
> segment, referral loop].

Explicitly not doing:
> We're not doing [channel] because [reason — economics don't work at this ACV, no
> product-channel fit, competitors have saturated it without our resources].

The single-channel dependency warning: If the primary channel is owned by a third party
(Google, Facebook, App Store), name this risk explicitly and state what the backup channel
is. (Tutorspree: 80% SEO dependency → Google algorithm update → company closed in 3 months.)

---

**THE FIRST 100**

The sequenced plan from 0 to 100 paying customers. Specific enough to execute tomorrow.

*0 → 10: The Validation Phase*

Who to call first — the "Collison Installation" list:
- [5-10 specific companies or roles to approach first, not a generic ICP description]
- Selection criteria: [what makes these the right 10? Strongest struggling moment?
  Known word-of-mouth influence in the beachhead? Founder connection that gets a reply?]

How to reach them:
- [Specific approach — LinkedIn + warm intro? Cold email with [specific framing]?
  Show up at [specific event or community]?]
- The message frame: [based on Moesta's demand-side logic — lead with the push
  (their struggling moment) or the pull (the progress they want)?]
  If a Brand Brief exists: apply VOICE_DO/VOICE_DONT/NEVER_SAY from the AI-Readable
  Layer. Outreach copy is the brand voice's first real test — don't write it in a
  different register from the brief. If no brief exists, note the voice choices here
  as inputs for a future brand brief.
- The ask: [demo? 20-minute call? pilot? free trial with goal?]

The Collison Installation equivalent for this product:
- [What can we do to eliminate friction between "interested" and "using it"?
  What's the unscalable thing that makes the first customer succeed?]

The 10-unaffiliated-customer test:
After the first 5-10 (which may include warm contacts), the test is: can we get 10
paying customers with no relationship to us through outreach alone? Until that test
passes, we don't have a GTM motion — we have a warm network.

*10 → 50: The Motion Building Phase*

What changes at this stage:
- Founder is still closing deals but documenting the pattern
- ICP gets tighter with each deal — what did the 10+ customers have in common?
- Win/loss analysis becomes mandatory: why did we win? Why did we lose?
- The Kazanjy stage gate is the milestone: can someone else replicate this without
  the founder on the call?

Who to target next:
- [Beachhead expansion within the same segment — second-ring targets]
- [How to find them: what the first 10 customers tell us about where the next 40 are]

*50 → 100: The Repeatability Phase*

What changes at this stage:
- Motion is documented and repeatable without founder
- ICP is validated: we know who wins, who churns, who expands
- Channel is either compounding (content, community, referral) or scaling (outbound at
  volume, paid if economics justify it)
- The first sales hire is now appropriate if Kazanjy criteria are met

The bowling pin decision:
At ~100 customers, assess: has the beachhead been won? (30%+ referral rate, organic
adjacent inbound, market leadership perception?) If yes: name the next pin. If no:
stay in the beachhead until word-of-mouth is propagating.

---

**THE METRICS**

3-5 leading indicators that tell you if GTM is working before revenue makes it obvious.
These are the numbers to watch weekly, not monthly.

Format: [Metric] — [What it tells you] — [Target / Signal threshold]

Essential metrics for any motion:
- **Qualified conversations per week** — Are you talking to enough right people?
  (Target: [N] per week based on motion and stage; below this = top-of-funnel problem)
- **Demo-to-qualified-close rate** — Is the motion working?
  (Target: 15-20%+ = viable; below 10% = positioning or ICP problem)
- **Time-to-close consistency** — Is the motion repeatable?
  (Widening variance = ICP drift or deal-by-deal positioning; tightening = repeatability)
- **Churn rate from channel-acquired customers** — Are you acquiring the right customers?
  (Above pre-scaling baseline = selling to wrong customers to hit targets; the Zenefits pattern)

PLG-specific (if applicable):
- **Activation rate** — Do users get to value?
  (Target: 25-40%; below 15% = onboarding problem)
- **Free-to-paid conversion** — Is PLG converting?
  (Target: 17%+ for free trial; 5%+ for freemium; below = value gap or friction)
- **Month-3 retention** — Is the value real?
  (Target: 20%+ for strong PMF; below 9% = product-value problem)

The leading-revenue signal: when referral rate within the beachhead approaches 30%,
the beachhead is compounding. That's the inflection point.

---

**THE STAGE GATE**

When to hire the first salesperson — and what they need to walk into.

Kazanjy criteria (from Founding Sales — the standard for sales hire readiness):
- [ ] 30-50 demos run personally by the founder
- [ ] 10-20 paying customers who onboarded and reached value
- [ ] Win rate >15% on qualified pipeline (>25% = capacity constraint, hire now)
- [ ] Sales motion documented: ICP identification → engagement → presentation → close → onboard
- [ ] Can answer all four: ICP in one sentence? 3 differentiators? Top 5 objections? If
  you stopped selling today, would the next hire know how to win?

If any criterion fails: do not hire. Fix the underlying problem (usually: ICP too broad,
positioning unclear, or product isn't delivering value post-sale).

Premature VP Sales failure rate: 70% don't make 12 months (SaaStr). Root cause: hired
before the playbook existed, expected to figure it out. The founder's job is to create
the playbook, not hire someone to create it.

The first hire configuration (after criteria met):
- ACV > $25K + bottleneck is closing capacity → AE first
- ACV < $25K + high inbound needing qualification → SDR first
- ACV < $5K + no repeatable motion yet → growth/PLG hire first

---

**THE EXPANSION PATH**

When to move beyond the beachhead and what the next segment is.

Beachhead won when (Moore + practitioner consensus):
- 30%+ of new customers referred by existing beachhead customers
- Organic inbound from adjacent segments appearing without outreach
- Referenceable customers: 5+ who will speak at conferences, take peer calls, put name publicly on your brand
- Repeatable motion: predicting conversion rates, consistent close patterns, playbook exists

The next bowling pin:
- Candidate: [the adjacent segment with highest Moore adjacency score]
- Why this adjacency works: [same product OR same customers; word-of-mouth path exists
  between beachhead and next pin; beachhead customers interact with this segment]
- What we carry forward: [the credibility, case studies, pricing data, and channel learnings
  from the beachhead that give us a head start in the adjacent segment]
- What we must rebuild: [what doesn't transfer — messaging, whole product components, channel]

The diagonal move warning: never move to a segment requiring both a new product AND
new customers simultaneously. You lose all leverage. Each expansion should preserve
at least one form of competitive advantage.

---

### Plan Tone Standards

- Answer first, evidence second. The motion recommendation comes before the analysis.
- Opinionated. "Your ACV and product complexity suggest inside sales" is not a recommendation.
  "Use inside sales, not PLG, because [specific reasons backed by evidence]" is.
- Honest about timing. "This stage gate will likely take 3-4 months" is more useful than
  leaving it open-ended.
- Specific enough to execute. "Target [this type of company experiencing this trigger] via
  [this channel] with [this framing]" is a plan. "Target mid-market SaaS" is not.
- No channel lists. Rank one channel as primary. The rest are secondary or explicitly never.
  A list of 8 channels is not a strategy; it's an anxiety response.


---

## Phase 4: Iteration

**Goal:** Refine the plan from first draft into something the founder can start executing
tomorrow. AI drives this — identify the weak spots before the founder has to find them.

**After presenting the plan:**

1. **Name the weak spots.** "Two things I'm least confident about: [X] and [Y]. Let's work
   through those."

2. **Ask the questions only the founder can answer:**
   - "Who do you know personally in the beachhead who could be customer 1-3? Not 'do you
     know anyone' — who specifically?"
   - "What's your best guess at why the first 3 people you call will say no? What's the
     objection you're most worried about?"
   - "What does the first version of the product need to do for the customer to be a
     success by their own standards? What's the Collison Installation equivalent here?"

3. **Push back when warranted.** If the founder's input contradicts research:
   "You said community is the channel, but no competitor in this space has used it
   successfully and the segment has no active community infrastructure. What makes you
   think it works here before the competition?"

4. **Test the beachhead against Moore's prerequisites:**
   - Same product for all companies in the segment?
   - Same sales cycle?
   - Word-of-mouth network exists?
   If any fails, the beachhead selection needs to be revised.

5. **Run the 10-unaffiliated-customer test:** "If you couldn't call anyone who knows you,
   and had to get 10 paying customers through outreach alone — what would the approach be?
   If you don't have a clear answer, we need to work on that before anything else."

6. **End when:** The beachhead has a clear word-of-mouth map, the motion is validated by
   comparable company evidence, the First 100 plan has specific targets for the first 10,
   and the founder can state the trigger event that activates the struggling moment.

**What good iteration looks like:**
- Founder identifies warm network targets for the first 10 → plan gets more specific
- Founder knows of a strong community → community becomes a real channel candidate
- Research turned up a dangerous competitor already in the beachhead → beachhead shifts
- ACV hypothesis changes → motion recommendation may need to change

**What bad iteration looks like:**
- Softening the channel bet because the founder wants to keep options open
- Expanding the ICP when the founder pushes back instead of validating the resistance
- Treating every founder concern as a reason to broaden the plan


---

## Output Standards

The final GTM Plan should:

- Name a beachhead specific enough to build a list from — not an industry, a situational profile
- Have a motion recommendation that's grounded in ACV data, not preference
- Have a channel architecture with one primary bet and explicit reasoning for what's excluded
- Have a First 100 plan specific enough that the founder knows who to call in the next 72 hours
- Have metrics the founder can check weekly, not quarterly
- Have a stage gate that tells the founder exactly when they're ready to hire sales

**File location:** Save as a bit with TAGS: gtm-plan, [product-name]. Include version
number and date in the header. Include a SOURCE RESEARCH section listing the bit IDs
of all Round 1 research bits:

```
SOURCE RESEARCH
  Beachhead & Early Adopter: bit [ID]
  Competitive GTM: bit [ID]
  First Customer Patterns: bit [ID]
  Sales Motion: bit [ID]
  Channel Intelligence: bit [ID]
```

**Versioning:** Each substantive revision bumps version (0.1 → 0.2). The strategy evolves
as evidence comes in — version it so the thinking trail is preserved.


---

## Key Behaviors Summary

**Load the Strategic Memo first.** If a Strategic Memo exists with a GTM Handoff block,
don't re-derive the Core Bet or ICP. Start from there. GTM strategy builds the execution
layer on top of strategy, not alongside it.

**ACV is the first input to the motion decision.** Before product characteristics, before
competitive analysis, before anything. The economics of the motion must work at this ACV.
Low ACV + sales team = Danger Zone. State the economics before recommending.

**Founder-led sales is not a motion — it's a stage.** Every non-PLG product starts here.
The GTM plan specifies what founder-led transitions into once the playbook is documented.
The Kazanjy stage gate is what separates "we're not ready to hire" from "we should hire now."

**Name the beachhead specifically enough to pass Moore's three prerequisites.** If the
segment doesn't have a word-of-mouth community, the bowling pin strategy doesn't work.
If the product varies significantly between companies in the segment, it's not a beachhead.

**One primary channel bet.** A list of channels is not a plan. Rank one channel as primary,
name the second, and state explicitly what you're not doing and why. 70%+ of growth comes
from one channel when product-channel fit is found (Balfour). Design for that reality.

**Name the failure modes.** For this specific plan, which of the five GTM failure patterns
is most likely? Premature scaling, single-channel dependency, wrong motion, ICP too broad,
premature sales hire? State which risk is highest here and what would trigger it.

**The First 100 plan must be specific enough to execute tomorrow.** "Target mid-market SaaS"
is not a plan. "Call these 5 companies via [channel] with [framing] and offer [specific ask]"
is a plan. If the founder reads the First 100 section and doesn't know exactly who to call
in the next 72 hours, the plan isn't done.

**This skill inputs from /business-strategy, /persona, and /brand-brief.** Load the
Strategic Memo, lead persona, and Brand Brief AI-Readable Layer before starting. The GTM
Plan builds on those — it doesn't re-derive the strategy, rebuild the customer profile,
or reinvent the brand voice from scratch.
