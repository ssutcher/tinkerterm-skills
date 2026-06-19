---
name: brand-naming
description: >
  Research-backed brand naming co-pilot for companies, products, and features. Generates
  candidates through five creative lenses (archetype, phonetic, competitive gap, metaphor,
  wild card), evaluates against trademark distinctiveness and domain strategy, and produces
  a shortlist with rationale and tagline drafts. Use when naming a product, company,
  feature, or project — or when the user asks "what should we call this."
---

# Brand Naming Skill

## What This Is

A structured naming co-pilot that generates and evaluates brand names grounded in
linguistics, trademark strategy, and competitive positioning — not pattern-matched
"startup name" outputs.

The core problem with AI-assisted naming: models generate whatever "sounds like a name
in this category." That produces the same crowded territory everyone else already
occupies. This skill forces category contrast first, phonetic intentionality second,
and strategic fit third — in that order.

**Distinct from /brand-brief:** That skill takes moodboard data and produces visual brand
directions. This skill produces the *name itself*, which feeds into brand brief work.
Run this first.

**Inputs from upstream:**
- `/business-strategy` — Strategic Memo with Onliness Statement, competitive landscape
- `/persona` — Target segment's JTBD, vocabulary, reference points

**Outputs to downstream:**
- Name shortlist (5-8 finalists) with rationale, name stories, tagline drafts
- Domain/trademark path for each finalist
- Handoff block for `/brand-brief` if visual identity work follows


## When to Invoke

**Auto-trigger on:**
- "name this", "what should we call it", "let's name X"
- "brand name", "product name", "company name"
- "come up with names", "naming session", "help me name"
- "what's a good name for", "name for our X"
- After /business-strategy when a name hasn't been established
- /brand-naming

**Also useful for:** Rebranding, naming features/sub-brands, evaluating a name
the team already has (skip to Phase 3).

**When NOT to invoke:** Name already locked (just answer questions), tagline/copy
only (just do it), quick reaction to a name (just give the reaction).


## Auto-Trigger Behavior

When this skill auto-triggers, confirm scope before proceeding:

> "Want me to run a full naming session? I'll map the competitive name landscape,
> generate candidates across multiple lenses, score them against the key criteria,
> and produce a shortlist with name stories and tagline drafts."

Wait for confirmation. If yes, proceed to Phase 1.


---

## The Phases

```
INTAKE -> GENERATE -> EVALUATE -> SHORTLIST
```

---

## Phase 1: Intake

**Goal:** Build the naming brief before any generation begins. Wrong brief = wrong
names. This phase is where the strategic clarity that makes naming obvious comes from.

**Step 1 — Load from upstream skills (preferred path):**

Check if a Strategic Memo and persona bits exist:
- `search_bits(query: "strategic-memo [product]")`
- `search_bits(query: "persona [product]")`

If found: load the Onliness Statement, competitive landscape, GTM Handoff, and
target persona description. Confirm: "I found the Strategic Memo. The Onliness
Statement is [X] and the category landscape is [Y]. Does this still hold?"

**Step 2 — Gather naming-specific inputs:**

Ask as a conversation, one or two questions at a time:

1. **What's being named?** Company / product / feature / sub-brand / product line?
   (Stakes and naming rules differ significantly by type.)

2. **The Onliness Statement (if not in memo):** "We are the ONLY [category] that
   [differentiator] for [audience]." Push until this is one sentence.
   If they can't state it yet, do this before naming — names without a trueline
   are just words.

3. **Names they admire and WHY.** 3-5 examples from any category.
   This is the single most diagnostic input — it reveals decision-maker taste faster
   than any other question. Don't skip it.

4. **The competitive name landscape.** List the 5-8 names they'll sit next to in
   search results, pitch decks, and conversations. What patterns dominate the category?
   This is where the zig is — we'll zag from here in Phase 2.

5. **Tone adjectives.** 3 the name should feel like; 3 it should NEVER feel like.
   These are guardrails for generation, not selection criteria.

