# Contributing to LLM-Wiki

Thank you for considering a contribution. This is a vault template — improvements to the schema, workflows, or included knowledge benefit all users.

---

## What's In Scope

- Improvements to `CLAUDE.md` workflows (Ingest, Query, Lint, MOC, Log Rotation, Promotion)
- New or improved note templates in `Atlas 🧠/_System/templates/`
- New or improved worked examples in `Atlas 🧠/_System/misc/`
- Bug fixes: broken wikilinks, stale index entries, incorrect cross-references
- README and documentation improvements
- New generic concept pages (AI Engineering, Testing, API design, system design, etc.)
- New generic entity pages (tools, frameworks, companies)

## What's Out of Scope

- Personal knowledge tied to one person's projects, clients, or study plan
- Venture/client-specific pages or named project tags
- Personal data or identifying info in demo content
- Major Obsidian plugin configuration changes (`.obsidian/`); minimal pre-config only
- Content from copyrighted sources without a permissive licence

---

## How to Contribute

1. Fork the repo and create a branch from `main`
2. Make changes following the existing conventions (see `CLAUDE.md → Conventions`)
3. Open the vault in Obsidian, run a Claude Code lint pass (`lint the vault`), verify zero broken wikilinks
4. Submit a pull request with a clear description of what changed and why

---

## File Conventions

- YAML frontmatter with `tags:` as a list on every page
- Internal links always use `[[WikiLinks]]`
- Every concept page has `source: ai`, `source: human`, or `source: collab`
- Log entries use `## [YYYY-MM-DD] action | Description`
- Concept pages live in `Atlas 🧠/[domain]/` — not in `1-Literature Notes/`
- Literature notes live in `Atlas 🧠/1-Literature Notes/[topic]/` — not in domain folders

---

## Issues

Open an issue for:
- Schema bugs (a workflow step that doesn't work as described)
- Missing templates for common use cases
- Broken cross-references in the included knowledge base
- Suggestions for new generic concept pages
