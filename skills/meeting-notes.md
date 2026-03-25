---
name: meeting-notes
description: >
  Use when summarizing meetings, extracting action items, writing follow-ups, or
  organizing discussion points from raw conversation. Trigger phrases: "summarize this meeting",
  "extract action items", "meeting notes", "what did we decide", "write a follow-up".
---

## Meeting Notes Process

### Step 1: Identify Meeting Type

Different meetings produce different outputs:

| Type | Primary Output | Secondary Output |
|------|---------------|-----------------|
| Decision meeting | Decisions made + rationale | Action items |
| Brainstorm | Ideas generated + clusters | Next steps |
| Status update | Progress summary | Blockers + risks |
| Planning | Plan outline + owners | Timeline + dependencies |
| 1:1 | Key topics discussed | Action items + follow-ups |
| Client/external | Summary for client | Internal action items |

### Step 2: Extract Structure

From raw meeting content (transcript, notes, recording summary), extract:

1. **Attendees** — Who was present
2. **Date and duration** — When, how long
3. **Agenda items** — What was discussed (in order)
4. **Decisions** — What was decided, by whom, with what rationale
5. **Action items** — What needs to happen, who owns it, by when
6. **Open questions** — What was raised but not resolved
7. **Parking lot** — Topics deferred to future discussion

### Step 3: Write the Summary

**Format:**

```
# Meeting: [Title]
**Date:** YYYY-MM-DD | **Duration:** Xm | **Attendees:** names

## Summary
2-3 sentences covering the meeting's purpose and outcome.

## Decisions
- [DECISION] Description of what was decided
  - Context: why this decision was made
  - Alternative considered: what was rejected and why

## Action Items
- [ ] [Owner] Action description — due [date]
- [ ] [Owner] Action description — due [date]

## Discussion Notes
### Topic 1
Key points discussed...

### Topic 2
Key points discussed...

## Open Questions
- Question that needs follow-up
- Question deferred to next meeting

## Next Meeting
Date/time if scheduled, or "TBD"
```

## Writing Principles

### Be specific, not vague
- Bad: "Discussed the timeline"
- Good: "Agreed to push launch from March 15 to April 1 due to auth integration delays"

### Capture decisions with rationale
- Bad: "Decided to use PostgreSQL"
- Good: "Decided to use PostgreSQL over MongoDB because the data is relational and we need ACID transactions for payment processing"

### Action items need three things
Every action item must have:
1. **Owner** — One specific person (not "the team")
2. **Action** — Clear, concrete task (not "look into X")
3. **Due date** — Specific date or "by next meeting"

- Bad: "Team will look into performance issues"
- Good: "[Sarah] Profile the /api/search endpoint and identify top 3 bottlenecks — by Friday 3/28"

### Distinguish facts from opinions
- Fact: "Revenue grew 15% month-over-month"
- Opinion: "The team feels the new onboarding is working well"
- Label opinions: "Sarah noted that..." or "The consensus was..."

### Keep it scannable
- Use headers, bullets, and bold for key terms
- Put the most important information first (decisions, action items)
- Discussion notes can be detailed but should be structured by topic

## Follow-Up Email Format

When asked to write a follow-up email from meeting notes:

```
Subject: [Meeting Title] — Summary & Action Items (MM/DD)

Hi team,

Quick summary from today's [meeting type]:

**Key Decisions:**
- [Decision 1]
- [Decision 2]

**Action Items:**
- [Owner]: [Task] — by [date]
- [Owner]: [Task] — by [date]

**Next Steps:**
[What happens next / when we meet again]

Full notes: [link if applicable]

Thanks,
[Name]
```

**Rules for follow-up emails:**
- Send within 2 hours of meeting end
- Lead with decisions and action items, not discussion recap
- Keep under 200 words (people skim)
- Link to full notes for anyone who wants detail

## Handling Incomplete Information

When the source material is incomplete:

- **Missing attendees:** Note "Attendees: [extracted names] + others"
- **Unclear decisions:** Mark as "[TENTATIVE]" and flag for confirmation
- **Missing owners:** Mark action items as "[UNASSIGNED]" and flag
- **Ambiguous timeline:** Use "by [best guess] (confirm)" notation
- **Inaudible/unclear sections:** Note "[unclear]" rather than guessing

Never fabricate details. Flag gaps explicitly so they can be filled.
