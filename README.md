# TinkerTerm Skill Catalog

Downloadable skills for [TinkerTerm](https://github.com/ssutcher/mocky). Skills are procedural knowledge files that TinkerTerm's AI loads on demand.

## How It Works

TinkerTerm fetches `catalog.json` from this repo to discover available skills. Users can browse and install skills from within the app — no app update required.

## Catalog Format

`catalog.json` contains a version number and array of skill entries:

```json
{
  "version": 1,
  "skills": [
    {
      "id": "skill-name",
      "name": "Display Name",
      "description": "When to use this skill...",
      "version": "1.0.0",
      "category": "category-name",
      "file": "skills/skill-name.md"
    }
  ]
}
```

## Skill File Format

Each skill is a Markdown file with YAML frontmatter:

```markdown
---
name: skill-name
description: >
  When to activate this skill. Include trigger phrases and keywords.
---

# Procedural instructions in markdown
```

## Categories

- **creative** — Naming, writing, branding, design thinking
- **development** — Code review, debugging, architecture
- **productivity** — Notes, planning, organization

## Contributing

This catalog is curated. To suggest a skill, open an issue describing the use case.
