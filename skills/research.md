---
name: research
description: >
  Guide systematic research workflows that check existing knowledge before external searches.
  Use when the user asks to research, investigate, compare options, evaluate alternatives,
  find best practices, check known issues, or explore a topic. Triggers on "research",
  "investigate", "compare", "alternatives", "best practices", "known issues", "what library",
  "how should we build".
---

# Research Workflow

## When This Applies

User asks you to research, investigate, or evaluate something external — not just read internal code. If the answer is in the codebase, just read the code.

## The Four Rules

### 1. Check Existing Knowledge Before Going External

Before any WebSearch or external lookup:

`search_bits("[topic]")`

If existing knowledge answers the question, use it. If it partially answers, note what we know and only research the gaps. Previous sessions may have already solved this — don't redo work.

### 2. State Your Confidence

Every research response must include a confidence level:

- **HIGH** — Multiple credible sources agree, official docs confirm
- **MEDIUM** — Limited sources, but consistent signal
- **LOW** — Contradictions, sparse info, or speculation

Say why. "MEDIUM confidence — found two blog posts but no official docs" is useful. Just "MEDIUM" is not.

### 3. Be Honest About Gaps

If you can't find something, say so. Don't fill gaps with plausible-sounding guesses.

- Mark speculation clearly: "It appears...", "This suggests..."
- Note what you couldn't determine
- Cite every claim — no sourceless assertions

### 4. Save Your Research

After completing research, save the findings as a bit:

`create_bit(type: insight, project: [relevant-project], tags: source-research general-research [topic-slug])`

Start the content with `## Research: [Topic]` so it's identifiable in search results.
This ensures research is referenceable in future sessions and by downstream skills.

## Example

**User:** "Research what state management works well with React Server Components"

**Good:**
1. Checks existing bits first
2. Finds we haven't researched this before
3. Does external research
4. Returns findings with sources, states MEDIUM confidence, notes that RSC patterns are still evolving
5. Saves findings as a bit for future reference

**Bad:**
1. Jumps straight to WebSearch
2. Lists 6 options with no comparison
3. No confidence level
4. Presents everything as settled fact
5. Doesn't save findings — research is lost after the session
