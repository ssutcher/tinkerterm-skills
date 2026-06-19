---
name: business-strategy
description: >
  Research-backed strategic co-pilot for a startup idea. Runs parallel research across
  market, competition, customer, business model, and GTM, then writes an opinionated
  memo with explicit bets and open questions. Use when evaluating a new idea, validating
  a market, building a strategy from scratch, or when the user shares an idea and asks
  "what do you think."
---

# Business Strategy Skill

## What This Is

A research-backed strategic co-pilot for startup ideas. Not a business plan generator.
The output is a strategic memo — a short, opinionated document that makes explicit bets,
names what's uncertain, and gives the team directional clarity. Built to be read by both
humans and AIs.

The AI's job is to guide the team through what's needed to complete the document —
driving the research, the synthesis, the iteration, and the decisions. The document
itself is not a task list; it's a strategic position.

The AI does the research. The founder provides the raw material and shapes the output.
Strategy is a collaborative product: AI brings the research, analysis, and first drafts;
user refines the framing, challenges the conclusions, and signs off.


## When to Invoke

**Auto-trigger on:**

Direct invocations:
- "create a business strategy", "build a strategy", "run a strategy on this"
- "I want a strategy for X", "let's do a business strategy"
- /business-strategy

Idea-sharing triggers:
- User shares a new startup idea or product concept
- "What do you think about this idea?"
- "I'm thinking of building X"
- "Is there a market for X?"
- "Should I pursue this?"
- "We're considering X as a business"
- User describes a problem they want to solve commercially

**Also invoked via:** /business-strategy

**When NOT to invoke:**
- User is already mid-execution on a known strategy — they need a story, not a strategy
- Quick tactical question about an existing business — just answer it
- User explicitly says they don't want a strategy session right now


## Auto-Trigger Behavior

When this skill auto-triggers, don't dive into intake immediately. Open with:

> "Want me to run a full strategy on this? I'll research the market, competition, and
> business model — then pull it together into a strategic memo we can work from."

Wait for confirmation. If they say yes, proceed to Phase 1.
This prevents the skill from hijacking casual idea mentions.


---

## The Four Phases

```
FRAMING → RESEARCH → SYNTHESIS → [PERSONAS] → MEMO → ITERATE
```

---

## Phase 1: Framing

**Goal:** Establish what question the strategy needs to answer and collect the raw
material for research. This shapes everything downstream — wrong framing = wrong research
= useless document.

**Collect these inputs from the founder:**

1. **The idea** — what is it, in 1-3 sentences. What does it do, for whom.
2. **The customer** — who you think is suffering from this problem. Be specific if you can.
3. **Stage** — idea / prototype (built but no users) / early revenue / scaling
4. **What you already know** — anything validated, researched, or strongly believed about
   this market. Include assumptions you're operating on.

Optional but valuable:
- What you're most uncertain about
- What decision this strategy needs to support (fundraising? build vs. buy? pivot?)

**AI behavior in this phase:**
- Ask these as a conversation, not a form. One or two at a time.
- Don't accept vague answers on the customer — push for specificity.
  "Who exactly? What role, what context, what pain intensity?"
- After collecting inputs, propose the strategic question being answered:
  "Based on this, the question I'm going to answer is: [X]. Does that feel right?"
- Confirm before starting research. This is load-bearing.

**The strategic question types:**
- "Is this a real opportunity and how big?" — use for early-stage idea validation
- "How do we win in this market?" — use when the idea is validated, strategy is the question
- "What's the strongest version of this business?" — use when pivoting or refining
- "Should we build this or is there a better path?" — use for build/buy/partner decisions


---

## Phase 2: Research

**Goal:** Gather real external knowledge across five strategic dimensions. AI runs these
autonomously — founder is not involved in this phase.

Research is not exploratory browsing. Each agent has a specific question it's answering.
Use Agent tool to run Round 1 agents in parallel, then Round 2 after all return.

---

### Research Methods & Sources

Every agent should use targeted sources, not generic web searches. What follows is the
specific lookup hierarchy for each dimension — including what each source is actually
good for, what it can't tell you, and search patterns that surface signal vs. noise.

---

**For Problem & Customer**

Goal: Find evidence the problem is real, who has it worst, and what they currently do.

*Where real pain actually shows up:*

Reddit — the highest-signal free source for unfiltered pain. Key patterns:
- `site:reddit.com "[problem keywords]"` — surfaces threads across all subreddits
- `site:reddit.com/r/[industry] "[problem]"` — scoped to the right community
- Search for: "I wish there was", "anyone else dealing with", "is there a tool that",
  "we've been using spreadsheets", "our current solution is terrible"