6. **Hard constraints.** Anything already ruled out? Languages it must work in?
   Character or syllable limits? TLD preferences?

7. **Archetype direction.** Where on the spectrum does the team lean?
   - Fanciful / coined (Kodak, Google, Figma) — complete ownership, zero built-in meaning
   - Arbitrary (Apple, Stripe, Notion) — real word, unrelated meaning, strong protection
   - Suggestive (Slack, Netflix, Swiffer) — hints at benefit, requires imagination
   - Descriptive (Zoom, Basecamp) — clear but nearly unprotectable; boxes the brand in

   No preference is fine — that's what Phase 2 will test.

**Deliverable:** Confirm the brief aloud before moving to generation:
"Here's the naming brief: [summarize]. Does this capture what we're working with?"


---

## Phase 2: Generation

**Goal:** Get to 40-50 raw candidates before any filtering. Good names rarely appear in
the first 10. Volume is not creative laziness — it's the only way to find what's
actually available in the name space.

Run all five lenses. Each produces 8-10 candidates. No filtering yet — just generate.

### The Five Lenses

**Lens 1: Archetype Lens**
Generate 8-10 names squarely within the preferred archetype(s).
- Fanciful: invented words, constructed phonemes, non-dictionary
- Arbitrary: real English words with zero categorical relationship
- Suggestive: real words that metaphorize one dimension of the product
- If no archetype preference stated, run at least two

**Lens 2: Phonetic Lens**
Generate for sound symbolism fit — the sounds should support the brand feeling,
not contradict it. This is science, not intuition.

Match sounds to brand feeling:
- Energy/sharpness: plosives (K, T, P, G, B, D), hard consonants
- Warmth/trust: nasals (M, N), soft consonants, rounded vowels
- Lightness: front vowels (ee, ih) | Substance: back vowels (oo, oh, aw)
- Precision: bilateral symmetry (Sonos, Kayak, Civic)

Two syllables are the sweet spot. Three is the limit. Names under eight characters
outperform in memory tests.

**Lens 3: Competitive Gap Lens**
Map the dominant naming pattern in the category, then generate *against* it.
- Tech-literal category (Linear, Notion, Craft): generate evocative/cultural names
- Nature metaphor category: generate abstract/constructed names
- Compound word category: generate single invented words
- The gap is where distinctiveness lives; the pattern is where you disappear

**Lens 4: Metaphor Lens**
Name the brand's *feeling or behavior*, not its function. Swiffer didn't describe
mopping — it reframed mopping as light and joyful. For each candidate: can you
explain the connection in one sentence without it feeling forced?

**Lens 5: Wild Card Lens**
Pick an unrelated domain (outdoor gear, cooking, sailing) and generate names for
it, then look for what transfers. This is Lexicon's "Team 3" method — the team
that doesn't know the real brief frequently produces the winning name because
they arrive without category assumptions.

