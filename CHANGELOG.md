# Changelog

All notable changes to this vault template are documented here.

Format: `## [version] — YYYY-MM-DD`

---

## [1.0.0] — 2026-05-30

Initial public release.

### Schema (`CLAUDE.md`)
- 6 core workflows: Ingest, Query, Lint, MOC Creation, Log Rotation, Promotion
- **Lint Workflow** — 6 numbered checks with grep commands (orphan pages, broken wikilinks, index coverage, stale one-liners, contradiction scan, missing MOCs)
- **Promotion Workflow** — extract 1–N concept pages from a literature note; marks lit note with `promotes:` frontmatter; lit note retained as source record
- **Log Rotation Workflow** — auto-trigger at >30 entries; rotate overflow to `Archive/archived-logs.md`
- **Snippets convention** — `#type/snippet`-tagged files live alongside the concept they implement (no dedicated `Snippets/` folder); discover via Dataview `LIST FROM #type/snippet`
- **Two-stream Inbox** — `00-Inbox/Fleeting Notes/` (manual jottings, deleted after ingest) + `00-Inbox/Clippings/` (Obsidian Webclipper articles, archived to `Archive/Clippings/` after ingest)

### Note Templates (`Atlas 🧠/_System/templates/`)
9 ready-to-use templates:
- Literature Note Template
- Fleeting Note Template
- Permanent Note Template
- Snippet Template
- Project CLAUDE.md Template (for downstream code projects)
- Output — Essay Template
- Output — Script Template
- Output — Thread Template
- Zotero Integration Template

### Worked Examples (`Atlas 🧠/_System/misc/`)
6 step-by-step ingest walkthroughs covering every source type:
- Example - Ingesting a PDF
- Example - Reading a Book
- Example - Reading Tool Docs *(for SDK and framework documentation)*
- Example - Studying for a Certification
- Example - Taking an Online Course
- Example - Watching a Video

### System Reference (`Atlas 🧠/_System/misc/System Reference - How This Vault Works.md`)
Comprehensive human-facing operations doc:
- Core philosophy (Library vs Lab, CODE + PARA mapping)
- Karpathy `llm-wiki` ↔ this vault mapping
- Zettelkasten note-type mapping (Fleeting / Literature / Permanent → Concept Page + `## My Take`)
- 6 knowledge domains explained
- Tag system (sources, knowledge types, content types, status)
- Promotion, Lint, Log Rotation workflows (cross-linked to `CLAUDE.md` for procedural detail)
- Zotero & Readwise integration patterns
- Vibe-coding workflow — connect external code projects back to the vault

### Demo Content
A self-contained Deep Work walkthrough showing how the pieces fit together:
- 1 literature note → 1 concept page → 1 entity page → 1 Topic MOC + matching `log.md` entry
- All demo files marked `(demo)` in filename and tagged `#status/demo` for one-command removal: `find . -name "*(demo).md" -delete`

### Repository Hygiene
- `LICENSE` — MIT
- `.gitignore` — Obsidian workspace state, OS noise (.DS_Store, Thumbs.db, etc.)
- `.github/ISSUE_TEMPLATE/` — bug report, feature request, schema question
- `.github/PULL_REQUEST_TEMPLATE.md`
- `CODE_OF_CONDUCT.md` — Contributor Covenant 2.1
- `.obsidian/` — minimal pre-config registering Dataview + Templater so first open works without manual plugin discovery

### Documentation
- `README.md` — repo landing page with feature overview
- `SETUP.md` — 7-step personalisation walkthrough
- `CONTRIBUTING.md` — what's in/out of scope, file conventions, contribution flow
- `How to use this vault.md` — vault-root orientation page