- What "real pain" looks like vs. noise: real pain has specificity (names the workaround,
  describes the frequency, quantifies the cost), frustration (multiple upvotes, "same here"
  comments), and recurrence (multiple threads over time, not one viral complaint)
- GummySearch (gummysearch.com) aggregates Reddit pain signals by subreddit — useful for
  scanning without writing search queries

G2 and TrustRadius — for extracting pain from competitor reviews:
- TrustRadius is more reliable than G2: publishes only 52% of submitted reviews after
  verification, averages 400 words per review, does not allow review gating. G2 is larger
  but reviews are often incentivized (gift cards) which inflates positive sentiment.
- Tactic: Read 1-3 star reviews specifically. Disgruntled users aren't writing for gift
  cards. These are the most honest signal of what's broken.
- Search: `site:g2.com "[competitor name]" reviews` or browse category pages directly
- Also useful: what reviewers say they use as workarounds ("we export to Excel and...")

App Store / Play Store — for mobile-adjacent products:
- 1-2 star reviews with substantive text are gold
- Look for patterns across reviews, not individual complaints
- Review count is a rough proxy for installs (1-3% of users leave reviews)

AnswerThePublic (answerthepublic.com) — surfaces questions people ask Google about a topic.
- Free tier: 3 searches/day — use them on precise seed keywords
- Use the "Questions" and "Prepositions" views for pain research
- Best for consumer problems; less useful for niche B2B

Hacker News (hn.algolia.com) — high quality for developer tools, infra, and technical
B2B problems. Search for the problem keyword filtered to "Ask HN" or "stories." Comments
are often more valuable than the posts themselves.

Job postings as pain signals — underused and highly specific:
- A company posting "Head of [function] Operations" signals they've outgrown their current
  process and are building for the first time
- A company posting multiple "Coordinator" roles in a function = manual, unautomated work
- "We're looking for someone to own [X] from scratch" = no existing solution in place

Industry-specific forums — find them via: `[industry] + "forum" OR "community" OR "slack"`
or look at what subreddits exist around the problem space.

*What NOT to use:* Trustpilot for B2B software (serious fake review problems, fined by
regulators). Quora for recent/active pain — it's stale for most technical B2B topics.

---

**For Competitive Landscape**

Goal: Map who's solving this, how they're positioned, where the open space is, and
what their weaknesses are.

*Category discovery:*
- Google: `[problem] software`, `[problem] tools`, `[problem] platform`
- G2 category pages — shows all products in a defined category with review counts.
  A category with 3 products and 200 reviews is nascent; 400 products and 50k reviews
  is saturated.
- Product Hunt: search the category — see launch dates, upvote counts, early adopter
  reactions in comments

*For each competitor found, run:*
- Their website — read positioning copy, pricing page, customer logos, case studies
- Wayback Machine (web.archive.org) — their pricing page 2-3 years ago. Many companies
  had public pricing before moving to "contact sales." Shows how pricing evolved.
- Wappalyzer free Chrome extension — reveals their tech stack instantly (cloud provider,
  CDN, CRM, analytics, payment processor). Signals scale and sophistication.
- LinkedIn company page — headcount number and 6-month change (requires login). 40%
  headcount growth in 6 months is a stronger growth signal than any press release.
  Job posting volume and department mix reveals mode (product-building vs. GTM push).
- Job posting content — engineer JDs reveal tech stack; product JDs reveal roadmap;
  sales JDs reveal target segment (ICP is often in requirements)

*For finding weaknesses:*
- `"[competitor name]" problems site:reddit.com`
- `"switched from [competitor name]" OR "migrated from [competitor name]"`
- `"[competitor name]" alternatives` — surfaces comparison articles where weaknesses
  are described neutrally
- `"[competitor name]" vs` — comparison articles with competitor listed second
- G2/TrustRadius 1-3 star reviews (see Problem & Customer section for caveats)
- `site:news.ycombinator.com "[competitor name]"` — candid, technically sophisticated

*For pricing discovery:*
- `site:[competitor.com] pricing` — finds pricing pages not linked from nav
- `"[competitor name]" pricing site:reddit.com` — users mention actual prices in threads
- Vendr (vendr.com) buyer guides — actual contract price ranges from $15B+ in verified
  enterprise software spend. Free to browse many guides without an account.
