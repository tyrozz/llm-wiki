# LLM-Wiki — Obsidian Vault Template for AI-Powered Knowledge Management

An Obsidian vault pre-wired for [Claude Code](https://claude.ai/code) as its AI operator. Implements the Karpathy-style "LLM-Wiki" pattern: a structured, interlinked knowledge base that an LLM actively builds and maintains alongside you.

This is a **template**: clone it, personalise `CLAUDE.md`, delete the demo content, and you have a working second brain.

---

## How It Works

1. **`CLAUDE.md`** — the operations schema. Tells Claude Code who owns the vault, what the folder structure means, and exactly how to run each of the 6 core workflows (Ingest, Query, Lint, MOC Creation, Log Rotation, Promotion).
2. **Claude Code** — the AI operator. Opens the vault, reads `index.md` for navigation, and executes workflows on demand.
3. **Obsidian** — the interface. Browse notes, explore the graph view, use Dataview queries, write in context.

You give Claude Code plain-English commands:

```
ingest 00-Inbox/Clippings/my-article.md
process the inbox
promote Atlas 🧠/1-Literature Notes/AI Engineering/Roadmap.md
lint the vault
rotate the log
what are the tradeoffs between REST and GraphQL?
```

...and it builds the wiki for you.

---

## What's Included

| Layer | What it ships |
|---|---|
| **Schema** | `CLAUDE.md` — 6 workflows with concrete steps and grep commands |
| **System Reference** | `Atlas 🧠/_System/misc/System Reference - How This Vault Works.md` — full human-readable spec of the system |
| **Note Templates** | 9 templates in `Atlas 🧠/_System/templates/`: literature note, fleeting note, permanent note, snippet, project CLAUDE.md, 3 output types, Zotero integration |
| **Worked Examples** | 6 step-by-step ingest walkthroughs in `Atlas 🧠/_System/misc/`: PDF, book, SDK/framework docs, certification, online course, video |
| **Demo Content** | A self-contained Deep Work walkthrough (1 lit note → 1 concept page → 1 entity → 1 MOC + log entry). All marked `(demo)` for one-command removal |
| **Scaffold** | All 6 domain folders, Entities sub-folders, 0-Map of Content (Topics/Books/Videos), two-stream Inbox (Fleeting Notes/ + Clippings/), Archive, Assets, Outputs — empty and ready |
| **Repo hygiene** | `LICENSE` (MIT), `.gitignore`, `.github/` issue + PR templates, `CODE_OF_CONDUCT.md`, minimal `.obsidian/` pre-config |

---

## Quick Start

```bash
git clone https://github.com/tyrozz/llm-wiki
cd llm-wiki
```

1. Open the folder in Obsidian (`File → Open folder as vault`). The bundled `.obsidian/` pre-registers Dataview and Templater — accept the install prompt.
2. Install Claude Code: `npm install -g @anthropic-ai/claude-code` (see [claude.ai/code](https://claude.ai/code))
3. Open a terminal in the vault folder and run `claude`
4. Follow [SETUP.md](SETUP.md) — about 20 minutes to personalise `CLAUDE.md` for your own projects

### Removing the demo content

The repo ships with a small Deep Work walkthrough so you can see how the pieces fit together. Once you've reviewed it:

```bash
find . -name "*(demo).md" -delete
```

Then open `log.md` and delete the single demo entry.

---

## Folder Structure

```
├── CLAUDE.md                        # Operations schema — Claude Code reads this first
├── index.md                         # LLM navigation map (one-liner per page)
├── log.md                           # Append-only operations record (rotates at 30 entries)
├── How to use this vault.md         # Orientation page (read this in Obsidian first)
├── README.md / SETUP.md / etc.      # GitHub-facing docs
│
├── .github/                         # Issue + PR templates
├── .obsidian/                       # Pre-config: Dataview + Templater registered
│
├── 00-Inbox/
│   ├── Fleeting Notes/              # Your own jottings (deleted after ingest)
│   └── Clippings/                   # Obsidian Webclipper articles (archived after ingest)
│
├── Atlas 🧠/                        # The wiki — Claude Code owns this layer
│   ├── 0-Map of Content/
│   │   ├── Topics/                  # Topic MOCs (created at ≥4 pages per topic)
│   │   ├── Books/                   # Dataview LIST over #type/source/book
│   │   └── Videos/                  # Dataview LIST over #type/source/video
│   ├── 1-Literature Notes/          # Source-bound notes (books, courses, articles)
│   ├── Entities/                    # Tools & Frameworks / Companies & Products / People
│   ├── _System/
│   │   ├── templates/               # 9 note templates
│   │   └── misc/                    # 6 worked examples + System Reference
│   ├── 💻 Product & Engineering/    # Permanent concept pages
│   ├── 🎨 Brand & Identity/
│   ├── ✍️ Content & Marketing/
│   ├── 📈 Business & Growth/        # Project / venture overview pages (personalise)
│   ├── 🤝 Customer Success & Experience/  # Client overview pages (personalise)
│   └── ⚙️ Operations & Admin/
│
├── Outputs/                         # Finished essays, posts, scripts
├── Assets/                          # Raw source materials (PDFs, articles, data)
└── Archive/                         # Superseded sources, archived clippings, rotated logs
```

---

## The Page Types

| Page type | Location | Purpose |
|---|---|---|
| **Literature Notes** | `Atlas 🧠/1-Literature Notes/` | What a *source* says — tied to a specific book, article, course |
| **Concept Pages** | `Atlas 🧠/[domain]/` | What *you* know — synthesised, source-independent, permanent |
| **Entities** | `Atlas 🧠/Entities/` | The *things* you work with — tools, frameworks, companies, people. Accumulate facts over time rather than explaining an idea |

Ingest creates literature notes. The Promotion Workflow extracts concept pages from them when the knowledge matures enough to stand alone. Entities are the three-shelf reference layer (Tools & Frameworks / Companies & Products / People) that concepts and notes link out to.

Sitting above all three is the navigation layer: `index.md` is the LLM's flat master map (read first every session), while Maps of Content in `Atlas 🧠/0-Map of Content/` are the human's curated "start here" pages for the graph view.

---

## Notion Integration (Optional)

Connect the vault to Notion so Claude Code can **read** your databases before brainstorming
(avoiding duplicate ideas and work already in flight) and **push** tasks, projects, and
content pipeline cards back to Notion with `obsidian://` backlinks after a planning session.

See [`NOTION_SETUP.md`](NOTION_SETUP.md) — takes about 5 minutes once you have a Notion
integration token. The vault runs fine without it.

---

## Why This Pattern

Most note systems are passive. The LLM-Wiki pattern makes your knowledge base an active participant — an AI that reads, writes, and maintains it alongside you. Read the full rationale in [`Atlas 🧠/_System/misc/System Reference - How This Vault Works.md`](Atlas%20%F0%9F%A7%A0/_System/misc/System%20Reference%20-%20How%20This%20Vault%20Works.md).

---

## Optional: Power Up with Skills

Out of the box the vault runs entirely on **plain-English commands** — no extra setup, which keeps the learning curve gentle. If you later want repeatable shortcuts, you can add Claude Code **skills** (slash commands) under `.claude/skills/`. Each skill is just a folder with a `SKILL.md` carrying `name` and `description` frontmatter:

```markdown
---
name: wiki-ingest
description: Ingest a source into the vault — read it, write a literature note, update cross-references, append to the log.
---
```

That turns `process the inbox` into `/wiki-ingest`, `lint the vault` into `/wiki-lint`, and so on. **This template ships without any skills on purpose** — plain English is friendlier to start with, and skills are a power-user layer you add once the workflows are second nature.

---

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Schema improvements, new templates, new worked examples, and generic concept pages are welcome.

## License

MIT — see [LICENSE](LICENSE). Use freely, personalise fully.
