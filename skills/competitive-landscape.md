---
name: competitive-landscape
description: >
  Research-backed competitive landscape analysis for new markets, products, and ventures.
  Runs parallel research agents across market players, positioning, product intelligence,
  momentum signals, and customer voice — then synthesizes into a Competitive Landscape Brief
  with positioning maps, threat scorecards, open space analysis, and moat assessment.
  Standalone skill that feeds /business-strategy, /persona, /pricing-strategy, and /gtm-strategy.
  Three modes: discovery (new market), focused (specific product context), refresh (update
  existing analysis). Triggers on: "who are the competitors", "competitive landscape",
  "competitive analysis", "who else is doing this", "what's the competition", "map the market",
  "who are we up against", "what does the competitive landscape look like", /competitive-landscape.
---

> **CLI note:** `create_bit` and `search_bits` references in this skill use `python3 scripts/tterm-tool-client.py <tool> '<args_json>'` when running in Claude Code CLI. In Tink chat they're available natively.

# Competitive Landscape Skill

## What This Is

A research-backed competitive analysis co-pilot that answers the question every other skill
in the strategy stack depends on but none answers deeply: who else is solving this problem,
how are they positioned, what's their trajectory, and where is the open space?

The business-strategy skill has a competitive agent, but it's one of five parallel agents
sharing bandwidth. This skill goes five-deep where that one goes one-deep. It produces a
standalone Competitive Landscape Brief that can be consumed by humans directly or fed into
every other skill in the stack.

The AI does the research autonomously. The founder shapes the framing, validates the
positioning map, and challenges the open space analysis. Competitive intelligence is a
collaborative product: AI brings the data and first-draft analysis; user provides market
intuition, insider knowledge, and strategic judgment.

**Three modes:**
- **Discovery** — "I'm exploring a new market, map everything." Broadest search.
- **Focused** — "I have a specific product concept, who am I up against?" Starts from
  the product and works outward.
- **Refresh** — "Update our competitive picture." Loads a prior brief, finds what changed.

**Feeds downstream skills:**
- `/business-strategy` — Competition section of the Strategic Memo, Core Bet validation
- `/persona` — Competitor user segments inform persona hypotheses, review language reveals JTBD
- `/pricing-strategy` — Competitive price map, substitute pricing, premium/discount patterns
- `/gtm-strategy` — Competitor GTM motions, channel signals, battlecard-ready profiles


## When to Invoke

**Auto-trigger on:**
- "who are the competitors", "who else is doing this", "what's the competition"
- "competitive landscape", "competitive analysis", "map the market"
- "who are we up against", "what does the landscape look like"
- "who competes with X", "compare us to competitors"
- Before starting a /business-strategy session (natural precursor)
- /competitive-landscape

**Also useful when:**
- Entering a new market segment and need to understand who's there
- A new competitor appeared and you need to assess the threat
- Preparing for fundraising and need a defensible competitive slide
- Product strategy decision depends on knowing what others are building
- Existing landscape brief is 3+ months old and needs a refresh

**When NOT to invoke:**
- Quick question about a single specific competitor — just answer it
- User wants a feature comparison spreadsheet — that's product work, not strategy
- Already mid-execution on a validated strategy — competitive monitoring, not analysis
- User explicitly says competition doesn't matter for their decision right now


## Auto-Trigger Behavior

When this skill auto-triggers, confirm scope and mode:

> "Want me to map the competitive landscape here? I'll research who's solving this problem,
> how they're positioned, and where the open space is. Are we doing **discovery** (broad
> market map), **focused** (starting from your product concept), or **refresh** (updating
> a prior analysis)?"

Wait for confirmation. If yes, proceed to Phase 1.


---

## The Phases

```
FRAMING → RESEARCH → LANDSCAPE BRIEF → ITERATE
```

---

## Phase 1: Framing

**Goal:** Establish the competitive question, the market boundaries, and the known
competitors before any research runs. Wrong framing wastes every agent's time.

**Step 1 — Determine the mode:**

If not already clear from the trigger:
- **Discovery:** User is exploring a market. No prior analysis. Start from the problem
  space, not the product.
- **Focused:** User has a product concept or an existing product. Start from what they're
  building and find who else is in the space.
- **Refresh:** A prior Competitive Landscape Brief exists. Load it and find what changed.

For Refresh mode, load the prior brief:
- Search bits for TAGS: competitive-landscape, [product-name]
- Confirm: "I found the landscape brief from [date]. I'll use this as baseline and
  research what's changed. Does it still reflect your understanding, or is anything
  already known to be outdated?"
- Skip to Phase 2 with refresh-specific agent instructions.

**Step 2 — Collect the framing inputs (conversationally, not as a form):**

For Discovery mode:
1. What problem space or market are we mapping? (The job to be done, not the product category)
2. Who has this problem? (The buyer/user — push for specificity)
3. What do you already know about the competitive landscape? (Competitors you're aware of,
   even if only by name)
4. What's driving this analysis? (Entering a new market? Fundraising? Strategic decision?)