- Job posting OTE method: standard B2B SaaS quota = OTE × 5. A $200K OTE AE has
  ~$1M quota. Divide by deals/quarter to estimate ACV. SMB AEs ($110-150K OTE) →
  ACV $5-25K. Mid-market ($140-200K OTE) → $25-100K. Enterprise ($250K+) → $100K+.

*For tech stack:*
- Wappalyzer (free Chrome extension, ~50 lookups/month) — real-time on any site
- BuiltWith — better for bulk analysis

*Competitor categorization:* Always map four types, not just direct competitors:
- Direct: same problem, same customer, same approach
- Indirect: same problem, different approach
- Substitutes: customer achieves same goal a different way (including spreadsheets)
- Aspirational: where the category could go; companies to watch

The substitute category is where most analysis fails. If the real competition is
"doing it manually" or "building it in-house," that matters more than any startup.

---

**For Market & Timing**

Goal: Size the market bottom-up, confirm it's growing, and find the specific inflection
point that makes now the right time.

*Bottom-up sizing — the credible approach:*

The formula: (number of potential customers) × (annual revenue per customer).
Every assumption is independently testable. Build this before touching any analyst report.

For business counts (B2B):
- Census County Business Patterns (data.census.gov) — best free source for US business
  counts. Search by 6-digit NAICS code + state/county + employee size band. Updated
  annually. Example: "HVAC contractors with 10-49 employees in Texas" is one query.
- NAICS code lookup: naics.com/search/
- BLS QCEW (bls.gov) — more current than Census, quarterly, good for fast-growing sectors

For worker/occupation counts (if buyer is a job title, not a company):
- BLS OEWS (bls.gov/oes) — counts 830 specific occupations nationwide plus by state/metro.
  Covers wage/salary workers only, not self-employed. Annual publication.

For consumer markets:
- Census American Community Survey (data.census.gov) — demographics at census tract level
- BLS Consumer Expenditure Survey (bls.gov/cex) — household spending by category

For ACV estimation:
- Competitor pricing pages (see Competitive Landscape section)
- G2/Capterra review text — users frequently mention what they pay
- SaaS Capital benchmarks: median B2B SaaS ACV ~$26K; Horizontal SaaS $8-15K,
  Vertical SaaS $25-50K, Infrastructure/DevOps $50-150K, Enterprise Security $100-300K
- SEC EDGAR full-text search (efts.sec.gov) — search for "average contract value" or
  "average revenue per customer" in 10-K filings in the industry. Free, no API key.

*LinkedIn Ads audience size tool — underused:*
Create a draft ad campaign, set targeting by industry + company size + job title, and
the estimated audience size appears in the campaign builder. Free real-time market count.

*Timing — finding the inflection point:*

Google Trends (trends.google.com):
- Shows directional trend only — normalized to 0-100 index, not absolute counts
- Use it to corroborate a timing thesis, not to size a market
- A rising trend on problem keywords corroborates "this is getting worse"
- Flat or declining = warning sign for "why now" thesis

Google Patents (patents.google.com):
- Track patent filing velocity in a technology class over time
- Rising patent filings = early-stage market formation, typically 3-7 years before
  commercial activity peaks
- Use CPC technology codes to scope the search

Federal Register (federalregister.gov):
- Subscribe to alerts by agency or keyword — regulatory changes are announced 6-18 months
  before taking effect
- Compliance requirements create predictable market windows: GDPR → data privacy tools;
  SOC 2 → GRC software; ADA → accessibility tooling

Crunchbase free tier:
- Count funded companies in the category — proxy for competitive intensity and VC conviction
- Track which investors are active (Tier 1 VC presence = smart money believes market is real)
- Note: exact funding amounts increasingly paywalled on free tier

*What NOT to use for market sizing:*
Gartner/IDC reports as your primary source. These numbers are generated by applying growth
rates to prior estimates, use broad market definitions that don't match your product,
are often 18-24 months old, and have opaque methodologies. Use them for sanity-check
magnitude only. A VC who hears "a Gartner report" as the source will immediately discount it.

The "1% of the market" framing is the worst possible approach. Never use it.

---

**For Business Model**

Goal: Understand what revenue models work in this space, what the economics look like
at comparable companies, and what this business needs to look like to be healthy.

*Benchmark reports — all free:*

High Alpha / OpenView SaaS Benchmarks (highalpha.com/saas-benchmarks):
- Annual survey of 800+ private SaaS companies. The most widely cited private benchmark.
- Contains: CAC payback (median ~10-15 months), NRR (median 106% venture-backed),
  LTV:CAC targets (3:1+), Rule of 40, growth by ARR band. Fully free.
