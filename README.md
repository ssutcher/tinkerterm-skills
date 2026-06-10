# TinkerTerm Skill Catalog

Downloadable skills for [TinkerTerm](https://github.com/ssutcher/mocky) and [Tink Skills](https://github.com/ssutcher/tink-skills) (both install skills from this catalog into `~/.claude/skills/`). Skills are procedural knowledge files that Claude Code loads on demand.

## How It Works

Consumers fetch `catalog.json` from this repo to discover available skills, then fetch the skill content from `skills/` and install into `~/.claude/skills/`.

## Catalog Format

See **[SCHEMA.md](SCHEMA.md)** for the canonical schema. Two entry forms are supported:
- **`file:`** — single-file skills (one `.md`)
- **`dir:`** — folder-shaped skills (`SKILL.md` + optional supporting files)

## Contributing

This catalog is curated. To suggest a skill, open an issue describing the use case.
