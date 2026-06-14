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
  Also generates a self-contained interactive HTML dashboard with gauge, dimension bars,
  threat vectors, and tiered action cards. Saved to scrap/reports/threat-assessment.html and opened.
  Triggers on: "threat analysis", "how safe are we", "should I be worried about",
  "risk assessment", "is my family safe", "threat to my family", "how dangerous is",
  "terrorist risk", "attack risk", "/threat-analysis".
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
- User explicitly invokes `/threat-analysis`
- User asks about terrorism risk, attack risk, or regional danger

## When NOT to Invoke

- General security/InfoSec threat assessments (use standard research instead)
- Business continuity / corporate threat modeling
- Fictional scenarios or creative writing

---

## Step 1: Extract Context from Conversation

**Do not ask. Infer.**

Pull from what the user has already said:

- **Location:** City, region, neighborhood — use what they've mentioned
- **Threat actor:** Who or what is the concern — state, group, ideology
- **Triggering event:** What prompted this — news event, deadline, escalation
- **Timeframe:** Any specific window mentioned (deadline, event, etc.)

**Default assumptions (state these explicitly in the output):**
- User is a private individual (not a public figure, government official, or known activist)
- No prior threats received directly
- No specific adversarial personal history
- Standard digital footprint for someone in their location

These assumptions lower the Specificity score. If any are wrong, the score changes.

---

## Step 1.5: Check for Prior Assessments

Before launching research, query bits for any previous assessment on this subject:

```bash
python3 scripts/query-bits.py --search "threat-assessment [location] [actor]" --tags threat-assessment --limit 5
```