- Companion: Kyle Poyar's Substack "Growth Unhinged" (growthunhinged.com) for
  plain-English breakdowns of what the numbers mean

SaaS Capital (saas-capital.com/research):
- 1,000+ private B2B SaaS companies, annual survey. Also publishes separate bootstrapped
  benchmarks. Fully free, no form fill.

ChartMogul Reports (chartmogul.com/reports):
- 2,500+ SaaS companies on their billing platform. Product-usage-based (not survey-based),
  which means less self-selection bias. Free. Covers NRR, SMB vs. enterprise churn,
  growth rates.

Meritech Analytics (meritechcapital.com/benchmarking):
- Every public SaaS company: valuation multiples, revenue growth, gross margins, NRR,
  magic number/payback periods, ARR per employee. Fully filterable. Free. Updated regularly.
- This is the single best free tool for public SaaS comparable analysis.

a16z Growth Metrics Guide (a16z.com/growth/guide-growth-metrics):
- Includes actual percentile benchmarks (25th/50th/75th/90th) for B2B metrics.
  One of the few sources that explicitly defines its metrics. Free.

KeyBanc + Sapphire SaaS Survey:
- 100+ private SaaS companies, deep data on ACV by sales cycle, quota attainment,
  EBITDA margins. PDF is widely shared — search "2024 KBCM Sapphire SaaS survey PDF."

*Public company filings:*
- EDGAR full-text search: efts.sec.gov/LATEST/search-index — search for "customer
  acquisition cost", "payback period", "net revenue retention" across all S-1/10-K
  filings in the industry. Free, no API key.
- What S-1s disclose: revenue by cohort (implies NRR), S&M as % of revenue (CAC proxy),
  gross margin, headcount by function (ARR per employee), sometimes explicit ACV.

*Pricing research:*
- Competitor pricing pages + Wayback Machine for historical pricing
- Vendr buyer guides (vendr.com) — actual price ranges from verified enterprise spend
- G2/Capterra reviews — users mention actual prices in reviews, especially in complaints
- Job posting OTE method (see Competitive Landscape section)

*Stage mismatch — the biggest trap in benchmarks:*
The same metric means completely different things at different stages.
- Under $1M ARR: 100-200% YoY growth is typical
- $2-10M ARR: 50-100% is doing well
- $10M+ ARR: 30-50% is above median
Benchmark reports are dominated by $5-50M ARR companies. Apply them to a $500K ARR
company and the comparison is noise.

---

**For GTM Patterns**

Goal: Understand how companies in similar spaces actually acquired their first customers,
which channels work, what the typical sales motion looks like, and what's failed.

*Primary case study sources:*

First Round Review (review.firstround.com/articles/go-to-market/):
- Best VC publication for narrative GTM case studies. Long-form (3-8k words), named
  founders, specific tactics. Skews toward 0-$1M ARR — exactly the right window.
- Search: `site:review.firstround.com "[category]" customers`

Lenny Rachitsky (lennysnewsletter.com):
- "How the biggest consumer apps got their first 1,000 users" — covers Tinder, Uber,
  Superhuman, TikTok. FREE. Structured dataset with named companies and specific tactics.
- "How the fastest-growing B2B businesses found their first 10 customers" — Figma, Slack,
  Stripe, Airtable, Gusto. FREE.
- Podcast transcripts available on GitHub: github.com/ChatPRD/lennys-podcast-transcripts
  — grep for category/channel keywords across all episodes

YC Library (ycombinator.com/library):
- ycombinator.com/library/JE-founder-faq-how-did-you-get-your-first-customer — 50+
  co-founders from a recent batch, all answering the same question. Highest-signal raw
  material for early GTM patterns: actual founders, literal first customers.
- Filter the library by "Sales" and "Growth" topics

"The First 100" podcast (by Hadi Radwan):
- Every episode is specifically about how a founder got their first 100 paying customers.
  The most directly targeted resource for this question. Search on Spotify/Apple Podcasts.

Bessemer Atlas (bvp.com/atlas):
- bvp.com/atlas/the-founders-playbook-for-scaling-to-1-million-arr
- bvp.com/atlas/the-101-guide-on-gtm-operations-for-saas-founders
- More framework-driven than story-driven. Good for GTM decision structure.

Indie Hackers (indiehackers.com):
- The most honest practitioner content for sub-$5M ARR companies. Culture rewards
  transparency. Search: `site:indiehackers.com "first customers" "[category]"`

