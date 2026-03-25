---
name: code-review
description: >
  Use when reviewing code, pull requests, or diffs. Covers security, performance,
  readability, and maintainability. Trigger phrases: "review this code", "check this PR",
  "what do you think of this implementation", "any issues with this?", "code review".
---

## Code Review Process

Review code in this order. Each layer builds on the previous.

### Layer 1: Correctness

Does the code do what it claims to do?

- Read the PR description or commit message first. Understand the intent.
- Trace the happy path. Does it produce the expected result?
- Trace the error paths. What happens when inputs are wrong, null, or missing?
- Check edge cases: empty arrays, zero values, undefined, concurrent access.
- Look for off-by-one errors in loops and array access.

**Output:** List of correctness issues with line references and suggested fixes.

### Layer 2: Security

Does the code introduce vulnerabilities?

**Check for:**
- SQL injection (string concatenation in queries)
- XSS (unsanitized user input in HTML output)
- Command injection (user input in shell commands)
- Path traversal (user input in file paths without validation)
- Hardcoded secrets (API keys, passwords, tokens in source)
- Insecure deserialization (untrusted JSON/YAML parsing with eval)
- Missing authentication/authorization checks on endpoints
- Overly permissive CORS or CSP headers

**Output:** Security findings with severity (critical/high/medium/low) and remediation.

### Layer 3: Performance

Will this code perform well at scale?

**Check for:**
- N+1 queries (database calls inside loops)
- Unnecessary re-renders (React: missing memo, deps arrays)
- Large allocations in hot paths
- Missing indexes on queried fields
- Unbounded data fetches (no pagination or limits)
- Synchronous I/O blocking the event loop
- Redundant computation that could be cached

**Output:** Performance concerns with estimated impact (critical path vs. cold path).

### Layer 4: Readability

Can another developer understand this code in 6 months?

**Check for:**
- Function/variable names that don't describe their purpose
- Functions longer than 30 lines (candidates for extraction)
- Deeply nested conditionals (> 3 levels)
- Magic numbers without named constants
- Inconsistent naming conventions within the file
- Missing or misleading comments (comments that say "what" instead of "why")
- Dead code or commented-out blocks

**Output:** Readability suggestions, prioritized by impact.

### Layer 5: Maintainability

Will this code be easy to change later?

**Check for:**
- Tight coupling between unrelated modules
- Duplicated logic that should be extracted
- Missing error handling at system boundaries
- Inconsistency with existing patterns in the codebase
- Missing types or overly permissive types (any, unknown abuse)
- Test coverage for new logic

**Output:** Maintainability recommendations.

## Review Output Format

Structure your review as:

```
## Summary
One paragraph: what this change does and overall assessment (approve/request changes/discuss).

## Must Fix
Issues that block merging. Each with:
- What: description of the problem
- Where: file and line reference
- Why: impact if not fixed
- Fix: suggested solution

## Should Fix
Issues worth addressing but not blocking. Same format.

## Nits
Minor style/preference suggestions. Brief, one line each.

## Praise
What was done well. Reinforces good patterns.
```

## Review Principles

1. **Review the change, not the person.** Say "this function" not "you wrote".
2. **Explain the why.** Don't just say "change this" — explain what goes wrong if they don't.
3. **Distinguish blocking from non-blocking.** Not everything is a must-fix.
4. **Acknowledge good work.** Point out clean implementations, good test coverage, clever solutions.
5. **Ask questions when unsure.** "Is this intentional?" is better than assuming a bug.
6. **One review, not death by a thousand comments.** Batch your feedback, don't comment on every line.
7. **Consider the context.** A quick fix has different standards than a core infrastructure change.

## Common Patterns to Flag

| Pattern | Risk | Suggestion |
|---------|------|------------|
| `catch (e) {}` | Swallowed errors | Log or rethrow |
| `any` type in TypeScript | Type safety bypass | Use specific type or `unknown` |
| `// TODO` without issue link | Forgotten work | Create issue or fix now |
| `console.log` in production code | Debug noise | Use structured logger |
| Hardcoded URLs or ports | Environment coupling | Use config/env vars |
| `setTimeout` for sequencing | Race condition risk | Use proper async/await |
| `==` instead of `===` | Type coercion bugs | Use strict equality |
