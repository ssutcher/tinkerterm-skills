---
name: publish-skill
description: >
  Publish one or more skills to the TinkerTerm public skill catalog on GitHub.
  Use when the user wants to add a skill to the TinkerTerm Library so it appears
  in the app's Browse Catalog modal. Triggers on "add to catalog", "publish this
  skill", "push to the skill catalog", "add to TinkerTerm Library", "publish to catalog".
---

# Publish Skill to TinkerTerm Catalog

## What This Does

Adds skills to the public TinkerTerm skill catalog hosted at `github.com/ssutcher/tinkerterm-skills`. Once pushed, skills appear in the TinkerTerm Library modal and can be installed by any TinkerTerm user.

## The Repo

- **GitHub:** `ssutcher/tinkerterm-skills`
- **Live catalog URL:** `https://raw.githubusercontent.com/ssutcher/tinkerterm-skills/main/catalog.json`
- **Local clone:** `scrap/workspace/tinkerterm-skills` (reuse if present, clone if not)

## Skill File Format

Each skill is a `.md` file with YAML frontmatter:

```
---
name: skill-name
description: One-line description of when to use this skill and what it does.
---

# Skill Title

## Section

Content...
```

**Rules:**
- `name` must be lowercase, alphanumeric, hyphens only (e.g. `design-luxury`, `code-review`)
- `description` is what the LLM reads to decide when to load the skill — make it trigger-phrase-rich
- Body is markdown procedural instructions

## Catalog Entry Format

Each entry in `catalog.json`:

```json
{
  "id": "skill-name",
  "name": "Display Name",
  "description": "One or two sentences shown in the Library UI.",
  "version": "1.0.0",
  "category": "design",
  "file": "skills/skill-name.md"
}
```

**Categories:** `creative`, `development`, `productivity`, `design`, `communication`, `data`

## Step-by-Step Workflow

### Step 1: Set Up the Repo

```bash
# Check if already cloned
ls /Users/tinkerbox/TinkerBot/scrap/workspace/tinkerterm-skills 2>/dev/null && echo "exists" || echo "missing"
```

If missing:
```bash
mkdir -p /Users/tinkerbox/TinkerBot/scrap/workspace && cd /Users/tinkerbox/TinkerBot/scrap/workspace && gh repo clone ssutcher/tinkerterm-skills
```

If exists, pull latest:
```bash
cd /Users/tinkerbox/TinkerBot/scrap/workspace/tinkerterm-skills && git pull
```

### Step 2: Read the Current Catalog

Always read `catalog.json` before editing — never blindly overwrite:

```bash
cat /Users/tinkerbox/TinkerBot/scrap/workspace/tinkerterm-skills/catalog.json
```

Check which skill IDs already exist so you don't create duplicates.

### Step 3: Write the Skill Files

For each skill, create `scrap/workspace/tinkerterm-skills/skills/{skill-name}.md` with proper YAML frontmatter + markdown body.

**If adapting from an external source under open license:**
- Include an `## Attribution` section at the bottom of the skill file
- Note the source and license (e.g. "Adapted from [TypeUI](https://typeui.dev) under the MIT License.")
- Include attribution in the git commit message too

### Step 4: Update catalog.json

Use Edit tool to append new entries to the `skills` array. **Never replace the entire file** — always preserve existing entries.

### Step 5: Commit and Push

```bash
cd /Users/tinkerbox/TinkerBot/scrap/workspace/tinkerterm-skills

# Stage only the files you created/modified
git add skills/skill-name.md catalog.json

git commit -m "Add [skill names]

[Attribution line if applicable]

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>"

git push
```

### Step 6: Verify the Live Catalog

Confirm GitHub's CDN is serving the updated data:

```bash
curl -s "https://raw.githubusercontent.com/ssutcher/tinkerterm-skills/main/catalog.json" \
  | python3 -m json.tool | grep '"id"'
```

All new skill IDs should appear in the output.

### Step 7: Sync to T2

T2 (TinkChat bot) also consumes skills from this catalog via Supabase. After publishing, sync:

```bash
cd ~/TinkerBot/t2/bot && source .venv/bin/activate && \
  SUPABASE_URL="https://hpqrjrzrjpfssmpkurcf.supabase.co" \
  SUPABASE_SERVICE_ROLE_KEY="$(ssh root@137.184.8.146 'grep SUPABASE_SERVICE_ROLE_KEY /opt/t2-bot/.env | cut -d= -f2')" \
  python3 seed_skills.py
```

**IMPORTANT:** Must use the **server's** Supabase keys — the server uses different JWT secrets than local `.env.primary`. Skills seeded with the wrong key will be invisible to the bot.

This fetches the updated catalog from GitHub and upserts all skills into Supabase. The live bot picks up new skills immediately (no restart needed — `list_skills` queries Supabase live).

### Step 8: Tell the User How to See It

**TinkerTerm:** Close and reopen the Library modal. The catalog is fetched fresh every time the modal opens — no app restart needed.

**T2 (TinkChat):** Skills are available immediately after Step 7. Ask the bot to `list_skills` to verify.

If skills still don't appear after reopening: GitHub's CDN sometimes caches for a few minutes. Wait 2-3 minutes and try again.

## Attribution Rules

| Source | What to do |
|--------|------------|
| MIT license | Include attribution in skill file footer + commit message |
| Apache 2.0 | Include attribution in skill file footer + commit message |
| Original / internal | No attribution needed |
| Unknown license | Ask the user before publishing |

## What NOT to Do

- Don't replace `catalog.json` wholesale — always preserve existing skills
- Don't use skill IDs that already exist in the catalog
- Don't publish skills with unknown licenses without checking with the user
- Don't forget to verify the live URL after pushing — CDN cache can mask failed pushes
