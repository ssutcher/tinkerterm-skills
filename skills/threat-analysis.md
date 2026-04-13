---
name: threat-analysis
description: >
  Structured, calibrated threat assessment for personal and family safety.
  Produces a ThreatIndex score (0-10) with 5-dimensional breakdown, calibrated
  probability language, and tiered action recommendations. Draws on professional
  intelligence methodology (JTAC, NTAS, CARVER, Meloy warning behaviors).
  Self-sufficient: extracts context from conversation, researches everything itself,
  states assumptions explicitly. Only asks the user one question if profile would
  materially change the score.
  Triggers on: "threat analysis", "how safe are we", "should I be worried about",
  "risk assessment", "is my family safe", "threat to my family", "how dangerous is",
  "terrorist risk", "attack risk".
---

# Threat Analysis Skill

## Purpose

Produce a structured, honest, calibrated threat assessment for personal or family safety.
Not alarmist. Not dismissive. Grounded in professional intelligence methodology.

**Do the work yourself. Don't interrogate the user.**
Extract context from the conversation. Research everything you can. State your assumptions.
Only ask the user something if knowing it would materially change the ThreatIndex score.

---

## When to Invoke

- User asks about threats to their personal or family safety
- User asks about risk from a specific group, actor, or geopolitical event
- User asks "should I be worried about X" in a safety context
- User asks about terrorism risk, attack risk, or regional danger

## When NOT to Invoke

- General security/InfoSec threat assessments (use standard research instead)
- Business continuity / corporate threat modeling
- Fictional scenarios or creative writing

---

## Step 1: Extract Context from Conversation

**Do not ask. Infer.** Pull from what the user has already said:

- **Location:** City, region, neighborhood
- **Threat actor:** Who or what is the concern — state, group, ideology
- **Triggering event:** What prompted this — news event, deadline, escalation
- **Timeframe:** Any specific window mentioned

**Default assumptions (state explicitly in output):** Private individual, no prior
threats received, no adversarial personal history, standard digital footprint. These
lower the Specificity score. If any are wrong, the score changes.

---

## Step 1.5: Check for Prior Assessments

Before launching research, query for any previous assessment on this subject:

`search_bits(query: "threat-assessment [location] [actor]", tags: threat-assessment, limit: 5)`

**If found:** Load full content, note previous ThreatIndex score/level/date/findings. The
prior assessment is an INPUT — all 6 research streams still run in full. Use it to ground
the DELTA section. **If not found:** proceed normally, omit DELTA section.

---

## Step 2: Run Research (All 6 Streams)

Run all streams. Do not skip. Do not score from memory.

### Stream 1: Official Threat Level
Check: UK JTAC (gov.uk), State Dept Travel Advisory (travel.state.gov), DHS NTAS (dhs.gov),
FBI threat advisories (news search). Get current level + definition for each.

### Stream 2: Threat Actor Profile
Sources: Counter Extremism Project, Soufan IntelBrief, Long War Journal, MEMRI JTTM,
UN Sanctions List. Determine: historical attacks on US soil, stated intent toward user's
geography/demographic, known sleeper networks in region, current operational status.

### Stream 3: Current Geopolitical Context
News search: "[actor] retaliation [month/year]", "[actor] US homeland threat". Determine
what triggered current threat environment, recent escalations/de-escalations, official
government statements on retaliation risk.

### Stream 4: Regional Intelligence
Search: "[city] [actor] threat", "FBI [city] [actor] warning", "[state] terrorism advisory".
Also check Long War Journal, UN News, local law enforcement advisories.

### Stream 5: Targeting Logic (most important for private individuals)
Determine: What profiles does this actor historically target? Does a private individual
in this location match? Opportunistic vs. highly targeted attack selection? Known proxy
networks or inspired individuals in region? If user does NOT match targeting logic,
Specificity drops significantly — say so clearly.

### Stream 6: Protective Environment
FBI field office coverage, current law enforcement posture, community resources or
emergency management advisories.

### Saving Research (After All Streams Complete)

After all 6 research streams complete, save a single combined research bit with all
stream outputs before scoring:

`create_bit(type: insight, project: threat-assessment, tags: source-research threat-analysis [actor-slug] [location-slug])`

Combine all 6 stream outputs under clear headers (## Stream 1: Official Threat Level, etc.).
Record the bit ID and reference it in the final assessment.

---

## Step 3: Score the 5 Dimensions

### 1. Probability (P) — weight 30%
9-10: Almost certain (>90%) | 7-8: Probable (60-90%) | 5-6: Possible (30-60%) |
3-4: Unlikely (10-30%) | 1-2: Remote (<10%)

### 2. Specificity (S) — weight 25%
9-10: Named target, known method, identified timing | 7-8: Specific target category and
location | 5-6: Regional or demographic targeting | 3-4: National/ideological (broad) |
1-2: Vague, diffuse — general tension only

**Private individual default:** Start at 3-4 unless research shows this actor targets
civilians broadly or this region specifically.

### 3. Capability (C) — weight 20%
9-10: Confirmed assets, weapons, access | 7-8: Demonstrated capability, plausible access |
5-6: Capability exists, access uncertain | 3-4: Limited capability, operational gaps |
1-2: No demonstrated capability or pathway

### 4. Imminence (I) — weight 15%
9-10: Hours | 7-8: Days | 5-6: Weeks | 3-4: Months | 1-2: No timeline

### 5. Impact (M) — weight 10%
9-10: Mass casualties, catastrophic disruption | 7-8: Significant casualties, major
disruption | 5-6: Moderate harm, localized | 3-4: Minor harm, limited | 1-2: Negligible

Score impact for the MOST LIKELY attack vector, not worst-case. If both cyber and
physical vectors are relevant, score them separately.

### Composite Formula

```
ThreatIndex = (P x 0.30) + (S x 0.25) + (C x 0.20) + (I x 0.15) + (M x 0.10)
```

Round to one decimal. Cap at 10.

### The ThreatIndex Scale

| Score | Level | Posture |
|-------|-------|---------|
| 9-10 | CRITICAL | Immediate protective action. Contact law enforcement. Consider evacuation. |
| 7-8 | HIGH | Significant precautions. Alert family. Vary routines. Emergency plan ready. |
| 5-6 | MODERATE | Reasonable precautions. Emergency supplies. Stay informed. |
| 3-4 | ELEVATED | Standard awareness. Know your exits. |
| 1-2 | LOW | Normal conditions. |

---

## Anti-Bias Checks (Run Before Finalizing Score)

- **Availability bias:** Overweighting the most recent/dramatic event? Compare against base rates.
- **Confirmation bias:** Searched for evidence AGAINST your initial read? (Mandatory disconfirmation pass)
- **Specificity inflation:** Treating a broad threat as more targeted than it is?
- **Single-source flag:** Any key finding from one uncorroborated source? Flag it.
- **Threat vs. posing threat:** Making threats does not equal posing a threat. Pathway behaviors matter more.

---

## Step 4: Output the Assessment

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
THREAT ASSESSMENT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Location:      [City, region]
Threat Actor:  [Name/group/state]
Context:       [One-sentence triggering situation]
Date:          [Today's date]
Assumptions:   Private individual, no prior threats, no public profile,
               standard digital footprint. [Other assumptions.]
               → Flag me if any are wrong — it would change the score.
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

ThreatIndex: X.X / 10 — [LEVEL NAME]

DIMENSIONAL SCORES
  Probability   X/10  [████████░░]  [one-line reasoning]
  Specificity   X/10  [█████░░░░░]  [one-line reasoning]
  Capability    X/10  [███████░░░]  [one-line reasoning]
  Imminence     X/10  [████░░░░░░]  [one-line reasoning]
  Impact        X/10  [█████████░]  [one-line reasoning]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
DELTA FROM PRIOR ASSESSMENT  (omit if no prior bit found)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Prior: X.X / LEVEL (date) | Current: X.X / LEVEL | Change: +/- X.X
What's new: [key developments]
What's unchanged: [stable factors]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
KEY FINDINGS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[3-6 bulleted findings, each with source and date]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
KEY UNCERTAINTIES
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[Name what is unknown and why it matters. "If X were true, score moves from Y to Z."]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
CALIBRATED ASSESSMENT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
"We assess [X] is [almost certainly / probably / possibly / unlikely / remote]
with [high / moderate / low] confidence because [reasoning]."
What would move this score up: [...]
What would move this score down: [...]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
THREAT TRAJECTORY
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[ESCALATING / STABLE / DE-ESCALATING]
[What's driving the direction]
[Key trigger events to watch]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
MOST LIKELY THREAT VECTORS (ranked)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
1. [Vector] — Broadly: ~X% / You: ~Y% — [why]
2. [Vector] — Broadly: ~X% / You: ~Y% — [why]
3. [Low prob / high impact] — Broadly: ~X% / You: ~Y% — [why worth naming]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
RECOMMENDED ACTIONS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
TIER 1 — DO NOW: [specific actions matched to threat level]
TIER 2 — PREPAREDNESS: [reasonable precautions]
TIER 3 — MONITOR: [things to watch; reassess if: triggers]
EMERGENCY: FBI tip line 1-800-CALL-FBI, [regional contact]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SOURCES CONSULTED
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[All sources with date. Mark unverified/single-source explicitly.]
```

---

### Saving the Assessment

After outputting the text assessment, save it as a bit:

`create_bit(type: insight, project: threat-assessment, tags: threat-assessment [actor-slug] [location-slug])`

Include a SOURCE RESEARCH line referencing the combined research bit ID.
This is what future assessments query for delta comparison.

---

## Calibrated Probability Language (Sherman Kent Standard)

Always pair a probability estimate with a confidence level.

| Term | Probability |
|------|-------------|
| Almost certainly | ~93% |
| Probably / Likely | ~75% |
| Possibly | ~50% |
| Unlikely | ~30% |
| Remote | <10% |

| Confidence | Meaning |
|-----------|---------|
| HIGH | Multiple independent corroborating sources |
| MODERATE | Limited sources but consistent signal, or one strong source |
| LOW | Fragmentary, single source, or contradictory |

---

## Reference Sources

### Tier 1 — Always Check
Counter Extremism Project (counterextremism.com), Soufan IntelBrief (thesoufancenter.org),
Long War Journal (longwarjournal.org), UK JTAC (gov.uk), State Dept Travel Advisories
(travel.state.gov), UN News (news.un.org), UN Sanctions List (scsanctions.un.org)

### Tier 2 — When Relevant
MEMRI JTTM (memri.org/jttm), CSIS (csis.org), Global Terrorism Index
(visionofhumanity.org), OSAC (osac.gov), ACLED (acleddata.com)

### Tier 3 — News Search Templates
"[actor] retaliation [month year]", "[actor] US homeland attack",
"FBI [city] [actor] warning", "[state] terrorism advisory [year]",
"DHS bulletin [actor]"

---

## Key Behaviors

**Extract, don't interrogate.** Start researching immediately from conversation context.
The user came worried — don't make them fill out a form.

**State assumptions, then offer to adjust.** One line at the bottom, not upfront.

**Targeting logic is the key question.** Does this actor target random civilians in this
geography, or specific profiles? If targeted and user doesn't match, say so clearly.

**Rank vectors with TWO probabilities.** Broadly (does this attack type happen in the US?)
vs. You (does it affect this specific person/location?). These often differ by an order
of magnitude. Collapsing them is the most common source of inflated personal risk estimates.

**Trajectory matters as much as score.** A 5/10 escalating fast is more urgent than a
stable 7/10.

**Don't catastrophize, don't minimize.** Be accurate. Let the score speak.

**Note what would change the assessment.** "If X happened, this moves from MODERATE to
HIGH." Gives the user a monitoring framework.

---

## Common Failure Modes

- Asking for inputs before researching — do the research first
- Treating broad national threats as personally specific — score Specificity honestly
- Scoring from conversation only — run the searches, situation changes fast
- Omitting disconfirmation pass — actively search for contradicting evidence
- Conflating cyber and physical risk — name them separately, different precautions
- "No imminent threat" without time horizon — always specify the window