**After all five lenses:**
Cull the ~50 candidates to 15-20 worth developing. Filter on: is it a plausible
name? (Not "is it the right name" — that's Phase 3.)

---

## Phase 3: Evaluate

**Goal:** Score each of the 15-20 candidates against consistent criteria.
Produce 5-8 finalists for the shortlist.

**Important warning:** If the team unanimously loves a name immediately, that's
a signal, not a win. Comfort often means safety. Azure was initially called "dumb."
Sonos was rejected for lacking entertainment appeal. Name this dynamic when scoring.

### Evaluation Criteria

**1. Neumeier's 7 Criteria** (score 1-5 each)
- Distinctive — stands out from competitors named in the brief
- Brief — short enough to use naturally in conversation
- Appropriate — fits the emotional territory of the product
- Easy to spell and pronounce — no friction, no embarrassment on the phone
- Likable — people enjoy saying it and hearing it
- Extensible — works as the company grows beyond current scope
- Protectable — can be trademarked; defensible

**2. Trademark Distinctiveness**
Each name falls somewhere on this spectrum. The position is both a legal and
strategic variable:
- **Fanciful:** Invented words (Kodak, Xerox, Google) — maximum legal protection,
  zero built-in meaning. Requires marketing investment to attach meaning.
- **Arbitrary:** Real word, unrelated to product (Apple, Stripe, Dove) — very
  strong protection, can register immediately.
- **Suggestive:** Hints at benefit, requires imagination (Netflix, Slack, Swiffer)
  — strong protection, some semantic signal. The practical sweet spot.
- **Descriptive:** Directly describes the product — weak protection, cannot register
  without proof of years of exclusive use. Boxes the brand in as it grows.
- **Generic:** The common name for the product class — never protectable.

Name the position for each finalist. Don't present a descriptive name without
flagging the trademark weakness explicitly.

**3. Processing Fluency Check**
- Say it out loud at normal conversational speed. Does it flow in a sentence?
  ("Check out [name]." "Have you tried [name]?" "We use [name] for this.")
- Can it be heard clearly in a noisy environment?
- Does it abbreviate naturally or awkwardly?
- Princeton research: easy-to-pronounce company names outperformed disfluent names
  by ~7 percentage points on IPO day. Fluency is a measurable advantage.

**4. The Bar Test** (Van Lancker)
Score 1-5 on: first impression (curiosity), clarity, memorability, "say it without
cringing" factor. Aggregate below 3.0 = discard.

**5. Name Story**
Does the name have one? "Names with a story travel."
The story doesn't have to have been true at inception — but it must be statable in
one sentence and feel earned, not manufactured. If you can't construct a plausible
name story, the name is harder to sell and harder to explain.

**6. Persona Filter**

Load persona bits if they exist: `search_bits(query: "persona [product]")`

If no persona bits exist, use the audience description from the naming brief. Run
each surviving candidate through the 1-2 personas who matter most for this brand.

For each persona x candidate, answer four questions:

- **First read:** Before any context — what does this word alone signal to this
  person? What category do they put it in?
- **Identity check:** Does it trigger a category the brand is trying to avoid?
  The silent killers vary by brand, but common ones: *prepper/tactical, tech
  startup, subscription/membership, medical, children's product.* A name that
  trips one of these for the primary buyer doesn't survive regardless of its
  Neumeier score.
- **Prior collision:** Does a dominant existing brand come to mind immediately?
  Google Keep killed "Keep" before any other evaluation could land.
- **Word-of-mouth test:** Would this persona say this name naturally in their own
  social context — to a friend, a partner, a colleague — without needing to
  explain or defend it? If they'd hesitate, they won't say it. If they won't
  say it, the referral loop the GTM depends on doesn't work.

**The primary persona is the decisive filter.** Weight the persona with the highest
purchase anxiety most heavily. Any candidate that triggers a wrong first read for
the primary persona does not make the shortlist, regardless of other scores.

---

## Phase 4: Shortlist

**Goal:** Present 5-8 finalists with full rationale. User selects 2-3 for
deeper development (domain acquisition, linguistic screening, attorney clearance).

**For each finalist, provide:**

**Name:** [Name]
**Archetype:** [Fanciful / Arbitrary / Suggestive]
**Trademark position:** [Position + one-sentence implication]
**Phonetic notes:** [What the sounds communicate, intentionally]
**Neumeier score:** [N/7 with brief rationale]
**Name story:** [One sentence. If this name spread, what's the story?]
**Domain path:** [Availability status, acquisition path if taken]
**Tagline draft:** [1-2 tagline options for this name]
**Cultural flags:** [Languages where native-speaker screening is needed;
  AI cannot substitute for this — flag specific languages and what to check]

**At the end of the shortlist:**
Recommend your top 2 with brief reasoning. Be direct. "Direction 1 is the strongest
because [X]. Direction 2 is the fallback because [Y]."

Then stop and listen. Ask: "Which of these feels like it has legs? What's your gut
reaction to the top two?"


### Domain Strategy

For each finalist, check availability across the priority stack:
1. **.ai** — strong signal for AI-native products; high value
2. **.com** — default consumer trust; worth owning even if not primary
3. **.io** — accepted in developer/startup culture
4. **.dev** — developer tools specifically
5. **.app** — software products
6. **.co** — acceptable .com substitute

If .com is taken:
- Check if the owner has an active website (harder) or a parked page (likely for sale)
- `get[name].com` and `use[name].com` are well-understood patterns
- Strong name + alternative TLD > mediocre name with .com

**Never:** let domain availability corrupt the ideation phase. Run names first,
solve domains second. Choosing names because their domains are available produces
whatever's left after everyone else took the good ones.

**When multiple URL patterns are available:**

Run them through the primary persona before registering. The URL is the first
brand touchpoint — it signals before a single word of copy loads.

- **Prefix signal:** `get` (neutral, widely understood) > `use` (functional) >
  `join` (triggers subscription anxiety) > `try` (implies freemium).
  No prefix + expressive TLD (`.family`, `.community`, `.care`) is often strongest.
- **"Say it to a friend" test:** "Just go to [domain]." If a follow-up question
  is required, the domain is doing negative work.
- **Expressive TLD check:** Before defaulting to prefix hacks, check whether
  expressive TLDs carry the brand's positioning better than a prefix that fights
  against its own implications.


### Trademark Clearance Path

The shortlist is not cleared. Before committing publicly:

1. **Knockout search** (before presenting finalists): Search USPTO TESS and basic
   web search for obvious identical conflicts on any name you're presenting.

2. **Comprehensive clearance** (after shortlist selected): Attorney-commissioned
   search covering USPTO, state databases, common law sources, domains, and social
   handles. Takes 3-5 days. In crowded categories, up to 90% of names may be
   legally unavailable — this is why volume in Phase 2 is necessary.

Flag any name that's clearly descriptive as requiring secondary meaning evidence
before registration is possible — that's a multi-year timeline, not a quick filing.


---

## Connection to the Stack

**After naming, the natural next steps:**

- **Visual identity:** `/brand-brief` — moodboard analysis and brand direction.
  Hand off: the chosen name + its tone adjectives + name story.

- **Pricing:** `/pricing-strategy` — fanciful/arbitrary names support premium
  pricing more easily than descriptive names (which anchor to category norms).

- **GTM:** `/gtm-strategy` — a name with a story travels through word-of-mouth.
  A technical name travels through search.

If handing off to `/brand-brief`, provide the naming handoff block:
```
NAME: [chosen name]
ARCHETYPE: [position]
TONE_DO: [the 3 adjectives it should feel like]
TONE_DONT: [the 3 it should never feel like]
NAME_STORY: [one sentence]
EMOTIONAL_TERRITORY: [what the metaphor/name conveys]
```

**Saving the shortlist:**
`create_bit(type: note, project: [product-name], tags: brand-naming name-shortlist [product-name])`


---

## Anti-Patterns to Watch For

**The thesaurus trap:** Opening a thesaurus and browsing synonyms produces
"Nimble," "Agile," "Swift," "Flow," "Apex" — words that feel like names but
occupy the most crowded name territory in every category.

**"Available" as the primary filter:** Finding names whose .com domains are available
gives you whatever's left after everyone else already took the good ones.

**AI generator outputs as final answers:** AI generators are trained on what "sounds
like a startup name" and produce pattern-matched plausibles. Use them for seed volume
only. They are Lens 1 inputs, not shortlist outputs.

**Comfort as a quality signal:** Internal team consensus = safety = invisibility.
The right name often feels slightly uncomfortable at first. Name this dynamic when
it appears.

**Descriptive names as the "safe" choice:** Nearly impossible to trademark in
crowded categories and permanently box the brand in.

**Skipping the name story:** Names without a one-sentence origin story are harder
to sell internally and harder to explain externally. Names with stories travel.
