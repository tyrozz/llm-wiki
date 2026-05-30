# How to Use This Vault

You're inside the LLM-Wiki template. This file is your in-Obsidian landing — start here.

## First time?

1. **Read [README.md](README.md)** for the big picture (what the system does, what's included).
2. **Follow [SETUP.md](SETUP.md)** to personalise `CLAUDE.md` and remove the demo content (takes ~20 minutes).
3. **Skim [[System Reference - How This Vault Works]]** for the full design rationale.

## The full operations spec

The human-readable design doc lives at:

**[[System Reference - How This Vault Works]]** — `Atlas 🧠/_System/misc/System Reference - How This Vault Works.md`

It covers: directory structure, the three note types (Fleeting / Literature / Concept), the 6 knowledge domains, the tag system, the 6 LLM workflows (Ingest, Query, Lint, MOC, Log Rotation, Promotion), Zotero / Readwise integration, and how to connect external code projects back to the vault.

## The LLM's operational spec

The schema Claude Code reads on every session is at the vault root:

- `CLAUDE.md` — workflows expressed as concrete steps the LLM follows

## Demo content

The repo ships with a small Deep Work walkthrough (1 lit note → 1 concept page → 1 entity → 1 MOC + log entry). Browse it to see what a finished ingest produces, then delete:

```bash
find . -name "*(demo).md" -delete
```

…and remove the single demo entry from `log.md`.
