# TinkerTerm Skill Catalog — Schema

The canonical format for `catalog.json` and the file layout under `skills/`.

## Top-level shape

```json
{
  "version": 1,
  "skills": [ /* entries */ ]
}
```

## Entry shape (two forms — `file:` OR `dir:`, never both)

### Form A: single-file skill (`file:`)

```json
{
  "id": "skill-name",
  "name": "Display Name",
  "description": "When to use this skill, with trigger phrases.",
  "version": "1.0.0",
  "category": "development",
  "file": "skills/skill-name.md",
  "changelog": "Optional: what changed in this version"
}
```

The file at `skills/skill-name.md` IS the entire skill. Consumers fetch via:

```
https://raw.githubusercontent.com/ssutcher/tinkerterm-skills/main/skills/skill-name.md
```

### Form B: folder-shaped skill (`dir:`)

```json
{
  "id": "skill-name",
  "name": "Display Name",
  "description": "...",
  "version": "1.0.0",
  "category": "development",
  "dir": "skills/skill-name/",
  "changelog": "..."
}
```

The folder MUST contain a `SKILL.md` at its root. Other files (scripts, references, helper docs) are optional. Consumers discover the file list at install time via:

```
https://api.github.com/repos/ssutcher/tinkerterm-skills/contents/skills/skill-name
```

…and fetch each via:

```
https://raw.githubusercontent.com/ssutcher/tinkerterm-skills/main/skills/skill-name/<file>
```

GitHub's unauthenticated API rate limit is 60 requests/hour — sufficient for a desktop app that polls occasionally.

## Mutual exclusion

Each entry has **exactly one** of `file:` or `dir:`. An entry with both, or neither, is invalid. Consumers that don't understand `dir:` (e.g., older readers) should skip those entries rather than fail.

## Installed-state convention (`tink_*` frontmatter)

Tink Skills (and any other installer that adopts this convention) writes the following keys into the installed skill file's YAML frontmatter so it can track install state without a separate manifest file.

### Single-file skill (Form A) — `tink_checksum` (scalar)

```yaml
---
name: skill-name
description: ...
tink_source: ssutcher/tinkerterm-skills
tink_version: 1.0.0
tink_checksum: <sha256-of-the-installed-md>
---
```

### Folder-shaped skill (Form B) — `tink_checksums` (map)

The `tink_*` keys live in the folder's `SKILL.md` frontmatter (not a separate file):

```yaml
---
name: skill-name
description: ...
tink_source: ssutcher/tinkerterm-skills
tink_version: 1.0.0
tink_checksums:
  SKILL.md: <sha256>
  helpers/example.sh: <sha256>
  references/spec.md: <sha256>
---
```

Update detection: an installer hashes each file on disk and compares to the stored `tink_checksums:` map; mismatches mean a user has edited the skill locally.

This convention is verified safe against Claude Code's skill loader — see TinkerBot's Epic 286 Story 002 (loader confirmed to accept unknown frontmatter keys in both `tterm` and vanilla `claude` CLI, 2026-06-09).

## Categories

Current vocabulary (informal — add as needed): `strategy`, `design`, `productivity`, `creative`, `development`, `testing`.

## Versioning

Each skill entry has its own semver `version:`. The top-level catalog `version: 1` describes the schema generation. If a future change is non-backward-compatible, bump to `version: 2` and document the migration here.