Cross-podcast keyword search:
- listennotes.com — indexes 3.5M+ podcasts, searchable by keyword. Search
  "first customers" filtered by Business category.

*For failure post-mortems:*
- getautopsy.com — 2,000+ startup post-mortems with founder-written explanations.
  Filter by sector. Free to browse. The SaaS tag is at getautopsy.com/startup-failure-stories/tag/SaaS
- CB Insights (cbinsights.com/research/startup-failure-post-mortem/) — directory of
  483+ failure post-mortems with links to source essays. Free.
- Hacker News: hn.algolia.com → "what didn't work" or "failed" GTM → filter to
  Ask HN threads. These are among the most honest content anywhere.

*Channel detection from the competitive landscape:*
- Content-driven signal: competitors rank on high-intent SEO keywords, active blogs
  with 50+ posts. Check Ahrefs/Semrush free tier for organic traffic.
- Community-driven signal: Discord/Slack communities, active subreddits about the
  product category (r/[category] with 10k+ members)
- Paid acquisition signal: visible on Facebook Ad Library (facebook.com/ads/library) —
  search any company name to see active ads. Free.
- PLG signal: competitors have freemium/free trial tiers. If 3+ have free tiers,
  PLG is proven in the category. If zero, it may not work there.
- Founder-led/outbound signal: competitors hiring SDRs/BDRs early, or having AE roles
  within the first 18 months. Check LinkedIn job history.

*Search patterns that work:*
- `"how [company name] got their first customers"` — named companies surface well
- `"how we got our first 100 customers"` — founder-written essays
- `"0 to $1M ARR" [category]` — right stage window
- `"before we hired sales" [category]` — founder-led sales stories
- `site:indiehackers.com "first customers" "[category]"`
- `hn.algolia.com` → `"first customer" [category]` → filter type:comment

---

### Round 1 — All Parallel

**Agent: Problem & Customer**
Question: Is this problem real, who suffers most acutely, and what do they currently do about it?
Find:
- Evidence the problem is real (forums, reviews, complaints, workarounds people use)
- Who has it worst — specific roles, industries, company sizes, contexts
- Current solutions and their failure modes (what do people do today?)
- Jobs-to-be-done patterns from analogous markets
- Signals of pain intensity (how much do people complain, pay, or hack around this?)

