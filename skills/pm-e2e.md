---
name: pm-e2e
description: Run E2E browser tests against any live or dev web app from a plain English journey description. No codebase required. Auto-triggers when the user says "test my website", "test that users can", "run a test on [URL]", "check that [feature] works at [URL]", "e2e test this", "can you test [journey] on [URL]", "does signup work on", "verify that [user flow]", "test [competitor] app", "run the [name] journey". Works on any publicly accessible web URL.
---

# PM E2E Testing Skill

## Purpose

Enable PMs and non-developers to run automated browser tests against any live web app
by describing user journeys in plain English. Claude generates the Playwright test,
runs it in a visible browser, and summarises the result.

No codebase access, no config, no test-writing knowledge required.

---

## Step 1 — Scaffold Check (once per TinkerBot install)

Before running any test, verify the scaffold is ready:

```bash
ls /Users/tinkerbox/TinkerBot/pm-tests/node_modules/@playwright 2>/dev/null && echo "READY" || echo "NEEDS_INSTALL"
```

If `NEEDS_INSTALL`:
```bash
cd /Users/tinkerbox/TinkerBot/pm-tests && npm install && npx playwright install chromium
```

This takes ~2 minutes the first time. After that it's instant.

---

## Step 2 — Gather Requirements

Extract from the user's message or ask conversationally:

| Required | What to ask |
|----------|-------------|
| **URL** | "What's the full URL of the app?" (must include https://) |
| **Journey** | "Walk me through what the user does — step by step." |
| **Auth** (if needed) | "Does this journey require login? If so, what credentials should I use?" |

**Don't over-ask.** If the URL and journey are clear from the message, go straight to generation.

**If the journey is vague** ("test signup"), ask one clarifying question:
> "What should the user see or land on after signing up? That helps me write the right assertion."

---

## Step 3 — Generate the Test

Write the test to: `/Users/tinkerbox/TinkerBot/pm-tests/e2e/[slug].spec.ts`

Slug: lowercase, hyphenated, descriptive. E.g. `signup-flow`, `checkout-guest`, `login-redirect`.

### Test structure

```typescript
import { test, expect } from '@playwright/test';

test('[plain English description of the journey]', async ({ page }) => {
  // Step 1: Navigate to the app
  await page.goto('https://full-url.com/path');
  await page.waitForLoadState('networkidle');

  // Step 2–N: User actions with comments
  await page.getByLabel('Email').fill('test@example.com');
  await page.getByRole('button', { name: 'Sign up' }).click();

  // Final assertion
  await expect(page).toHaveURL(/dashboard/);
  await expect(page.getByText('Welcome')).toBeVisible();
});
```

### Locator priority (best to worst)

1. `getByRole('button', { name: 'Submit' })` — most robust
2. `getByLabel('Email address')` — for form fields
3. `getByPlaceholder('Enter your email')` — fallback for unlabelled inputs
4. `getByText('Create account')` — for links and text elements
5. `locator('[data-testid="submit"]')` — if data-testid is visible in the page source
6. CSS/XPath selectors — last resort only

### Always include

- A comment on each step explaining what the user is doing
- A `waitForLoadState` after navigating to a new page
- At least one final assertion that confirms the journey succeeded
- Full URLs in `goto()` calls (not relative paths) unless baseURL is explicitly set

### Auth pattern (when login is needed)

```typescript
// Login first
await page.goto('https://myapp.com/login');
await page.waitForLoadState('networkidle');
await page.getByLabel('Email').fill('user@example.com');
await page.getByLabel('Password').fill('password123');
await page.getByRole('button', { name: 'Log in' }).click();
await page.waitForURL('**/dashboard');

// Now test the actual journey
await page.getByRole('button', { name: 'New Project' }).click();
// ...
```

---

## Step 4 — Run the Test

```bash
cd /Users/tinkerbox/TinkerBot/pm-tests && npx playwright test e2e/[filename].spec.ts 2>&1
```

The config sets `headless: false` — the browser opens visibly so the PM watches it run.
After the run, the HTML report opens automatically in the browser (pass or fail).

**If in TinkerTerm** (`$TTERM_SESSION_ID` is set), open the report in sidekick after the run:
```bash
curl -s "http://127.0.0.1:${TTERM_IPC_PORT:-19876}/sidekick?target=/Users/tinkerbox/TinkerBot/pm-tests/playwright-report/index.html&session=$TTERM_SESSION_ID"
```

---

## Step 5 — Summarise Results

Give a plain-English summary in this format:

**If passed:**
```
✓ Journey passed in [X]s.

[What was verified — 2-3 bullet points of what the test confirmed worked]

Report is open in your browser with screenshots and a full video recording.
```

**If failed:**
```
✗ Journey failed at: "[step description]"

What happened: [plain English explanation of what the browser saw vs what was expected]

Likely cause: [your best assessment — missing element, wrong selector, unexpected redirect, etc.]

Want me to fix the test and retry, or is this a real bug in the app?
```

Do NOT show raw error messages or stack traces to the PM. Translate them.

---

## Step 6 — Offer Next Steps

After every run, offer:

```
Options:
- Save this journey to run again later
- Test another user flow
- [If failed] Fix and retry
```

---

## Saving a Journey

When the PM wants to save:

1. Copy the test: `pm-tests/e2e/[slug].spec.ts` → `pm-tests/saved/[slug].spec.ts`
2. Add an entry to `pm-tests/journeys.md`:

```markdown
## [Journey Name] — [App/Company]
- **URL**: https://example.com
- **Journey**: [Plain English description]
- **File**: `saved/[slug].spec.ts`
- **Last run**: [date] ✓
```

---

## Re-running a Saved Journey

When the PM says "run the [name] journey" or "re-run saved [name] test":

1. Find it in `pm-tests/journeys.md`
2. Run: `cd pm-tests && npx playwright test saved/[slug].spec.ts 2>&1`
3. Update the `Last run` date in `journeys.md`

---

## Common Failure Patterns & How to Handle Them

| Symptom | Likely cause | Fix |
|---------|-------------|-----|
| Element not found | Selector is wrong or element hasn't loaded | Add `waitForLoadState` or `waitForSelector` before the action |
| Timeout on navigation | Slow server or wrong URL | Increase `navigationTimeout` or check the URL is correct |
| `strict mode violation` | Locator matches multiple elements | Use a more specific locator (add `{ exact: true }` or narrow the context) |
| Test passes but wrong page | Assertion too loose | Tighten the URL pattern or check for more specific text |
| Login fails | Credentials wrong or login flow uses OAuth | Ask the PM for correct credentials or walk through the actual login manually first |

---

## What This Is NOT For

- Tests against `localhost` (use the main r2 e2e suite for that)
- Tests that require database access or seeded test data
- Load testing or performance testing
- Tests that need to stay in sync with production code (use r2's test suite)

This is for **quick, ad-hoc journey verification** against any live URL.