For Focused mode:
1. What are you building, in 1-3 sentences? (The product concept)
2. Who's the target customer? (Role, context, pain intensity)
3. Who do you already consider competitors? (Direct and indirect)
4. What's the strategic question this analysis needs to answer?

Don't accept vague market definitions — push for the job:
"When you say 'project management space,' what specific job is the customer hiring for?
'Coordinate a cross-functional team on a deadline' is different from 'track my personal
tasks.' The competitors are completely different for each."

**Step 3 — Define market boundaries:**

Before research, state the boundaries explicitly:
- The job to be done (JTBD framing — competitors are anything hired for this job)
- The buyer profile (who makes the purchase/adoption decision)
- Geographic scope (global, US-only, specific region)
- Market segment (SMB, mid-market, enterprise, consumer)

"Based on what you've described, I'm defining the competitive boundary as: anything a
[buyer profile] would consider when trying to [job]. This includes dedicated products,
adjacent tools, manual workarounds, and doing nothing. Does this feel right, or should
I narrow/broaden?"

**Step 4 — Confirm the competitive question:**

State the specific question research will answer:

Competitive question types:
- "Who is in this space and how is it structured?" — pure discovery, no product yet
- "Where is the open space for our product?" — have a concept, need positioning intel
- "How dangerous is [specific competitor] and what's their trajectory?" — targeted threat assessment
- "What changed in this landscape since [date]?" — refresh mode
- "What's the defensible position in this market?" — moat-oriented analysis

"The question I'm going to answer is: [specific competitive question]. I'll come back
with a complete landscape brief. Sound right?"

Confirm before starting research. This is load-bearing.


---

## Phase 2: Research

**Goal:** Gather real external evidence across five competitive dimensions. AI runs these
autonomously — founder is not involved in this phase. Come back with findings, not requests
for input.

Use Agent tool to run Round 1 agents in parallel, then Round 2 after all return.


---

### The Competitor Taxonomy

Every competitor found gets classified into one of four types. This taxonomy is JTBD-native:
competitors are defined by the job they're hired for, not the product category they belong to.

**Direct competitors** — Same core job, same target buyer, purpose-built product. These are
the obvious category rivals. If someone Googles "[your product category] software," these
show up. Example: Slack vs. Teams for team messaging.

**Indirect competitors** — Different product category, but hired for an overlapping job.
Often more dangerous than direct competitors because they can expand scope. Example:
Notion competes with project management tools even though it's a "workspace."

**Substitutes** — Including "do nothing," spreadsheets, email, manual processes, hiring
someone, or cobbling together free tools. JTBD analysis ALWAYS includes these. Often the
REAL competition — 40-60% of B2B deals are lost to "no decision," not to a competitor.
Example: A family emergency communication app competes with "we'll just text each other."

**Emerging/Adjacent** — Not yet competing but positioned to enter. Signals: adjacent product
with overlapping user base, recent funding in your space, hiring for roles in your domain,
patent filings, beta features that encroach. Example: A note-taking app adding project
management features to compete with Asana.


---

### Research Sources & Methods

What follows is the specific source hierarchy for each competitive dimension — what each
source reveals, reliability level, and search patterns that surface signal.

---

**For Market Players Discovery**

Goal: Find every relevant player across all four competitor types. Cast the net wide.
Missing a competitor is worse than including a marginal one.

*Web search patterns (run all):*
- `"[job to be done]" software OR tool OR platform` — finds direct competitors
- `"[job to be done]" alternative to [known competitor]` — finds indirect competitors
  and substitutes people actually use
- `"[problem keyword]" site:reddit.com "I use" OR "we switched to" OR "we ended up using"`
  — finds substitutes from user behavior, not marketing
- `"[problem keyword]" site:news.ycombinator.com` — finds emerging players and developer
  tools the broader market hasn't noticed yet
- `"[product category]" G2 OR Capterra OR TrustRadius comparison` — finds comparison pages
  that list competitors you might miss
- `"[product category]" "alternative to" site:alternativeto.net` — comprehensive
  alternative listings
- `"[adjacent category]" adding "[your category feature]"` — finds adjacent encroachers

*Crunchbase (if available):*
- Search by category and funding stage — surfaces funded startups not yet visible in SEO
- Look for recent seed/Series A rounds in your category — these are emerging competitors
- Check investor overlap — companies funded by the same investors often target similar markets

*Product Hunt:*
- Search by problem keywords — surfaces early-stage products pre-marketing
- Sort by recent launches — finds new entrants in the last 6-12 months
- Comment threads reveal positioning, early reception, and comparison to alternatives

*App stores (for mobile/consumer products):*
- Search by problem keywords, not product names
- Read "Customers also viewed" sections — reveals competitive sets the market defines

*Job posting signals for emerging competitors:*
- Companies posting roles that reference your product category or adjacent technology
- "We're building the [category] for [segment]" in about-us sections of job posts
- Surge in engineering roles in specific tech stacks that signal a product pivot

---

**For Positioning & Messaging Analysis**

Goal: Understand how each competitor positions themselves — not just what they say, but
who they're talking to, what promise they make, and what they implicitly reject.