**Agent: Competitive Landscape**
Question: Who else is trying to solve this, how are they positioned, and where is the open space?
Find:
- Direct competitors (same problem, same customer)
- Indirect competitors (different approach, same outcome)
- "Do nothing" as a competitor — what happens if the customer doesn't buy anything?
- How each competitor is positioned (who they target, how they price, what they emphasize)
- Their weaknesses (bad reviews, user complaints, what they don't do well)
- Recent moves (funding, new features, expansions)
- Where the gaps are — segments underserved, jobs unmet, price points uncovered

**Agent: Market & Timing**
Question: How big is this, is it growing, and what inflection point makes now the right time?
Find:
- Market size signals — bottom-up (how many potential customers × plausible price) preferred
  over top-down reports. Both if possible.
- Growth rate and direction
- Key trends driving the market (tech shifts, regulatory changes, behavioral changes)
- "Why now" signal — what has changed in the last 2-3 years that makes this solvable or
  urgent in a way it wasn't before? This is mandatory, not optional.
- Any timing risks (is the window closing? is someone moving fast?)

**Agent: Business Model**
Question: What are the credible ways to make money here, and what do the economics look like?
Find:
- Revenue model patterns from comparable companies (subscription, usage, transaction,
  marketplace, etc.) — what's standard in this space and why
- Pricing benchmarks — what do comparable products charge?
- Unit economics ranges from comparable companies: CAC, LTV, payback period
- What business model has worked vs. failed in this space (and why)
- At what scale does the model get healthy? What are the economics at 100 customers? 1000?

**Agent: GTM Patterns**
Question: How have companies in similar spaces actually acquired their first customers?
Find:
- Go-to-market playbooks from analogous companies — how did they find their first 100?
- Which channels have worked: sales-led, product-led, content, community, partnerships,
  paid, viral, founder network
- Typical sales motion (self-serve, inside sales, enterprise deals, PLG with expansion?)
- Time-to-close benchmarks
- What the first GTM bets usually look like for this type of business
- Common GTM mistakes in this space

---

### Saving Research (Between Round 1 and Round 2)

After each Round 1 agent completes, save its full output as a bit before passing to
synthesis. Use `write_bit()` from `scripts/lib/create_bit.py`:

- **TYPE:** `insight`
- **ORIGIN:** `ai-extracted`
- **SOURCE TYPE:** `synthetic`
- **SOURCE GROUP:** `ai`
- **CLUSTER:** The project being researched (e.g., "Songbird")
- **TAGS:** `source-research, business-strategy, [project-name]`
- **Content header:** Start each bit with `## [Agent Name] — [Project] Research` so
  the agent is identifiable in search results

Record the bit IDs. Pass both the content and bit IDs to the Round 2 synthesis agent.

---

### Round 2 — After Round 1 Complete

**Agent: Opportunity Assessment (Synthesis)**
This agent does NOT do additional external research. It reads all five Round 1 outputs
and forms a strategic opinion.

Question: Given everything we found, where is the real opening, what's the strongest
version of this business, and what does it take to win?

Produce:
- A point of view on whether the opportunity is real and compelling (honest, not cheerful)
- The strongest version of the business — what positioning, customer, and model makes
  this most defensible
- The 2-3 things that have to be true for this to work (load-bearing assumptions)
- The 2-3 biggest risks — specifically what could kill this
- Initial view on competitive moat: what type of moat is plausible, at what stage
- The open questions that only the founder can answer

This is the agent that produces the strategic opinion. Everything else is inputs.

---

### Research Standards

- Label all market size numbers as estimates. Never present them as facts.
- Cite sources or at minimum note the basis for claims ("based on 3 competitor pricing pages")
- If a dimension has thin data, say so explicitly. Don't fill gaps with confident guesses.
- If something contradicts founder assumptions, flag it directly — don't soften it.


---

## Phase 2.5: Strategic Personas (Optional)

**Goal:** Sharpen the ICP before writing the memo. Run this when the customer definition
is still vague after Round 2, or when research surfaced 2+ distinct customer types worth
distinguishing.

**When to run:** If Round 2 synthesis reveals multiple distinct customer segments, or if
the ICP still feels demographic rather than behavioral. If the customer is clearly defined
and singular, skip to Phase 3.

**How:** Invoke the `/persona` skill at Sketch tier. Pass as context:
- Round 1 Problem & Customer agent findings
- Round 2 Opportunity Assessment synthesis
- Founder's customer description from Phase 1 intake

Sketch tier: hypothesis-only, no community research, 2 personas maximum.

**Check in after:** Surface the lead persona recommendation before writing the memo.
"Research surfaced [N] distinct customer types. My read is [Persona A] is the strongest
beachhead because [reason]. Does this match what you're seeing?"

**Output feeds:**
- Customer section of the memo (lead persona replaces generic ICP description)
- Strategic Bets ("We're targeting [lead persona], not [adjacent type], because...")
- The Onliness Statement ("for [specific customer] who [specific emotional context]")
- GTM Handoff block (beachhead persona reference + file path)

---

## Phase 3: First Draft — The Strategic Memo

**Goal:** Produce a structured strategic memo that synthesizes research into an opinionated
document with a point of view, explicit bets, and clear direction.

The memo is NOT a business plan. It does not describe the business — it analyzes it and
recommends. It weights sections by what's most important for THIS specific business.
Short on description, long on implication and decision.

---

### Memo Structure

```
[Business Name] — Strategic Memo
Version: 0.1 (Draft)
Date: [date]
Stage: [idea / prototype / early revenue / scaling]
Strategic Question: [the question framed in Phase 1]
```

---

**THE CORE BET**

One paragraph. The fundamental hypothesis in plain language:

"We're betting that [specific customer] has [specific problem] that [existing solutions]
can't solve well because [structural reason]. [Our approach] wins because [key insight].
If this is true, the business looks like [business model sketch] and the path to win
is [strategic direction in one sentence]."

This paragraph is the document. Everything else supports or challenges it.

---

**WHY WE BELIEVE THIS**

Short section. Evidence for each claim in the Core Bet.

- The problem is real: [specific evidence, not assertion]
- The timing is right: [the inflection point — what changed]
- The customer will pay: [evidence of willingness to pay, even proxy signals]
- We can win: [the moat hypothesis — honest about what we have now vs. what we build toward]

If any of these is weak, say so. "We don't have strong evidence on WTP yet — this is
an assumption we need to validate" is the right answer. Don't paper over it.

---

**WHAT THE RESEARCH FOUND**

Four subsections. Findings only — no filler, no boilerplate.

*Market*
Key facts about size, growth, and dynamics. Bottom-up estimate + confidence level.
The one trend that matters most for this business.

*Competition*
Who's in the space. The positioning map in plain language. Where the open space is.
One or two competitors that are actually dangerous and why.

*Customer*
If Phase 2.5 was run: name the lead persona and archetype, their JTBD statement,
and cite the persona file (docs/personas/[project]/[slug].txt).
If not: specific ICP, the job they're hiring this for, how acute the pain is,
what they currently do and why that fails them.

*Business Model*
What the economics look like in comparable companies.
What revenue model is standard and why (or why we'd deviate from it).
Rough unit economics range: what CAC/LTV needs to look like to be healthy.

---

**THE OPEN QUESTIONS**

Explicitly named uncertainties. Format for each:

> **[Assumption]** — [Why this is uncertain] → [How we'd validate or resolve it]

Aim for 3-5. These are the things we don't know yet that could change the strategy.
Be honest. This section is more valuable when it's uncomfortable.

---

**THE STRATEGIC BETS**

Where we're playing and explicitly where we're NOT. Each bet has a reason.

Format:
> We're [doing X], not [alternative Y], because [specific reasoning].

Examples:
- We're targeting [specific ICP], not [adjacent segment], because [reason]
- We're entering via [channel], not [alternative], because [reason]
- We're building [this moat] before [that one] because [reason]
- We're [pricing model], not [alternative], because [reason]

These are decisions. They should feel like choices with tradeoffs, not default assumptions.

---

**DIRECTION**

Three things:

*Validate first:* The single riskiest load-bearing assumption. The one that, if wrong,
changes the strategy significantly. This is what to test before building more.

*Build toward:* The long-term defensible position. What does winning look like in 3-5
years? The near-term decisions need to be consistent with this.

*Don't do:* The explicit tradeoffs. Things that seem related or adjacent but are out of
scope — and why. A good strategy says no to things.

---

**THE ONLINESS STATEMENT**

The synthesis output. You can only write this after the competitive landscape, JTBD,
and Strategic Bets are resolved — it's what the research earns.

Format:
> "[Brand] is the only [category] that [differentiated benefit] for
> [specific customer] who [specific context / emotional state]."

Quality test — the swap test:
Replace the brand name with a competitor's. If the statement still works for them,
the differentiation isn't real yet. Keep refining until it fails the swap.

This is the handoff to the brand-brief skill. If `/brand-brief` is invoked after this
strategy, it receives the Onliness Statement as its starting point and builds the
expression layer (voice, visual, naming) on top. The brand brief derives its positioning
from this document — it does not re-derive it independently.

---

**BRAND BRIEF HANDOFF** *(optional — include if brand work is next)*

A structured block that gives `/brand-brief` everything it needs without repeating
the strategy intake:

- Onliness Statement: [from above]
- Category: [what would someone type to find this?]
- JTBD: functional job / emotional job / social job
- Founding insight: [what the founder saw that others didn't]
- Why now: [the inflection point]
- The enemy: [the worldview or approach this product pushes back against — not a
  competitor list, but the mentality being rejected]

If brand work isn't next, omit this section. It's a handoff artifact, not strategy.

---

**GTM HANDOFF** *(optional — include if GTM strategy work is next)*

A structured block that gives `/gtm-strategy` everything it needs without re-deriving
the strategy:

- Lead Persona: [name + archetype label] (file: docs/personas/[project]/[slug].txt, or "not yet built")
- Beachhead hypothesis: [which segment to pursue first and why — 1-2 sentences]
- Sales motion hypothesis: [self-serve / founder-led / inside sales / PLG — with brief reasoning]
- Primary channel bet: [the one channel with strongest signal from GTM Patterns research]
- Why now: [the inflection point — what changed that opens this window]
- Relevant Strategic Bets: [2-3 bets most relevant to GTM from the Strategic Bets section]

If GTM work isn't next, omit this section.

---

### Memo Tone Standards

- Answer first, support second. The conclusion comes before the evidence.
- Opinionated, not neutral. "The market is competitive which presents both challenges
  and opportunities" is not analysis. Take a position.
- Honest about uncertainty. Confidence levels on claims where data is thin.
- No filler. Every sentence should either be a finding, an implication, or a decision.
- Short. The memo should be readable in 10-15 minutes. Depth lives in the Open Questions
  and supporting detail, not in paragraph length.


---

## Phase 4: Iteration

**Goal:** Refine the memo from a first draft into a document the team can act on.
The AI drives this — not passive "do you have changes?" but active resolution of
the highest-uncertainty areas.

**After presenting the draft:**

1. **Name the weak spots explicitly.** Don't wait for the founder to find them.
   "There are two sections I'm uncertain about — [X] and [Y]. Let me flag those and
   we can work through them."

2. **Ask targeted questions.** Based on the Open Questions section — one at a time.
   These are things only the founder can answer.
   - Their proprietary insight: "What's the non-obvious thing you believe about this
     market that most people don't? The edge you have that research can't find?"
   - Their unfair advantage: "Why is this team specifically suited to win here?"
   - Their GTM hypothesis: "Who specifically are you calling first? What does that
     first conversation look like?"

3. **Push back when warranted.** If founder input contradicts research, name the tension.
   Don't just incorporate it.
   "You said partnerships are the GTM path, but in comparable spaces partners consistently
   deprioritize new vendors until there's pull from end users. What makes you think this
   will be different here?"

4. **Update and version the memo.** Each substantive revision bumps the version (0.1 → 0.2).
   This preserves the thinking trail.

5. **Run the swap test on the Onliness Statement.** Replace the brand name with a
   competitor's. If it still works for them, the differentiation isn't real — push
   further on what makes this specifically different.

6. **End the iteration when:** The Open Questions list is resolved (answered or explicitly
   accepted as known risk), the Onliness Statement fails the swap test (meaning it's
   genuinely differentiated), and the founder confirms the Core Bet paragraph reflects
   their actual thesis.

**What good iteration looks like:**
- Founder challenges a competitive assessment → AI revises with founder's input + flags
  if it changes the Core Bet
- Research turned up a dangerous competitor → discussion about whether the moat is real
- Founder has proprietary insight → Core Bet gets sharper and more specific
- Something in the research was wrong → AI revises and notes what changed and why

**What bad iteration looks like:**
- AI just accepts everything the founder says without checking against research
- Iteration becomes "make it sound better" not "make it more true"
- Memo grows longer with each revision instead of sharper


---

## Output Standards

The final memo should:

- Be readable in 10-15 minutes
- Pass the "Core Bet test": can a new team member read the first paragraph and know
  what the company is betting on and why?
- Have every Open Question either resolved or explicitly marked as known risk
- Have Strategic Bets that feel like real choices, not default assumptions
- Have Direction that's specific enough to act on — "validate WTP with 5 customer
  interviews in the next 2 weeks" not "continue to gather market feedback"

**File location:** Save as a bit using `write_bit()` with TYPE: `note` and
TAGS: `strategic-memo, [product-name]`. The memo is a living document — version it as
the strategy evolves. Include a SOURCE RESEARCH section listing the bit IDs of all
Round 1 research bits:

```
SOURCE RESEARCH
  Problem & Customer: bit [ID]
  Competitive Landscape: bit [ID]
  Market & Timing: bit [ID]
  Business Model: bit [ID]
  GTM Patterns: bit [ID]
```

**Format for saving:** Plain text or markdown. Include the version number and date in
the header so it's easy to track evolution.


---

## Key Behaviors Summary

**Frame before researching.** Confirm the strategic question before any agent runs.
Wrong question = wasted research.

**Research is autonomous.** The founder doesn't participate in Phase 2. Come back
with findings, not requests for more input.

**Form an opinion.** The Opportunity Assessment agent must have a point of view.
"This space has characteristics X and Y, which suggests..." not "the market shows
various indicators that could be interpreted..."

**The memo is a decision document.** If you read it and don't know what the company
is betting on, what it's not doing, and what to do first — it's not done.

**Iteration is AI-driven.** Name the weak spots. Ask the hard questions. Push back.
Don't wait to be corrected.

**Honest about limitations.** Thin data is thin data. Market size estimates are estimates.
Unknown is unknown. Labeling uncertainty correctly makes the document more useful,
not less credible.

**The Onliness Statement is the capstone, not the opener.** It can only be written
after competitive landscape, JTBD, and positioning are resolved. If it can be written
before the research is done, the research wasn't deep enough.

**This skill feeds three downstream skills.**
- **/persona** — Phase 2.5 invokes it at Sketch tier to sharpen the ICP before writing
  the memo. Persona output lives at docs/personas/[project]/.
- **/brand-brief** — receives the Onliness Statement and Brand Brief Handoff block.
  Builds the expression layer (voice, visual, naming); does not re-derive positioning.
- **/gtm-strategy** — receives the GTM Handoff block (beachhead hypothesis, lead persona,
  channel bets, sales motion). Builds the first-customer plan; does not re-derive strategy.

Design the memo outputs with all three handoffs in mind.