**If a prior bit is found:**
- Load its full content
- Note the previous ThreatIndex score, level, date, and key findings
- Pass this as context when synthesizing research and writing the output
- The prior assessment is an INPUT — all 6 research streams still run in full
- Use it to ground the DELTA section in the output (what changed, what didn't)

**If no prior bit found:** proceed normally, omit DELTA section from output.

---

## Step 2: Run Research (All Streams in Parallel)

Run all streams. Do not skip. Do not score from memory.

### Stream 1: Official Threat Level
Check in this order — use what's accessible:

| Source | URL | What to get |
|--------|-----|-------------|
| UK JTAC | `https://www.gov.uk/terrorism-national-emergency/terrorism-threat-levels` | Current level + definition |
| State Dept Travel Advisory | `https://travel.state.gov/content/travel/en/traveladvisories/traveladvisories/[country].html` | Advisory level + threat types |
| DHS NTAS | `https://www.dhs.gov/national-terrorism-advisory-system` | Current bulletin if any (may block automated fetch) |
| FBI Threats | Search current news for "FBI threat advisory [actor] [month/year]" | Any recent public advisories |

### Stream 2: Threat Actor Profile
Use news search + these sources:

| Source | URL | What to get |
|--------|-----|-------------|
| Counter Extremism Project | `https://www.counterextremism.com` | Group profile, capabilities, recent activity |
| Soufan IntelBrief | `https://thesoufancenter.org` | Recent analysis on this actor |
| Long War Journal | `https://www.longwarjournal.org` | Recent operational activity |
| MEMRI JTTM | `https://www.memri.org/jttm` | Statements, propaganda, declared intentions |
| UN Sanctions List | `https://scsanctions.un.org/consolidated` | Designated individuals / entities |

Specifically determine:
- Historical attacks on US soil or against US civilians abroad
- Stated intent toward the user's geography or demographic
- Known sleeper networks or proxy groups in relevant region
- Current operational status (active / degraded / surging)

### Stream 3: Current Geopolitical Context
News search for: "[threat actor] retaliation [current month/year]", "[threat actor] US homeland threat"

Determine:
- What triggered the current threat environment
- Recent escalations or de-escalations
- Official government statements on retaliation risk

### Stream 4: Regional Intelligence
Search for: "[city/region] [threat actor] threat", "FBI [city] [threat actor] warning", "[state] terrorism advisory"

Also check:
- Long War Journal RSS for recent regional incidents
- UN News: `https://news.un.org/en/tags/terrorism`
- Local law enforcement advisories (search "[city PD] threat advisory")

### Stream 5: Targeting Logic
This is the most important stream for private individuals.

Determine:
- What profiles does this threat actor historically target? (government officials, military, specific ethnicities, public figures, symbolic locations, infrastructure)
- Does a private individual in this location match that targeting profile?
- What is the threat actor's attack selection logic? (opportunistic vs. highly targeted)
- Are there known proxy networks or inspired individuals active in this region?

If the user's profile does NOT match the targeting logic → Specificity score drops significantly → say so clearly.

### Stream 6: Protective Environment
- What FBI field office covers this region?
- What is current law enforcement posture in the area?
- Any community resources or emergency management advisories?

---

### Saving Research (After All Streams Complete)

After all 6 research streams complete, save a single combined research bit with all
stream outputs before scoring. Use `write_bit()` from `scripts/lib/create_bit.py`:

- **TYPE:** `insight`
- **ORIGIN:** `ai-extracted`
- **SOURCE TYPE:** `synthetic`
- **SOURCE GROUP:** `ai`
- **CLUSTER:** Use the threat actor or location as cluster (e.g., "Threat assessment")
- **TAGS:** `source-research, threat-analysis, [actor-slug], [location-slug]`
- **Content:** Combine all 6 stream outputs under clear headers
  (`## Stream 1: Official Threat Level`, etc.)

Record the bit ID. Reference it in the final assessment output.

---

## Step 3: Score the 5 Dimensions

### 1. Probability (P) — weight 30%
How likely is an attack to occur in the relevant timeframe?

| Score | Meaning |
|-------|---------|
| 9–10 | Almost certain (>90%) — corroborated intelligence, active planning indicators |
| 7–8 | Probable (60–90%) — strong indicators, historical precedent in this context |
| 5–6 | Possible (30–60%) — some indicators, mixed signals |
| 3–4 | Unlikely (10–30%) — theoretical risk, minimal supporting intelligence |
| 1–2 | Remote (<10%) — no meaningful current indicators |

### 2. Specificity (S) — weight 25%
How targeted is the threat to this person / location?

| Score | Meaning |
|-------|---------|
| 9–10 | Named target, known method, identified timing |
| 7–8 | Specific target category and location identified |
| 5–6 | Regional or demographic targeting (this group, this geography) |
| 3–4 | National/ideological targeting (broad population) |
| 1–2 | Vague, diffuse — general geopolitical tension only |

**Private individual default:** Start at 3–4 unless research shows this actor targets civilians broadly or this region specifically.

### 3. Capability (C) — weight 20%
Does the threat actor have the means to execute in this location?

| Score | Meaning |
|-------|---------|
| 9–10 | Confirmed assets, weapons, and access to target area |
| 7–8 | Demonstrated capability in similar attacks, plausible access |
| 5–6 | Capability exists but access to this target is uncertain |
| 3–4 | Limited capability, significant operational gaps |
| 1–2 | No demonstrated capability or logistical pathway |

### 4. Imminence (I) — weight 15%
How soon could an attack occur?

| Score | Meaning |
|-------|---------|
| 9–10 | Hours — specific deadline or trigger event imminent |
| 7–8 | Days — active operational window |
| 5–6 | Weeks — near-term planning window |
| 3–4 | Months — indeterminate near-term future |
| 1–2 | No timeline — theoretical future risk |

### 5. Impact (M) — weight 10%
If an attack occurs, how severe for this person/family?

| Score | Meaning |
|-------|---------|
| 9–10 | Mass casualties, catastrophic infrastructure disruption |
| 7–8 | Significant casualties or major regional disruption |
| 5–6 | Moderate harm — injuries, localized disruption |
| 3–4 | Minor harm — property damage, limited disruption |
| 1–2 | Negligible direct impact |

**Note:** Score impact for the MOST LIKELY attack vector, not the worst-case scenario.
Cyberattack on infrastructure and physical attack have very different impact profiles — score them separately if both are relevant.

### Composite Formula

```
ThreatIndex = (P × 0.30) + (S × 0.25) + (C × 0.20) + (I × 0.15) + (M × 0.10)
```

Round to one decimal. Cap at 10.

---

## The ThreatIndex Scale

| Score | Level | Posture |
|-------|-------|---------|
| 9–10 | **CRITICAL** | Immediate protective action. Contact law enforcement. Consider evacuation. |
| 7–8 | **HIGH** | Significant precautions. Alert family. Vary routines. Have emergency plan ready. |
| 5–6 | **MODERATE** | Reasonable precautions. Emergency supplies. Stay informed. Avoid high-profile targets. |
| 3–4 | **ELEVATED** | Standard awareness. Know your exits. Don't ignore the environment. |
| 1–2 | **LOW** | Normal conditions. |

---

## Anti-Bias Checks (Run Before Finalizing Score)

- **Availability bias:** Am I overweighting the most recent or dramatic event? Compare against base rates.
- **Confirmation bias:** Have I searched for evidence AGAINST my initial read? (Mandatory disconfirmation pass)
- **Specificity inflation:** Am I treating a broad threat as more targeted than it is?
- **Single-source flag:** Is any key finding from one uncorroborated source? Flag it.
- **Threat vs. posing threat:** Making explicit threats ≠ posing a threat. Pathway behaviors matter more.

---

## Step 4: Output the Assessment

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
THREAT ASSESSMENT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Location:      [City, region — from conversation]
Threat Actor:  [Name/group/state]
Context:       [One-sentence summary of triggering situation]
Date:          [Today's date]

Assumptions:   Private individual, no prior threats, no public profile,
               standard digital footprint. [Note any other assumptions.]
               → Flag me if any of these are wrong — it would change the score.
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

ThreatIndex: X.X / 10 — [LEVEL NAME]

DIMENSIONAL SCORES
  Probability   X/10  [████████░░]  [one-line reasoning]
  Specificity   X/10  [█████░░░░░]  [one-line reasoning]
  Capability    X/10  [███████░░░]  [one-line reasoning]
  Imminence     X/10  [████░░░░░░]  [one-line reasoning]
  Impact        X/10  [█████████░]  [one-line reasoning]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
DELTA FROM PRIOR ASSESSMENT  (omit this section if no prior bit was found)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Prior:   X.X / LEVEL  (date)
Current: X.X / LEVEL
Change:  +/- X.X points

What's new: [key developments since last assessment]
What's unchanged: [stable factors that didn't move the score]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
KEY FINDINGS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[3-6 bulleted findings, each with source and date]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
KEY UNCERTAINTIES
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[Explicitly name what is unknown and why it matters for the score.
Include: "If X were true, the score would move from Y to Z."]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
CALIBRATED ASSESSMENT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[Format: "We assess [X] is [almost certainly / probably / possibly / unlikely / remote]
with [high / moderate / low] confidence because [specific reasoning]."]

[What would move this score up significantly: ...]
[What would move this score down significantly: ...]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
THREAT TRAJECTORY
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[ESCALATING / STABLE / DE-ESCALATING]
[What's driving the direction]
[Key trigger events to watch — what would cause a material change]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
MOST LIKELY THREAT VECTORS (ranked)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. [Most likely vector] — Broadly: ~X% / You: ~Y% — [why, what it would look like]
2. [Second most likely] — Broadly: ~X% / You: ~Y% — [why]
3. [Low probability but high impact] — Broadly: ~X% / You: ~Y% — [why it's worth naming]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
RECOMMENDED ACTIONS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

TIER 1 — DO NOW:
  • [Specific, concrete action matched to threat level]

TIER 2 — PREPAREDNESS:
  • [Reasonable precautions]

TIER 3 — MONITOR:
  • [Specific things to watch]
  • Reassess if: [specific trigger events]

EMERGENCY CONTACTS:
  • FBI tip line: 1-800-CALL-FBI
  • [Relevant regional contact]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SOURCES CONSULTED
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[All sources with publication date. Mark unverified/single-source explicitly.]
```

---

### Saving the Assessment

After outputting the text assessment, save it as a bit using `write_bit()` from
`scripts/lib/create_bit.py`:

- **TYPE:** `insight`
- **ORIGIN:** `ai-extracted`
- **SOURCE TYPE:** `synthetic`
- **SOURCE GROUP:** `ai`
- **CLUSTER:** `Threat assessment`
- **TAGS:** `threat-assessment, [actor-slug], [location-slug]`

Include a SOURCE RESEARCH line referencing the combined research bit ID from Step 2:
```
Source research: bit [ID]
```

This is what Step 1.5 queries for in future assessments — without saving here, the
delta comparison has no prior data to work from.

---

## Reference Sources (Bookmark These)

### Tier 1 — Always Check (Free, No Auth, Reliable)
| Source | URL | Best For |
|--------|-----|----------|
| UK JTAC Threat Level | `gov.uk/terrorism-national-emergency/terrorism-threat-levels` | Current baseline threat level |
| State Dept Travel Advisories | `travel.state.gov/content/travel/en/traveladvisories` | Country-level threat by type |
| Counter Extremism Project | `counterextremism.com` | Group profiles, capabilities, ideology |
| Soufan IntelBrief | `thesoufancenter.org` | Narrative threat analysis from ex-intelligence |
| Long War Journal | `longwarjournal.org` | Near-real-time conflict events, Middle East/South Asia |
| UN News | `news.un.org/en/tags/terrorism` | Official/multilateral context |
| UN Sanctions List | `scsanctions.un.org/consolidated` | Designated terrorist individuals/entities |

### Tier 2 — Check When Relevant
| Source | URL | Best For |
|--------|-----|----------|
| MEMRI JTTM | `memri.org/jttm` | Jihadi/extremist stated intent, Arabic/Farsi sources |
| CSIS Analysis | `csis.org/programs/transnational-threats-project` | Policy-grade US national security analysis |
| Global Terrorism Index | `visionofhumanity.org/maps/global-terrorism-index` | Country baseline risk scores (annual) |
| OSAC | `osac.gov` | Country security reports (business travel focus) |
| ACLED | `acleddata.com` | Real-time armed conflict data by location (free API w/ registration) |

### Tier 3 — Supplement with News Search
When the above sources don't have current enough information, run targeted news searches:
- `"[threat actor] retaliation [current month year]"`
- `"[threat actor] US homeland attack"`
- `"FBI [city] [threat actor] warning"`
- `"[state/region] terrorism advisory [year]"`
- `"DHS bulletin [threat actor]"`

---

## Calibrated Probability Language (Sherman Kent Standard)

Always pair a probability estimate with a confidence level.

| Term | Approximate Probability |
|------|------------------------|
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

## Key Behaviors

**Extract, don't interrogate.**
Pull location, threat actor, and situation from the conversation. Start researching immediately.
The user came to you worried — don't make them fill out a form first.

**State assumptions explicitly, then offer to adjust.**
"I'm assuming you're a private individual with no specific adversarial profile — if that's wrong, the Specificity score changes significantly." One line. At the bottom. Not upfront.

**The most useful question about any private individual:**
"Does this actor's targeting logic include random civilians in this geography, or is it targeted at specific profiles?"
If the answer is "targeted," and the user doesn't match the profile, say so clearly — it's the most reassuring honest thing you can tell them.

**Rank threat vectors, not just overall risk.**
Cyberattack on infrastructure vs. physical attack vs. lone actor inspired attack have different precautions. Name each likely vector separately with TWO probabilities:
- **Broadly** — does this type of attack occur anywhere in the US in this context?
- **You** — does it affect this specific family, location, and profile?

These will often differ by an order of magnitude. State both. Collapsing them into one number is the single most common source of inflated personal risk estimates.

**Trajectory matters as much as score.**
A 5/10 that's escalating fast is more urgent than a 7/10 that's been stable for months.

**Don't catastrophize, don't minimize.**
False comfort is as bad as false alarm. Be accurate. Let the score speak.

**Always note what would change the assessment.**
"If X happened, this would move from MODERATE to HIGH." This gives the user a monitoring framework.

---

## Step 5: Generate HTML Report

After completing the text assessment, generate an interactive visual dashboard.

### How it works

The template at `.claude/skills/threat-analysis/report-template.html` is a complete
self-contained HTML dashboard. **You only need to replace the JSON data block** — the
HTML, CSS, and JS are static and handle all rendering automatically.

### Instructions

1. **Read the template:**
   ```bash
   cat .claude/skills/threat-analysis/report-template.html
   ```

2. **Replace the JSON data** inside `<script id="threat-data" type="application/json">` with
   your actual assessment values. The JSON schema:

   ```json
   {
     "score": 6.2,
     "level": "MODERATE",
     "levelColor": "#eab308",
     "location": "Berkeley, CA",
     "threatActor": "Iranian Government / Proxies",
     "context": "One sentence describing the triggering situation",
     "date": "April 7, 2026",
     "assumptions": "Private individual, no prior threats, no public profile",
     "dimensions": {
       "probability": { "score": 5, "text": "One-line reasoning" },
       "specificity": { "score": 4, "text": "One-line reasoning" },
       "capability":  { "score": 7, "text": "One-line reasoning" },
       "imminence":   { "score": 8, "text": "One-line reasoning" },
       "impact":      { "score": 8, "text": "One-line reasoning" }
     },
     "trajectory": {
       "direction": "ESCALATING",
       "color": "#ef4444",
       "icon": "↑",
       "text": "Explanation of trajectory direction",
       "triggers": ["Trigger 1", "Trigger 2", "Trigger 3"]
     },
     "findings": [
       { "text": "Finding text", "source": "Source name — Date" }
     ],
     "uncertainties": ["Uncertainty 1", "Uncertainty 2"],
     "assessment": "Full calibrated assessment paragraph",
     "scoreUp": "What would raise the score",
     "scoreDown": "What would lower the score",
     "vectors": [
       {
         "name": "Vector name",
         "probabilityBroad": "~35%",
         "probabilityPersonal": "~7%",
         "description": "Why this vector, what it looks like. 'Broadly' = does this type of attack happen anywhere in the US? 'You' = does it affect this specific family/location?"
       }
     ],
     "actions": {
       "tier1": ["Action 1", "Action 2"],
       "tier2": ["Action 1", "Action 2"],
       "tier3": ["Action 1", "Action 2"]
     },
     "reassess": "Reassess when condition X or Y occurs",
     "sources": [
       { "title": "Source title", "date": "Date", "unverified": false }
     ],
     "prior": {
       "score": 4.0,
       "level": "ELEVATED",
       "date": "April 7, 2026",
       "bitId": "1772050948"
     }
   }
   ```
   Set `"prior": null` if no prior assessment bit was found.

3. **Level color mapping** (use exact hex):
   - LOW (1–2): `#22c55e`
   - ELEVATED (3–4): `#84cc16`
   - MODERATE (5–6): `#eab308`
   - HIGH (7–8): `#f97316`
   - CRITICAL (9–10): `#ef4444`

4. **Trajectory icon and color:**
   - ESCALATING: icon `↑`, color `#ef4444`
   - STABLE: icon `→`, color `#eab308`
   - DE-ESCALATING: icon `↓`, color `#22c55e`

5. **Write the file:**
   ```bash
   # Write the full HTML (template + your JSON) to:
   mkdir -p /Users/tinkerbox/TinkerBot/scrap/reports
   # Save to: /Users/tinkerbox/TinkerBot/scrap/reports/threat-assessment.html
   ```

6. **Open it:**
   ```bash
   open /Users/tinkerbox/TinkerBot/scrap/reports/threat-assessment.html
   ```

### What the dashboard shows

- **Animated SVG gauge** — semicircle arc fills to the score with a needle indicator
- **Dimensional bars** — all 5 dimensions animate in with width proportional to score
- **Trajectory** — color-coded direction with trigger event list
- **Threat vectors** — ranked by probability with descriptions
- **Key findings** — bulleted with source citations
- **Calibrated assessment** — full text plus score-mover boxes (what raises/lowers)
- **Key uncertainties** — explicitly named
- **Tiered actions** — 3-column grid, color-coded by tier
- **Sources** — with UNVERIFIED flags where applicable

---

## Common Failure Modes

**Asking for inputs before researching.**
Do the research first. Most of what you need is in public sources + the conversation.

**Treating a broad national threat as personally specific.**
A DHS bulletin about general elevated threat is not the same as a specific warning about this city. Score Specificity honestly — don't inflate it.

**Scoring from the current conversation only.**
Run the searches. The situation is live and changes fast. Don't rely on what you already know.

**Omitting the disconfirmation pass.**
Actively search for evidence that contradicts your initial read. Finding nothing contradictory is the goal — but you have to look.

**Conflating cyber and physical attack risk.**
Name them separately. They have different probability, different impact, different precautions.

**Saying "no imminent threat" without a time horizon.**
Always specify the window your assessment covers: "No imminent threat in the next 48 hours based on available intelligence" is more useful than an unqualified "no imminent threat."
