---
name: plan
description: >
  Guide strategic thinking sessions before committing to work. Use when the user
  wants to think through a problem, evaluate options, or make decisions before
  jumping into implementation. Triggers on "let's plan", "let's think through",
  "let's figure out", "what should we do about", "how should we approach",
  "before we start building". Prevents premature implementation-level planning.
---

# Plan Skill

## Purpose

Facilitate structured strategic thinking BEFORE committing to work. Produces a
lightweight planning artifact (saved as a bit) that captures the problem, options
considered, decision made, and next actions.

## When to Invoke

- User wants to think through a problem before starting work
- Conversation is drifting into implementation details without agreement on the "what"
- Multiple possible directions and we need to choose
- Deciding whether something warrants a project, a process change, or nothing

## When NOT to Invoke

- Quick decisions that don't need structured thinking
- Pure research — use the `research` skill instead
- Already inside another strategic skill (e.g., `business-strategy`)

## The Anti-Pattern This Prevents

```
❌ User: "We need to improve our deploy process"
   AI: "Let me create a project plan with 5 phases, here's the acceptance criteria..."
   (Jumped to work items without thinking through what the actual problem is)

✅ User: "We need to improve our deploy process"
   AI: "Let's plan this. What specifically is broken about deploys right now?"
   (Stays in thinking mode until we've agreed on the problem and direction)
```

## Three Stages

### Stage 1: Frame

**Goal:** Agree on what we're actually trying to figure out.

**AI behavior:**
- Draft a clear problem/question statement based on what the user said
- Keep it to 2-3 sentences max
- Present it for refinement: "Is this what we're trying to figure out?"

**Do NOT:**
- Jump to solutions
- List options yet
- Mention implementation details

**Done when:** User agrees on the framing.

### Stage 2: Explore

**Goal:** Understand options, tradeoffs, and considerations.

**AI behavior:**
- Bring relevant context (check conversation history, search for related bits with `search_bits()`)
- Present options with honest tradeoffs — not a recommendation disguised as options
- Ask questions that help the user think through implications
- Stay at the strategic level — "we'd use X approach" not "we'd write a function that..."

**This is the main collaborative stage.** Could be a quick 2-exchange conversation or a
longer exploration depending on complexity. Follow the user's lead.

**Do NOT:**
- Make the decision for the user
- Drift into implementation details (file names, code structure, API design)
- Present a single option as if it's decided

**Done when:** Direction is clear and user is ready to decide.

### Stage 3: Decide

**Goal:** Record what we decided and what happens next.

**AI behavior:**
- Draft a decision summary capturing: problem framed, options considered, decision made, next actions
- Present it for approval
- On approval, save the planning artifact as a bit

**Next actions are explicit.** Examples:
- "Start building X" — begin implementation
- "Update process Z" — make the change
- "No action needed" — just the artifact as a record
- "Need more research on A before deciding" — defer with clear next step

## Planning Artifact

Save the artifact as a bit using `create_bit()` with type `decision` and tags
including `planning` plus relevant topic tags.

**Content format:**

```
## Problem

[The framing from Stage 1]

## Options Considered

### Option A: [name]
[Description, pros, cons]

### Option B: [name]
[Description, pros, cons]

[More options if applicable]

## Decision

[What we decided and why]

## Next Actions

- [ ] [Specific next step with owner/context]
- [ ] [Another step if applicable]
```

**The artifact is intentionally lightweight.** It's a decision record, not a specification.
Detailed planning happens when the actual work begins.

## Key Behaviors

**Stay strategic.** If the conversation drifts to "which CSS framework" or "what database
schema" — pull it back: "That's an implementation question. Let's nail down what we're
building first, and those details come during the build."

**Don't rush to decide.** The user might need to sit with options. It's fine to end Stage 2
with "let's think on this" and come back later. Note this in the bit with a `deferred` status.

**Honor the collaborative model.** AI brings first drafts, user refines. Don't present a
decision as if it's made — present a draft and ask what the user would change.