*Website analysis (for each competitor):*
- Homepage headline: what promise, in what language, to whom?
- Subheadline: what supporting proof or mechanism?
- Social proof: what customer logos, what testimonials, what metrics?
- Navigation structure: what do they consider primary? (Products, Solutions, Pricing, Resources)
- "About" or "Why us" page: what founding story, what worldview?
- Apply Dunford's lens: what competitive alternative are they positioning against?

*Messaging archaeology (Wayback Machine CDX API):*
- Pull historical snapshots of competitor homepages at 6-month intervals
- Track: when did the headline change? When did they add/drop a feature from the hero?
  When did they shift target audience language?
- Positioning pivots are the most revealing competitive signal — they tell you what the
  market taught the competitor

*Ad copy analysis (Meta Ad Library):*
- Search by company name — see all active ads
- What value proposition do they lead with in paid acquisition?
- What audience signals are in the targeting? (revealed by ad copy language)
- Are they running ads at all? (No ads = organic/PLG motion; heavy ads = paid acquisition)

*Content strategy signals:*
- What topics do they blog about? (Reveals target keywords and audience)
- What webinars/events do they host? (Reveals what segment they're nurturing)
- What comparison pages do they publish? (Reveals who they consider their competition)

*LinkedIn company page:*
- "About" section positioning vs. website positioning (sometimes diverges)
- Content strategy: what do they post? thought leadership vs. product features vs. hiring

---

**For Product & Business Model Intelligence**

Goal: Understand what each competitor actually sells, how they price it, what their
business model is, and what their tech stack signals about their roadmap.

*Pricing intelligence:*
- Public pricing pages — capture current tiers, features per tier, listed prices
- Wayback Machine — pull pricing page snapshots from 6, 12, 18, 24 months ago.
  Track: tier structure changes, price increases, feature tier movements (what got
  pushed from lower to higher tier = monetization signal)
- G2/TrustRadius/Capterra reviews mentioning price — users mention actual prices paid,
  especially in negative reviews ("we were paying $X and they raised it to $Y")
- Vendr buyer guides (vendr.com) — verified enterprise contract ranges for B2B SaaS
- OTE method for B2B: find sales job postings. Standard quota = OTE x 5. A $200K OTE
  AE → ~$1M quota. Divide by deals/quarter to estimate ACV. An SDR's OTE reveals
  whether the motion is transactional or enterprise.
- For hardware: Amazon/retail pricing + eBay sold listings for actual transaction prices

*Product intelligence:*
- Feature pages and documentation — what capabilities do they expose?
- Changelog/release notes — what have they shipped recently? What's the velocity?
- API documentation — what integrations do they prioritize? (Reveals their ecosystem bet)
- Free trial or freemium experience — what do they show first? What's gated?

*Business model signals:*
- Revenue model: SaaS subscription, usage-based, one-time, freemium, marketplace cut?
- Is there a free tier? What's included? (PLG signal)
- Enterprise "contact sales" tier? (Signals upmarket motion and deal size)
- Annual vs. monthly pricing delta — standard 20% discount for annual = normal;
  40%+ = desperate for cash flow commitment

*Tech stack signals from job postings:*
- Engineering roles: what technologies? (Reveals platform, infrastructure, AI investment)
- New roles in areas they didn't hire before (signals pivot or expansion)
- "We're building [X]" language in job descriptions reveals roadmap 6-18 months out

---

**For Momentum & Trajectory**

Goal: Understand where each competitor is going, not just where they are. A weak competitor
gaining momentum is more dangerous than a strong one that's stalled.

*Funding and financial signals:*
- Crunchbase: funding rounds, amounts, investors, valuation (if disclosed)
- Recent funding = runway to execute. Series A in your space = validated market, new rival.
  Series C+ = scaled competitor with distribution advantage.
- Investor identity matters: a16z vs. unknown seed fund signals different trajectories

*Hiring patterns (the strongest leading indicator):*
- LinkedIn headcount: check "Insights" tab for 6-month and 2-year growth rate
- Headcount growth >40% in 6 months = aggressive expansion
- Headcount flat or declining = stalled or pivoting
- WHAT they're hiring for matters more than HOW MANY:
  - Engineering surge = product investment
  - Sales/SDR surge = scaling a motion that's working
  - Marketing surge = brand awareness push (often pre-IPO or post-funding)
  - New function (e.g., first ML engineers) = strategic pivot
  - Executive hires (new CRO, CPO) = strategy shift incoming

*Recent moves (last 12 months):*
- Product launches, major features, platform announcements
- Partnerships and integrations (reveals ecosystem strategy)
- Acquisitions (reveals capability gaps they're buying vs. building)
- Geographic expansion (new offices, new language support)
- Customer wins mentioned in press or case studies

*Likely next moves (inferred):*
- Job posting content = roadmap signal (what they're building next)
- Patent filings = R&D direction (12-18 month leading indicator)
- Conference talks by founders = strategic thinking revealed
- Domain registrations (WHOIS) = potential new product or brand
- Beta features discovered by users = imminent launches

---

**For Customer Voice**

Goal: Understand what actual users think — not marketing claims or feature lists, but
real experience, real frustrations, and real reasons for switching.

*Review platforms:*
- G2, TrustRadius, Capterra — structured reviews with pros/cons/ratings
- Focus on 1-3 star reviews: these reveal genuine pain, switching triggers, and what's
  broken. 5-star reviews are often incentivized or written at peak enthusiasm.
- Look specifically for:
  - "We switched from [competitor] because..." — switching triggers reveal competitive dynamics
  - "The one thing I wish they had..." — unmet needs = open space
  - "We evaluated [competitors] and chose this because..." — decision criteria
  - "We use this alongside [other tool]" — cobbled-together solutions = integration opportunity

*Community discussions:*
- Reddit: `"[competitor name]" site:reddit.com review OR alternative OR "switched from"`
- Hacker News: `"[competitor name]" site:hn.algolia.com` — high quality for dev tools and B2B
- Twitter/X: `"[competitor name]" (love OR hate OR switched OR alternative)` — real-time sentiment
- Product-specific communities: Slack groups, Discord servers, dedicated forums

*Switching behavior (highest signal):*
- G2 "Switched From" data — which competitors lose users to which alternatives
- Reddit threads: "Why I left [competitor]" or "Moving from [X] to [Y]"
- Review sites: "Reasons for switching" fields
- This data directly reveals competitive dynamics in the market

*Sentiment patterns:*
- What do happy users praise most? (Core value proposition validation)
- What do unhappy users complain about most? (Structural weaknesses)
- What do users say about pricing? (WTP signals for /pricing-strategy)
- What segments are most/least satisfied? (By company size, role, use case)


---

### Confidence Labeling

Every finding in the research must carry a confidence label:

- **Verified** — Direct evidence from primary source (pricing page screenshot, SEC filing,
  confirmed announcement, published review). Citable and checkable.
- **Inferred** — Derived from multiple signals that converge (hiring pattern + funding round
  + job posting language = "likely building X"). Reasonable but not confirmed.
- **Estimated** — Reasonable assumption based on limited data, analogies, or single signals.
  Needs validation before building strategy on it.

If a finding would change the strategic recommendation and its confidence is Estimated,
flag it explicitly in the Open Questions section.


---

### Round 1 — All Parallel

**Agent: Market Players Discovery**
Question: Who is in this space — direct competitors, indirect competitors, substitutes,
and emerging/adjacent players?
Find:
- Every company, product, or workaround a [buyer profile] would consider when trying to [job]
- Classify each into the four-type taxonomy (Direct/Indirect/Substitute/Emerging)
- For each: one-line description, target segment, estimated stage (startup/growth/mature)
- Cast the net wide — it's easier to trim than to discover late

**Agent: Positioning & Messaging Analysis**
Question: How does each known competitor position themselves, and what do the patterns reveal
about market structure?
Find:
- Homepage headline and core promise for each competitor
- Target audience language (who are they talking to?)
- Positioning evolution: any major messaging pivots in the last 2 years?
- What competitive alternative each implicitly positions against (Dunford lens)
- Clustering: which competitors say essentially the same thing? Where's the messaging gap?

**Agent: Product & Business Model Intelligence**
Question: What does each competitor sell, how do they price it, and what does their business
model reveal about their strategy?
Find:
- Pricing model, tiers, and listed prices for each competitor
- Revenue model (subscription, usage, one-time, freemium, marketplace)
- Pricing history: price increases, tier restructuring, model changes
- Free tier scope (what's included, what's gated)
- Tech stack and architecture signals from job postings

**Agent: Momentum & Trajectory**
Question: Where is each competitor headed — growing, stalling, or pivoting?
Find:
- Funding history and recent rounds
- Headcount trajectory (6-month and 2-year growth from LinkedIn)
- Recent product launches, partnerships, and acquisitions (last 12 months)
- Hiring patterns that signal strategy (what roles, what volume, what's new)
- Any signals of likely next moves (job posts, patents, beta features, exec talks)

**Agent: Customer Voice**
Question: What do actual users say about these competitors — what works, what's broken,
and why do people switch?
Find:
- Top 3-5 praised strengths per competitor (from reviews, communities)
- Top 3-5 complaints per competitor (from 1-3 star reviews)
- Switching patterns: who loses users to whom, and why?
- Unmet needs mentioned repeatedly across the competitive set
- Sentiment differences by segment (SMB vs. enterprise, technical vs. non-technical)


---

### Saving Research (Between Round 1 and Round 2)

After each Round 1 agent completes, save its full output as a bit before passing to
synthesis. Use `write_bit()` from `scripts/lib/create_bit.py`:

- **TYPE:** `insight`
- **ORIGIN:** `ai-extracted`
- **SOURCE TYPE:** `synthetic`
- **SOURCE GROUP:** `ai`
- **CLUSTER:** The project being researched (e.g., "Songbird")
- **TAGS:** `source-research, competitive-landscape, [project-name]`
- **Content header:** Start each bit with `## [Agent Name] — [Project] Research` so
  the agent is identifiable in search results

Record the bit IDs. Pass both the content and bit IDs to the Round 2 synthesis agent.

---

### Round 2 — After Round 1 Complete

**Agent: Competitive Synthesis**

This agent does NOT do additional external research. It reads all five Round 1 outputs,
the framing context, and any upstream strategic data — and produces structured analysis.

Apply these frameworks to the raw findings:

*Positioning Map:*
- Propose a 2x2 positioning map with two axes
- Axes must reflect buyer decision criteria, not product features
- Axes must represent real tradeoffs (not "good vs. bad")
- Test: "Would a buyer describe their choice in terms of these dimensions?"
- Good axes: self-serve vs. sales-led, point solution vs. platform, simple vs. powerful,
  individual vs. team, general vs. vertical, reactive vs. proactive
- Bad axes: quality (everyone claims it), innovation (unmeasurable), price alone
  (doesn't reveal positioning)
- Plot each competitor on the map. Note clusters and empty quadrants.
- If more than 8 competitors or more than 6 value factors need comparison, produce a
  Strategy Canvas (Blue Ocean) instead of or in addition to the 2x2:
  - X-axis: value factors (price, ease of use, features, support, customization, etc.)
  - Y-axis: investment level (low to high)
  - Each competitor is a line. Where lines cluster = commoditized. Where they diverge
    or where no line exists = differentiation opportunity.

*Threat Assessment:*
Score each Direct and Indirect competitor on five dimensions (1-5 scale):
1. **Market Overlap** — How much do they target the same buyer for the same job?
2. **Resource Advantage** — Funding, team size, distribution, brand recognition
3. **Strategic Intent** — Evidence they're moving toward your space (inferred from signals)
4. **Momentum** — Growth trajectory (hiring, funding, product velocity, market buzz)
5. **Capability Match** — Can they replicate your offering? How quickly?

Composite threat score = weighted average. Weight market overlap and momentum highest —
a well-funded competitor in an adjacent space with no intent to enter yours is not a threat.

*Open Space Analysis:*
Identify gaps across four dimensions:
1. **Underserved segments** — Buyer types no one targets well
2. **Unmet jobs** — Tasks or outcomes existing products handle poorly (from Customer Voice)
3. **Pricing gaps** — Price points with no credible option (from Product Intelligence)
4. **Positioning angles** — Worldviews, values, or narratives no one owns

For each open space: assess why it's empty. Two possibilities:
- **Genuinely underserved** — The market hasn't solved this yet. Opportunity.
- **Structurally unattractive** — Others tried and failed, or the economics don't work.
  Not an opportunity until the structural barrier changes.

Name which one. "Empty quadrant" is not automatically opportunity.

*Moat Assessment (Helmer's 7 Powers):*
For the top 3 competitors and for the user's own position, assess:
1. **Scale Economies** — Does unit cost decline meaningfully with volume?
2. **Network Effects** — Does the product get more valuable as more people use it?
   (Direct vs. cross-side; how strong; multi-homing risk)
3. **Counter-Positioning** — Would adopting the new entrant's model damage the incumbent's
   existing business?
4. **Switching Costs** — What does it cost a customer to leave? (Data, workflow, training,
   integrations)
5. **Brand** — Does the brand command a price premium or lower CAC? (Requires evidence,
   not assertion)
6. **Cornered Resource** — Unique access to talent, data, relationships, IP, or regulatory
   position?
7. **Process Power** — Organizational capabilities that are hard to replicate?

For each: rate current strength (None / Weak / Moderate / Strong) and trajectory
(Building / Stable / Eroding). A weak moat that's building is more strategically
important than a strong moat that's eroding.

Produce:
- Tiered competitor list (Tier 1: top 3-5 threats, Tier 2: rest)
- Positioning map with axis rationale
- Threat scorecard with composite scores
- Open space analysis with attractiveness assessment
- Moat assessment for top competitors and user's own position
- The 2-3 competitors that actually matter and why
- The single most important competitive insight (the one finding that should change
  strategy or validate it)


---

### Research Standards

- Cite sources or note the basis for claims ("based on G2 reviews", "inferred from
  3 job postings on LinkedIn")
- Apply confidence labels (Verified/Inferred/Estimated) to every substantive finding
- If a competitor's positioning or pricing couldn't be determined, say so — don't guess
- If Customer Voice reveals something that contradicts Positioning Analysis, flag it
  explicitly ("they claim X but users say Y")
- If the landscape is thin (few competitors found), say so — "thin competitive landscape"
  is itself a finding (either very early market or wrong search terms)
- Use the FIA framework for actionable findings:
  **Fact** (the verifiable intelligence) → **Impact** (why it matters) → **Action**
  (what to do about it)


---

## Phase 3: The Competitive Landscape Brief

**Goal:** Produce a structured document that gives the founder (and downstream skills)
a complete, opinionated picture of the competitive landscape.

---

### Brief Structure

```
[Market/Product] — Competitive Landscape Brief
Version: 0.1 (Draft)
Date: [date]
Mode: [Discovery / Focused / Refresh]
Competitive Question: [the question framed in Phase 1]
Market Boundary: [the JTBD-defined boundary]
```

---

**THE LANDSCAPE NARRATIVE**

One paragraph. The shape of this market in plain language: who's winning, what's shifting,
where the energy is, and what the structural dynamics are. A new team member reads this
paragraph and understands the competitive environment.

This is not a summary of the sections below — it's the strategic interpretation. It should
contain a point of view: "This market is [consolidating / fragmenting / nascent / mature].
The dominant pattern is [X]. The biggest shift underway is [Y]. The open space is [Z]."

---

**THE COMPETITIVE FIELD**

All competitors found, organized by the four-type taxonomy. For each:

> **[Company Name]** — [Type: Direct/Indirect/Substitute/Emerging] | [Threat Tier: 1/2]
> One-line description. Target segment. Estimated stage. Key differentiator.

Group by type. Within each type, order by threat level (highest first).

Include the "do nothing" / manual workaround as a named substitute. It is always a
competitor and often the primary one.

---

**TIER 1 COMPETITOR PROFILES**

For the top 3-5 competitors (highest threat scores), produce a full profile:

> **[Company Name]**
> **Type:** [Direct/Indirect/Substitute/Emerging]
> **Stage:** [Startup / Growth / Mature / Declining]
> **Positioning:** [Their core promise, in their own language. Source: homepage headline]
> **Target:** [Who they're selling to. Evidence: website language, ad targeting, case studies]
> **Product:** [What they sell. Key capabilities. Architecture if known.]
> **Pricing:** [Model, tiers, listed prices. Confidence: Verified/Inferred/Estimated]
> **GTM Motion:** [How they acquire customers. Evidence: ad presence, sales hiring, PLG signals]
> **Momentum:** [Funding, headcount trajectory, recent moves. Direction: Growing/Stable/Declining]
> **Strengths:** [Top 3, evidence-linked. Source: reviews, market position, capabilities]
> **Weaknesses:** [Top 3, evidence-linked. Source: reviews, gaps, structural limitations]
> **Moat:** [Current moat type and strength per Helmer's 7 Powers]
> **Likely Next Move:** [Inferred from signals. Confidence label.]
> **Why They Matter:** [1-2 sentences: the specific reason this competitor is relevant to YOUR strategy]

Tag each finding with confidence level. If pricing is Estimated or a weakness is Inferred,
say so explicitly.

---

**POSITIONING MAP**

The 2x2 map (or Strategy Canvas if appropriate). Include:
- The two axes with explicit rationale for why these dimensions
- Every competitor plotted (use quadrant labels if helpful)
- Clusters identified and named ("the enterprise cluster," "the PLG cluster")
- Empty quadrants analyzed: underserved opportunity or structurally unattractive?
- Where the user's product would sit (if Focused mode)

If axis selection is uncertain, propose 2 alternative maps with different axes and note
which one reveals more strategic insight. Let the founder choose.

---

**THREAT SCORECARD**

| Competitor | Market Overlap | Resources | Intent | Momentum | Capability | Composite | Tier |
|------------|---------------|-----------|--------|----------|------------|-----------|------|
| Name       | 1-5           | 1-5       | 1-5    | 1-5      | 1-5        | Weighted  | 1/2  |

Weights: Market Overlap (30%), Momentum (25%), Strategic Intent (20%), Resources (15%),
Capability Match (10%). Momentum and overlap matter more than raw resources — a well-funded
company with no intent to enter your space is not a threat.

Below the table: 1-2 sentences per Tier 1 competitor explaining the score.

---

**OPEN SPACE ANALYSIS**

For each identified gap:

> **[Gap Name]** — [Type: Underserved Segment / Unmet Job / Pricing Gap / Positioning Angle]
> **The gap:** [What's missing in the current landscape]
> **Evidence:** [Why we believe this gap exists — review complaints, missing segments, pricing holes]
> **Why it's empty:** [Genuinely underserved OR structurally unattractive? Be honest.]
> **Attractiveness:** [High / Medium / Low — based on market size, accessibility, defensibility]
> **What it would take:** [What you'd need to own this space — product, positioning, GTM]

This section is the most strategically valuable part of the brief. If there's no compelling
open space, say so — "this market is well-covered and the open spaces are structurally
unattractive" is a valid and important finding.

---

**MOAT ASSESSMENT**

For the top 3 competitors:

> **[Company Name]** — Moat Strength: [None / Weak / Moderate / Strong]
> **Primary moat:** [Which of Helmer's 7 Powers, if any]
> **Trajectory:** [Building / Stable / Eroding]
> **What makes it durable (or not):** [1-2 sentences]

For the user's position (if Focused mode):

> **Your Position** — Current Moat: [likely None at early stage]
> **Buildable moat:** [Which power could you build toward?]
> **Timeline:** [When does the moat become real? What has to happen?]
> **Moat dependency:** [What single thing has to be true for the moat to emerge?]

---

**STRATEGIC IMPLICATIONS**

What this competitive landscape means for the user's strategy. This section has a point of
view — it's not neutral.

Format:
> **For positioning:** [What the landscape implies about how to position]
> **For product:** [What to build, what not to build, what to prioritize based on gaps]
> **For pricing:** [What the competitive pricing context implies]
> **For GTM:** [What competitor GTM patterns suggest about viable motions and channels]
> **The single biggest insight:** [The one finding that should change or validate strategy]

---

**OPEN QUESTIONS**

What we couldn't determine from desk research and how to resolve it.

For each:
> **[Assumption]** — [Why uncertain] → [How to validate: customer interviews, trial
> teardown, sales call analysis, win/loss interviews, specific research]

Required open questions:
- Any Tier 1 competitor with Estimated pricing (need real price to compete)
- Any "likely next move" that would significantly change the landscape
- Any open space rated High attractiveness that hasn't been validated with customers
- Missing data that would change the threat scorecard rankings

---

**HANDOFF BLOCKS**

Pre-formatted inputs for downstream skills. Include all that are relevant:

*For /business-strategy (Competition section of Strategic Memo):*
> Landscape summary: [2-3 sentences]
> Top threats: [names and why]
> Open space: [the strongest opportunity]
> Moat hypothesis: [what's buildable]

*For /persona (segment hypotheses):*
> Competitor user segments found: [from Customer Voice — who uses what and why]
> JTBD language from reviews: [exact phrases users use to describe the job]
> Switching triggers: [what causes users to leave competitors]

*For /pricing-strategy (competitive price map):*
> Price points found: [all competitor prices with confidence labels]
> Pricing models in market: [subscription, one-time, freemium, etc.]
> Premium/discount patterns: [what features command premium, what's table stakes]
> Pricing gaps: [price points with no credible option]

*For /gtm-strategy (competitive GTM patterns):*
> Competitor GTM motions: [PLG, inside sales, outbound, community, content]
> Channel signals: [what's working for competitors]
> Competitive messaging angles: [how competitors talk about themselves and each other]


---

### Battlecard Output (Optional Secondary Deliverable)

If the user requests battlecards or if the analysis is being used for sales/fundraising,
produce a one-page battlecard per Tier 1 competitor:

```
[Competitor Name] — Competitive Battlecard
Last Updated: [date]

QUICK FACTS
- Stage: [X] | Funding: [X] | Headcount: [X] | Pricing: [X]

WHY WE WIN
- [Specific advantage with evidence, not generic claim]
- [Specific advantage with evidence]

WHY WE MIGHT LOSE
- [Honest assessment of their strength]
- [Where they're ahead]

WHEN YOU ENCOUNTER THEM
- [In what deal context or buyer journey they appear]
- [What triggers the buyer to compare]

TALK TRACK
- If buyer says "[common objection]": [response]
- If buyer says "[comparison question]": [response]

WHAT'S CHANGING
- [Their trajectory — what to watch for]
```

FIA framework: every line should be Fact (evidence-linked), Impact (why it matters for
a deal), and Action (what to say or do).


---

## Phase 4: Iteration

**Goal:** Refine the brief from first draft into something the founder can defend to an
investor, use for product strategy, or hand to sales.

**After presenting the brief:**

1. **Name the weak spots.** Don't wait for the founder to find them.
   "Two things I'm least confident about: [competitor X's pricing is Estimated, not Verified]
   and [the open space analysis assumes the manual workaround is the primary competitor,
   but I only found 3 data points supporting that]."

2. **Challenge the positioning map.** "I chose [axis 1] and [axis 2] because [reasoning].
   But [alternative axes] could reveal different structure. Does this map match how buyers
   actually think about their options?"

3. **Ask the questions only the founder can answer:**
   - "Which of these competitors do you actually encounter in deals or conversations?
     My threat ranking might be wrong if I'm missing real-world signals."
   - "Is there a competitor or substitute I'm not seeing? Sometimes the real competition
     is invisible to desk research."
   - "Does the open space analysis match your instinct? If not, what am I missing?"

4. **Push back on blind spots.** If the founder dismisses a competitor: "What's your
   evidence that [competitor] isn't a threat? They have [momentum signal] and [capability].
   Are you sure this isn't wishful thinking?"

5. **Validate the moat hypothesis.** "The moat I see you building toward is [X power].
   Is that what you're optimizing for? If not, what structural advantage are you building?"

6. **Test the narrative.** Read the Landscape Narrative paragraph and ask: "If a board
   member or investor asked 'what's the competitive situation?' — does this paragraph
   give them the real answer?"

7. **End when:**
   - Founder can name the top 3 threats and why each matters
   - Positioning map reflects buyer decision criteria (validated by founder)
   - Open space analysis identifies at least one compelling gap (or honestly concludes
     there isn't one)
   - Handoff blocks are populated for downstream skills
   - Open questions are either resolved or flagged as known risks


---

## Refresh Mode

When updating an existing Competitive Landscape Brief:

**What triggers a refresh:**
- 3+ months since last brief (routine cadence)
- New competitor appeared (announced, discovered, encountered in a deal)
- Existing competitor made a significant move (funding, launch, pivot, price change)
- User's own strategy shifted and competitive context needs revalidation
- Preparing for fundraising, board meeting, or strategic decision

**How it works:**

1. Load the prior brief from bits
2. Run abbreviated research agents (same five, but scoped to "what changed since [date]"):
   - Market Players: any new entrants? Any exits/acquisitions?
   - Positioning: any messaging pivots or rebrandings?
   - Product/Pricing: any new features, pricing changes, model shifts?
   - Momentum: any funding rounds, hiring surges, leadership changes?
   - Customer Voice: any sentiment shifts, new complaint patterns?
3. Produce a "What Changed" summary highlighting:
   - New competitors added to the field
   - Threat score changes (with reasoning)
   - Open space changes (gaps that closed or opened)
   - Moat trajectory updates
4. Update the full brief to a new version (0.1 → 0.2, etc.)

**Refresh is not rewrite.** Only update what changed. Stable findings carry forward with
the original confidence labels. Changed findings get new labels and the date of change.


---

## Output Standards

The final Competitive Landscape Brief should:

- Have an opinionated Landscape Narrative (not a neutral summary)
- Have every competitor classified by the four-type taxonomy
- Have Tier 1 profiles with confidence-labeled findings
- Have a positioning map with explicit axis rationale
- Have a scored threat scorecard with composite rankings
- Have open space analysis that honestly assesses attractiveness
- Have a moat assessment using Helmer's 7 Powers
- Have strategic implications specific enough to inform decisions
- Have populated handoff blocks for downstream skills
- Have open questions with specific validation methods

**Saving the brief:** Use `create_bit` with `type: note` and TAGS: competitive-landscape,
[product-name]. Include version number and date in the content header. Include a
SOURCE RESEARCH section listing the bit IDs of all Round 1 research bits:

```
SOURCE RESEARCH
  Market Players: bit [ID]
  Positioning & Messaging: bit [ID]
  Product & Biz Model: bit [ID]
  Momentum & Trajectory: bit [ID]
  Customer Voice: bit [ID]
```


---

## Connection to Other Skills

**Standalone invocation:** Produces the full Competitive Landscape Brief as described.

**Called from /business-strategy:** When the business-strategy skill's Phase 2 competitive
agent runs, it can invoke this skill in Focused mode with the framing from Phase 1. The
Landscape Brief's handoff block feeds directly into the Strategic Memo's "Competition"
section. The open space analysis informs the Core Bet.

**Feeds /persona:**
- Competitor user segments (from Customer Voice) become persona segment hypotheses
- Review language provides real JTBD vocabulary for persona construction
- Switching triggers map to the Four Forces (Push and Pull)

**Feeds /pricing-strategy:**
- Competitive price map (all prices with confidence labels)
- Pricing model prevalence (what's standard in this market)
- Premium/discount patterns (what drives willingness to pay more)
- Pricing gaps (empty price points where no credible option exists)

**Feeds /gtm-strategy:**
- Competitor GTM motions (what's working, what's not)
- Channel intelligence (where competitors acquire customers)
- Competitive messaging angles (how to position against top threats)
- Battlecards (if produced) ready for sales enablement

**Feeds /simulate:**
- Competitor profiles provide the "realistic market response" model
- Threat trajectories inform stress-case scenarios
- Open space analysis provides the "base case" positioning assumption


---

## Key Behaviors Summary

**Competitors are defined by the job, not the category.** A spreadsheet competing for the
same job is a real competitor. An enterprise platform in the same category but serving a
different job is not. JTBD framing is non-negotiable.

**Always include substitutes and "do nothing."** 40-60% of B2B deals are lost to no
decision. The manual workaround is almost always a competitor. If you don't name it,
the analysis has a blind spot.

**Empty space is not automatically opportunity.** An empty quadrant on the positioning map
might be empty because it's structurally unattractive. Always assess WHY it's empty before
calling it an opportunity.

**Confidence labels are mandatory.** A pricing figure from a public page (Verified) and
a pricing figure inferred from an OTE calculation (Estimated) are very different grades
of evidence. Strategy built on Estimated findings needs different risk management than
strategy built on Verified ones.

**Positioning maps require buyer-centric axes.** If the axes don't reflect how buyers
actually make decisions, the map is vanity. "Would a buyer describe their choice in these
terms?" is the test. Founder must validate axis selection.

**Momentum matters more than size.** A 20-person startup growing 40%/quarter with a
recent Series A is more threatening than a 500-person company with flat headcount. Score
trajectory, not just position.

**The Landscape Narrative is the capstone.** If someone reads only one paragraph of the
brief, it should be this one. It must contain a point of view — "the market is [X], the
shift is [Y], the opportunity is [Z]." Neutral summaries are not strategy.

**Refresh is cheaper than rediscovery.** Once you've built the initial brief, updates
are incremental. Design the initial brief with refresh in mind — structured findings
are easier to update than narrative prose.

**Name the most important insight.** Every competitive landscape has one finding that
matters more than the rest — the one that should change strategy or confirm it. Name it
explicitly in Strategic Implications. If you can't name one, the analysis isn't done.

**This skill feeds every downstream skill.** The Landscape Brief is the competitive
foundation for strategy, persona, pricing, GTM, and simulation. Populate every relevant
handoff block. Missing handoff data means downstream skills work with incomplete context.
