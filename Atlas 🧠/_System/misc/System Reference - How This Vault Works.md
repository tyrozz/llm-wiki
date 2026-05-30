# System Reference — How This Vault Works

Everything you need to understand, operate, and extend this vault. The single source of truth for system design decisions, conventions, and workflows.

---

## 1. Core Philosophy

This vault is **The Library** (Permanent Knowledge). It is distinct from **The Lab** (Notion).

- **Notion** is for _Action_: Projects, Tasks, Deadlines, Raw Inputs.
- **Obsidian** is for _Understanding_: Concepts, Patterns, Mental Models, Writing.

**The Golden Rule:** If it has a "Status" (To Do, In Progress), it belongs in Notion. If it is "Truth" (How Auth Works, Production Checklist, Brand Guidelines, Testing Principles), it belongs here.

This vault is maintained by an LLM (Claude) using the schema in `CLAUDE.md`. The master navigation map is `index.md`.

---

## 2. Where This Comes From

Built on three frameworks:

**Tiago Forte's Building a Second Brain (CODE + PARA)** — the overall philosophy: Capture → Organise → Distill → Express, with knowledge organised into Projects, Areas, Resources, Archives. This vault implements the full CODE loop and the Areas + Resources layers of PARA.

**Andrej Karpathy's LLM-Wiki pattern** — an LLM acts as active maintainer of a personal wiki, handling all the bookkeeping (cross-references, tagging, page updates) that typically kills knowledge management projects.

**Edward de Bono's Six Thinking Hats (1985)** — the 6 knowledge domains map to the 6 cognitive modes of a solo founder: Product, Brand, Content, Growth, Customer Success, Operations.

---

## 3. Directory Structure

```
Workspace/
├── CLAUDE.md                      ← LLM operational schema (read on every session)
├── index.md                       ← Master map of all concept pages
├── log.md                         ← Append-only record of all LLM operations
├── How to use this vault.md       ← Redirects here
│
├── 00-Inbox/                      ← Two input streams (Fleeting + Clippings). Processed on demand.
│   ├── Fleeting Notes/            ← Your own rough jottings (delete after ingest)
│   └── Clippings/                 ← Obsidian Webclipper articles (archive to Archive/Clippings/ after ingest)
│
├── Atlas 🧠/                      ← The Wiki. LLM owns this layer.
│   ├── 0-Map of Content/          ← Topic landing pages (human navigation)
│   │   ├── Topics/                ← One MOC per topic (ai engineering, testing, aws)
│   │   ├── Books/                 ← Dataview LIST queries over #type/source/book*
│   │   └── Videos/                ← Dataview LIST queries over #type/source/video*
│   ├── 💻 Product & Engineering/   # Snippets live alongside their concept, tagged #type/snippet
│   ├── 🎨 Brand & Identity/
│   ├── ✍️ Content & Marketing/
│   ├── 📈 Business & Growth/
│   ├── 🤝 Customer Success & Experience/
│   ├── ⚙️ Operations & Admin/
│   ├── Entities/
│   │   ├── Tools & Frameworks/    ← LiteLLM, LangGraph, etc.
│   │   ├── Companies & Products/  ← Anthropic, OpenAI, etc.
│   │   └── People/
│   ├── 1-Literature Notes/        ← Summaries of books, videos, courses, papers
│   │   └── Certifications/
│   └── _System/
│       ├── templates/             ← Note templates
│       └── misc/                  ← This file and other system docs
│
├── Assets/                        ← Immutable raw files. Never modify.
│   ├── raw/
│   │   ├── pdfs/                  ← Books, syllabi, course PDFs
│   │   ├── articles/              ← Saved web articles
│   │   ├── data/                  ← CSVs, JSON, structured files
│   │   └── writing/               ← Drafts before they become Outputs
│   ├── zotero_annotations/        ← Zotero annotation imports
│   ├── zotero_attachments/        ← Zotero file attachments
│   └── (root)                     ← Obsidian auto-pastes images here
│
└── Outputs/                       ← Final deliverables (essays, scripts, reports)
```

---

## 4. Karpathy's System vs This Vault

| Karpathy (`llm-wiki`) | This Vault | Notes |
|---|---|---|
| `raw/pdfs/` | `Assets/raw/pdfs/` | Books, syllabi, course PDFs |
| `raw/articles/` | `Assets/raw/articles/` | Saved web articles |
| `raw/assets/` | `Assets/` root | Obsidian auto-pastes images here |
| `raw/data/` | `Assets/raw/data/` | CSVs, JSON, structured files |
| `raw/writing/` | `Assets/raw/writing/` | Drafts before Outputs |
| `wiki/sources/` | `Atlas 🧠/1-Literature Notes/` | Summaries of external media |
| `wiki/concepts/` | `Atlas 🧠/<domain folders>/` | Concept pages inside 6 domains |
| `wiki/entities/` | `Atlas 🧠/Entities/` | Tools, companies, people |
| `wiki/topics/` (MOCs) | `Atlas 🧠/0-Map of Content/` | Topic landing pages + Dataview lists |
| `wiki/comparisons/` | — | Write inside domain folders for now |
| Schema file | `CLAUDE.md` | LLM reads this on every session |
| Index file | `index.md` | Master navigation map |
| Log file | `log.md` | Append-only operations record |

---

## 5. This Vault vs Zettelkasten

The note types map directly to Zettelkasten, just with different names:

| This Vault | Zettelkasten | What it answers |
|---|---|---|
| Fleeting note (`00-Inbox/`) | Fleeting Note | "I just thought/read something" |
| Literature Note | Literature Note | "What did this source say?" |
| Concept Page | Permanent Note | "What do I actually know about this?" |
| `## My Take` section | Personal interpretation | "How have I applied this?" |

The key difference from classic Zettelkasten: **the LLM does the initial synthesis** from literature notes into concept pages. You don't write concept pages from scratch — the AI drafts them, you fill in `## My Take`.

---

## 6. The Three Note Types

### Inbox (`00-Inbox/`)
Two purpose-built subfolders, two input streams. Both processed by the same trigger (`"process the inbox"`) but disposed differently after ingest:

| Subfolder | What lives here | Author | Disposal after ingest |
|---|---|---|---|
| `00-Inbox/Fleeting Notes/` | Your own rough jottings, half-formed ideas, questions, decisions | You | **Deleted** — value fully transferred into the wiki |
| `00-Inbox/Clippings/` | Web articles saved via **Obsidian Webclipper** | External (URL source, often tagged `#clippings`) | **Archived** to `Archive/Clippings/` — original wording and source metadata retain reference value |

The `00-Inbox/` root itself is a transient drop zone for files that don't yet have a home — process and relocate them quickly. Authored reference docs (roadmaps, structured files you wrote) get archived to an appropriate `Archive/` subfolder rather than deleted.

Full disposal rules: `CLAUDE.md` §Directory Rules → 6. The Inbox.

### Literature Notes (`Atlas 🧠/1-Literature Notes/`)
Tied to one specific source. Organized around what that source says.
- Created by the LLM when you say "ingest [source]"
- Has a `resource:` field pointing to the original file or URL
- Organized by the source's structure (chapters, sections)
- `source: ai` in frontmatter

### Concept Pages (`Atlas 🧠/<domain>/`)
Source-agnostic. One page per idea, as rich as your current understanding.
- Synthesized from one or more literature notes
- Organized around the concept itself, not around any source
- Updated every time a new source adds something relevant
- The most valuable pages over time — they compound across sources
- `source: ai` in frontmatter, but `## My Take` is always yours

### Maps of Content (`Atlas 🧠/0-Map of Content/`)
A fourth layer that is **not a note**, but a navigation aggregator. Two readers, two purposes:

| | `index.md` (root) | Topic MOC (`0-Map of Content/Topics/`) |
|---|---|---|
| Reader | LLM (read first on every session) | You, in Obsidian graph view |
| Scope | Whole vault, flat one-liners | One topic, curated narrative |
| Updates with | Every new page | Manually when the topic shifts |
| Best for | LLM routing | "Start here" landing pages |

Three sub-folders:

- `Topics/` — one MOC per topic. Create when a topic accumulates ≥ ~4 concept pages or lit notes. Examples: `ai engineering.md`, `testing.md`, `aws.md`.
- `Books/` — Dataview `LIST FROM #type/source/book*` queries. Auto-updates as you tag new sources.
- `Videos/` — Dataview `LIST FROM #type/source/video*` queries. Auto-updates as you tag new sources.

Topic MOCs should mirror the structure of [ai engineering.md](../../0-Map of Content/Topics/ai engineering.md) and [testing.md](../../0-Map of Content/Topics/testing.md) — group links by section: Concept Pages, Templates, Literature Notes, Outputs, Related MOCs. Every Topic MOC is also referenced from `index.md` under its domain section.

---

## 6.5 Lint Workflow

Trigger phrase: `"health-check the vault"` or `"lint the vault"`.

Six checks run in order against `Atlas 🧠/`:

1. **Orphan pages** — concept pages with no inbound `[[wikilinks]]` anywhere in the vault.
2. **Broken wikilinks** — `[[targets]]` that don't resolve to any `.md` file.
3. **`index.md` coverage** — concept pages in domain folders missing a one-liner in `index.md`.
4. **Stale `index.md` one-liners** — sampled pages whose one-liner no longer reflects current scope.
5. **Contradiction scan** — cross-linked concept-page pairs with conflicting definitions, metrics, or claims.
6. **Missing MOCs** — topics with ≥ ~4 pages but no Topic MOC in `Atlas 🧠/0-Map of Content/Topics/`.

Full procedural detail (exact grep commands, what to flag, how to suggest fixes): `CLAUDE.md` §Core Workflows → 3. Lint Workflow.

---

## 6.6 Promotion Workflow

Trigger phrase: `"promote [lit note]"` or `"extract concept pages from [lit note]"`.

Promotes one or more universal concepts out of a source-bound literature note into permanent domain concept pages. Key rules:

- The literature note is **NOT deleted** — it remains as the source record.
- Add a `promotes:` frontmatter field to the lit note listing the concept pages created/updated.
- If a concept page already exists, **enrich** it; don't duplicate.
- Update `index.md` for any newly created concept pages and the relevant Topic MOC.
- Append a `## [YYYY-MM-DD] promote | …` entry to `log.md`.

Full detail: `CLAUDE.md` §Core Workflows → 6. Promotion Workflow.

---

## 6.7 Log Rotation Workflow

Trigger phrase: `"rotate the log"`, or auto-triggered during any operation that pushes the active log past 30 entries.

`log.md` is the append-only operations record. To keep it scannable, it caps at 30 entries; older entries spill into [Archive/archived-logs.md](../../../Archive/archived-logs.md).

When `log.md` exceeds 30 entries (`grep -c "^## \[" log.md`):

- Copy entries beyond the newest 30 into `Archive/archived-logs.md` (append at bottom; preserve exact text).
- Remove those entries from `log.md`, keeping the header + newest 30.
- Append a rotation entry to `log.md`: `## [YYYY-MM-DD] maintenance | Log rotation. Moved N oldest entries to Archive/archived-logs.md. Active log reset to 30 entries.`

`log.md`'s own header (line 5) already points readers to `Archive/archived-logs.md` so historical context is one click away.

Full detail: `CLAUDE.md` §Core Workflows → 5. Log Rotation Workflow.

---

## 7. The Six Knowledge Domains

All synthesized knowledge in `Atlas 🧠/` belongs to one of these domains. They are **cross-venture by default** — a concept page on Brand Identity applies to all your businesses, not just one.

| Domain | What goes here |
|---|---|
| `💻 Product & Engineering` | Technical concepts, AI, architecture, code patterns, testing |
| `🎨 Brand & Identity` | Brand guidelines, design system, tone of voice |
| `✍️ Content & Marketing` | Content strategy, SEO, campaign notes, scripts |
| `📈 Business & Growth` | Business strategy, sales, revenue, metrics |
| `🤝 Customer Success & Experience` | Client protocols, user journeys, feedback loops |
| `⚙️ Operations & Admin` | Internal processes, workflows, tool guides |

---

## 8. Working Across Multiple Projects & Clients

### The core principle
Domain pages hold **universal knowledge**. Project/client tags in `## My Take` mark **where you applied it**.

> Example: A concept page on `RAG - Retrieval-Augmented Generation` explains RAG for everyone.
> Your `## My Take` says: *"Built this for [project] document chat. Used pgvector. Chunking at 512 tokens worked well. #project/myapp"*
> Next time you build RAG for a different project, that experience is already in the vault.

### Defining your projects

Maintain the canonical list of project / client / area tags in `CLAUDE.md` (`## About This Vault → Projects` table). Pick one slug per project and use it consistently in every `## My Take` and concept-page tag.

```
| Tag                | Name                                           |
|--------------------|------------------------------------------------|
| `#project/myapp`   | My App — one-line description                  |
| `#client/acme`     | Acme Inc — what they do                        |
| `#area/research`   | Personal research thread                       |
```

The slug after the `/` is what you'll type in every `## My Take` so make it short and memorable.

### Onboarding a new project or client
1. Add their tag to `CLAUDE.md` (About This Vault → Projects table)
2. Create an overview page in the appropriate domain (e.g. `📈 Business & Growth/` for a venture, `🤝 Customer Success & Experience/` for a client)
3. Drop any briefs or specs into `Assets/raw/pdfs/`
4. Say "ingest [brief]" to create a literature note from it

### Finding project-specific knowledge
Use Dataview inside Obsidian:
```dataview
LIST FROM #project/myapp
```
Or ask the LLM directly: *"What do I know about authentication for myapp?"*

### Cross-project learning
A lesson from one project automatically benefits all future projects:
1. You solve a problem on a project
2. Drop a fleeting note in `00-Inbox/Fleeting Notes/` describing the solution
3. LLM processes it → updates the relevant concept page
4. Tag with `#project/myapp` in `## My Take`
5. Next project with the same problem: the solution is already in the vault

### Project vs knowledge
- Active project management (tasks, timelines, deliverables) → **Notion**
- What you learned from the project → **this vault**
- The vault accumulates over time. Notion resets with each project.

---

## 9. The Tag System

**Folders for Topics. Tags for Types.** Never create folders for "Book Summaries" or "Snippets" — use tags.

### Source Tags
| Tag | Use Case |
|---|---|
| `#type/source/book` | Books |
| `#type/source/article` | Blog posts, docs, web articles |
| `#type/source/video` | YouTube, conference talks |
| `#type/source/paper` | Academic papers |
| `#type/source/course` | Udemy, Coursera, certification syllabi |
| `#type/source/podcast` | Key insights from audio |

### Knowledge Tags
| Tag | Use Case |
|---|---|
| `#type/concept` | Concept pages — mental models, definitions |
| `#type/entity` | Entity pages — tools, companies, people |
| `#type/snippet` | Reusable code blocks. **The only way snippets are organised — there is no `Snippets/` folder.** Drop the snippet alongside the concept it implements (e.g. a tRPC snippet lives in `💻 Product & Engineering/` next to backend concept pages; a Vercel AI SDK snippet lives in `💻 Product & Engineering/AI Engineering/`). Discover with `LIST FROM #type/snippet`. |
| `#type/guide` | How-to's and step-by-step processes |
| `#type/diagram` | Excalidraw files and architecture maps |
| `#type/meeting` | Technical decisions from client or team calls |

### Content Tags (Outputs/)
| Tag | Use Case |
|---|---|
| `#type/draft/script` | YouTube video scripts |
| `#type/draft/post` | Blog post drafts |
| `#type/draft/thread` | Twitter/LinkedIn threads |
| `#type/draft/newsletter` | Email newsletter drafts |

### Status Tags
| Tag | Meaning |
|---|---|
| `#status/stub` | Placeholder — needs work |
| `#status/wip` | Work in progress |
| `#status/evergreen` | Polished, trusted reference |
| `#status/deprecated` | Outdated — kept for reference only |

---

## 10. The `source:` Frontmatter Field

Every page has a `source:` field in its frontmatter.

- `source: ai` — the LLM wrote this page
- `source: human` — you wrote this
- `source: collab` — LLM drafted, you significantly edited or added your voice (mainly used in `Outputs/`)

A vault full of `source: ai` pages with empty `## My Take` sections means you're collecting, not learning.

---

## 11. The `## My Take` Convention

Every concept page and entity page has `## My Take` at the bottom. **This section is always yours — the LLM never writes in it.**

**What to write:**
- Where you applied this concept and what happened
- What surprised you or contradicted your assumptions
- What failed and why
- Which business or project it's relevant to (use venture/client tags here)

Leave the prompt question in place until you have something real to say. A blank `## My Take` is a signal that you've read about something but haven't yet used it.

---

## 12. Division of Labour

```
YOU                          AI (LLM)
───────────────────────────────────────────────────
Capture raw thoughts    →    Expand into wiki pages
Drop files in Assets/   →    Create literature notes
Ask questions           →    Synthesize from vault
Fill ## My Take         →    Everything else
Apply knowledge         →    Track cross-references
Onboard new clients     →    Update index + log
```

---

## 13. How Knowledge Compounds

1. You read a PDF → LLM creates a literature note
2. Literature note feeds into a concept page
3. You ask a question → LLM synthesizes from concept pages → answer
4. Good answer becomes a new concept page or updates an existing one
5. You fill `## My Take` with what you actually did with it
6. Next question on the same topic: answer is richer
7. Lesson from one client → concept page → benefits all future clients

Each iteration adds a layer. The vault gets more valuable the more you use it, not just the more you add to it.

---

## 14. LLM Trigger Phrases

| Say this | What happens |
|---|---|
| `"process the inbox"` | Reads both `00-Inbox/Fleeting Notes/` and `00-Inbox/Clippings/` (plus anything loose at root), expands notes into domains. Disposes per type: fleeting notes deleted; clippings archived to `Archive/Clippings/`; authored reference docs archived to appropriate `Archive/` subfolder. |
| `"health-check the vault"` / `"lint the vault"` | Runs the 6-check lint workflow (orphans, broken wikilinks, index coverage, stale one-liners, contradictions, missing MOCs). See §6.5. |
| `"promote [lit note]"` | Extracts universal concept pages from a source-bound lit note; the lit note stays put. See §6.6. |
| `"rotate the log"` | Moves oldest entries beyond 30 from `log.md` into `Archive/archived-logs.md`. Also auto-triggered during any operation that pushes the active log past 30. See §6.7. |
| `"ingest [source]"` | Reads source, creates literature note + concept pages, updates index + log |
| `"health-check the vault"` | Scans for orphans, broken links, contradictions, stubs |
| Ask any question | Reads `index.md`, synthesizes answer, writes new insights back if valuable |

All operations are logged in `log.md`.

---

## 15. Integration with Notion

**The core rule:** Notion manages *flow*; Obsidian stores *value*.

- **Notion** = action, status, deadlines, structured data, catalogues
- **Obsidian** = understanding, principles, patterns, permanent knowledge

---

### Which databases stay in Notion

These are purely action/flow databases — they never need to migrate to Obsidian:

| Database | Why Notion owns it |
|---|---|
| Tasks, Projects, Areas | Active work with statuses — classic Notion territory |
| Goals, Time Sessions, Events | Time-bound, trackable, need reminders |
| Issue Tracker | Status-driven, tied to active projects |
| Expenses, Invoices, Subscriptions | Structured financial data, needs filtering/formulas |
| Contacts, Clients | CRM-style relational data |
| Content Pipeline | Editorial calendar with statuses and deadlines |
| Feature Requests & Feedbacks | Collected input awaiting triage |
| Features | Product backlog with status |

---

### Databases that split between Notion and Obsidian

**Resources**
The most important one to get right. Resources (YouTube videos, articles, tools, repos) live in Notion as a catalogue. The Notion Resource card has an `Obsidian Link` field — leave it empty until you actually process the resource.

Workflow:
1. Resource lands in Notion with Status: `To review`
2. You review it — watch the video, read the article
3. If it contains permanent knowledge worth keeping → say *"ingest [notes or URL summary]"* in Obsidian
4. Obsidian creates a literature note → updates or creates concept pages
5. Copy the Obsidian note URL (right-click note → Copy Obsidian URL) → paste into the `Obsidian Link` field on the Notion card
6. Set Notion status to `Migrated`

If the resource is not worth ingesting (low quality, already known, superseded) → set status to `Archived` and move on.

**Notes**
Quick notes and meeting notes stay in Notion. If a note reaches permanent value — a decision, a principle, a how-to — move it to Obsidian and paste the Obsidian URL back into the Notion note.

**Topics**
Notion Topics = project-scoped context. Obsidian concept pages = universal knowledge. They overlap by area but serve different purposes. Don't try to sync them — let Notion Topics stay project-specific, let Obsidian pages stay universal.

**Asset Library**
Files and creative assets stay in Notion/storage. If an asset relates to a brand or design decision worth documenting → create a concept page in `🎨 Brand & Identity/` and link both ways.

---

### The Notion Resource card fields

From the Notion setup, each Resource card has:

| Field | Use |
|---|---|
| `Status` | `To review` → `Migrated` or `Archived` |
| `Type` | Collection, Video, Article, Tool, etc. |
| `Area` | Maps to one of the 6 domains |
| `Venture` | Which venture/client this is relevant to |
| `Obsidian Link` | Paste the Obsidian note URL here after ingesting |
| `Parent Resource / Sub-Resources` | Resource hierarchy for collections |

The `Obsidian Link` field is the connection point. An empty `Obsidian Link` means the resource hasn't been processed yet — it's a catalogue entry, not yet knowledge.

---

### The migration workflow (full loop)

```
Notion Resources (catalogue)
        ↓  review + decide it's worth keeping
"ingest [resource]" in Obsidian
        ↓
Literature note created in Atlas 🧠/1-Literature Notes/
        ↓  LLM synthesises
Concept page updated/created in Atlas 🧠/<domain>/
        ↓
Copy Obsidian URL → paste into Notion Obsidian Link field
        ↓
Set Notion status to Migrated
```

---

## 16. Zotero Integration & PDF Strategy

### The problem with putting PDFs in the vault

Large PDFs bloat the vault and cause sync issues. PDFs do **not** need to live inside the vault for the LLM to read them — they just need to be accessible as a file path on disk.

### Recommended setup

| What | Where | Why |
|---|---|---|
| Raw PDFs (books, papers) | Zotero library (outside vault) | Keeps vault small, readable in Zotero with highlights |
| Your highlights & annotations | `Assets/zotero_annotations/` (exported) | Small text files, syncs fine |
| Short reference PDFs | `Assets/raw/pdfs/` | Fine for small files you want co-located |

### The preferred ingest workflow (Zotero → Obsidian)

1. Read and highlight the PDF in Zotero as normal
2. Export annotations to Obsidian using the keyboard shortcut → file lands in `Assets/zotero_annotations/`
3. Say *"ingest Assets/zotero_annotations/[file].md"*
4. The LLM reads **your highlights**, not the raw PDF — the resulting literature note reflects what *you* found important, not a cold summary of the whole document

This is better than ingesting the raw PDF.

### Ingesting a large PDF directly (without Zotero)

If you need the LLM to read the raw PDF, point it at the file path directly — it does not need to be inside the vault:

> *"ingest ~/Zotero/storage/ABC123/bookname.pdf, pages 14–31"*

Zotero stores PDFs at `~/Zotero/storage/<key>/filename.pdf`. You can find the path by right-clicking the item in Zotero → Show File.

### Exporting annotations from Zotero

Set up a keyboard shortcut in Zotero (e.g. `Cmd+Shift+E`) bound to the Obsidian export action — see the [Zotero Integration plugin docs](https://github.com/mgmeyers/obsidian-zotero-integration) for the current binding setup.

### Alternative: Readwise Reader

Readwise Reader is a cloud-native reading app that handles PDFs, articles, newsletters, and web pages. It is the strongest Zotero alternative for this system because the Obsidian integration is automatic — no manual export step required.

**How it fits into this system:**

1. Upload or import a PDF into Readwise Reader
2. Read and highlight as normal (stored in Readwise cloud)
3. The official Readwise Obsidian plugin syncs all highlights to a folder in the vault automatically
4. Say *"ingest [synced highlight file]"* — same workflow as Zotero annotations

**Comparison:**

| | Zotero | Readwise Reader |
|---|---|---|
| Cost | Free | ~$8/month |
| PDF storage | Local + cloud sync (optional) | Readwise cloud |
| Obsidian sync | Manual export via hotkey | Automatic via plugin |
| Works with articles/web | No | Yes |
| Academic citation management | Yes | No |

**When to use which:**
- Academic papers, books with citations you need to manage → Zotero
- Articles, newsletters, general reading, or if you want zero-friction Obsidian sync → Readwise Reader

---

## 17. Ingesting a PDF When You Already Have Notes

If you've taken your own notes before asking the LLM to ingest a source, follow this protocol to avoid losing your work.

### The risk

The LLM rewrites the body of a literature note when ingesting. Any personal notes written *outside* `## My Take` (in Summary, Key Quotes, etc.) are treated as the LLM's territory and may be reorganized or overwritten.

### What is safe

`## My Take` is always yours. The LLM never writes in it. If your personal notes are there, they survive any ingest.

### The safe workflow

1. Drop the PDF in `Assets/raw/pdfs/`
2. Move any personal notes into `## My Take` of the existing literature note *before* triggering ingest
3. Say: *"ingest [PDF] — I already have a literature note at [path], update it rather than creating a new one"*
4. The LLM fills in the structured body (Summary, Key Quotes, Connections) from the PDF and leaves `## My Take` untouched

### Two-file scenario

If your personal notes are in a *separate* file (a fleeting note or a note you wrote from scratch), the ingest creates a new AI-written literature note and your file is not touched. Afterwards, either link the two files or say "merge my note at [path] with the ingested one."

### The rule of thumb

| Location | Owner | Safe from ingest? |
|---|---|---|
| `## My Take` | You | Yes — always |
| Body sections (Summary, Key Quotes, etc.) | LLM | No — may be rewritten |
| A separate personal file | You | Yes — ingest won't touch it |

---

## 18. Vibe Coding Workflow — Connecting Projects to the Vault

Your projects live in `/DEV/`. Your knowledge lives here. This section explains how to connect them so the vault actively improves your coding sessions.

### The core problem

Without a connection layer, every coding session starts from zero. You re-solve the same class of problem across every project without the solutions compounding.

### The connection layer: project CLAUDE.md

Every project should have its own `CLAUDE.md` at its root. It tells the LLM about the project *and* points back to relevant vault pages. A template is in `Atlas 🧠/_System/templates/Project CLAUDE.md Template.md`.

Key section to include:

```markdown
## Knowledge Base References
| Topic | Vault page |
|---|---|
| Auth | /path/to/your/vault/Atlas 🧠/💻 Product & Engineering/Auth Patterns.md |
| Client context | /path/to/your/vault/Atlas 🧠/🤝 Customer Success & Experience/Acme Inc.md |
```

When a coding session opens, Claude reads both the project CLAUDE.md and any vault pages you point it at.

### Before coding a feature

Ask the vault first:

> *"what do I know about JWT refresh token handling?"*
> *"what are the patterns for file upload in Next.js?"*

The LLM reads your concept pages and answers from your accumulated experience. If a concept page doesn't exist yet, the gap is visible — and worth filling before you start.

### During coding

Drop decisions into `00-Inbox/` as fleeting notes in real time. Keep it minimal — one paragraph is enough:

> *"decided to use pgvector over Pinecone for [project] document chat — already on Postgres, cheaper at scale, 512-token chunks worked well #project/myapp"*

### After solving something non-obvious

> *"process the inbox"*

The fleeting note becomes a concept page or updates an existing one. Tagged with the venture/client so it's findable. Next time you face the same problem — on a different project, months later — the solution is already there.

### The compounding loop

```
Project problem → solve it → fleeting note → 00-Inbox/
                                                  ↓
                                         "process the inbox"
                                                  ↓
                               concept page in Atlas 🧠/ (tagged)
                                                  ↓
                        next project with same problem → already solved
```

### Starting a new project

1. Create a client/project overview page in `🤝 Customer Success & Experience/`
2. Set up `CLAUDE.md` at the project root using the template
3. Add vault reference links to relevant concept pages
4. Check the vault for existing knowledge on the stack before writing any code

### What goes where

| | Notion | This vault | Project CLAUDE.md |
|---|---|---|---|
| Tasks, tickets, deadlines | ✓ | | |
| What you learned | | ✓ | |
| Why you made a decision | | ✓ | summary link |
| Project-specific conventions | | | ✓ |
| Reusable patterns & concepts | | ✓ | link to it |

---

## 19. CODE + PARA — How This Vault Implements Forte's Framework

### The full mapping

| Forte | This vault | Tool |
|---|---|---|
| **Capture** | `00-Inbox/` fleeting notes + Notion Resources DB | Obsidian + Notion |
| **Organise** | `Atlas 🧠/` 6 domain folders + `Assets/` | Obsidian |
| **Distill** | Literature Notes → Concept Pages → `## My Take` | Obsidian + LLM |
| **Express** | `Outputs/` folder | Obsidian |
| **Projects** | Notion (tasks, deadlines, active work) | Notion |
| **Areas** | `Atlas 🧠/` 6 domains (ongoing knowledge areas) | Obsidian |
| **Resources** | Notion Resources DB + concept pages | Notion + Obsidian |
| **Archives** | `#status/deprecated` pages, Notion archived resources | Both |

---

### Distill — how it works here

Forte's progressive summarisation distils a source into increasingly refined layers. This vault does it in three passes:

**Pass 1 — Literature Note**
The LLM reads the source and creates a structured summary tied to that source. Organised by the source's own structure (chapters, sections). This is a faithful summary, not an opinion.

**Pass 2 — Concept Page**
The LLM synthesises across one or more literature notes into a source-agnostic concept page. The concept page answers *"what do I actually know about this topic?"* — not *"what did this book say?"* This is where compression happens.

**Pass 3 — `## My Take`**
You write this. Where you applied the concept, what surprised you, what failed. This is the most distilled layer — personal, contextual, irreplaceable by AI. A blank `## My Take` means distillation is incomplete.

**The progressive summarisation principle:**
Each layer is shorter and more essential than the last. The concept page should be readable in 2 minutes and convey the core insight. If it's longer than that, it needs more distillation.

---

### Express — the Outputs folder

`Outputs/` is where distilled knowledge becomes a finished artefact. Forte calls this the payoff of the whole system — the point where captured knowledge creates real value in the world.

```
Outputs/
├── Essays/       ← Long-form thinking, published or not
├── Scripts/      ← YouTube, podcast, presentation scripts
├── Posts/        ← Blog posts, LinkedIn, newsletter issues
└── Threads/      ← Twitter/X threads
```

**Outputs are flexible — anyone can write them.** There is no rule that you must write outputs yourself, or that the LLM must draft them. Use whatever mode fits the situation:

| Mode | When to use | `source:` field |
|---|---|---|
| `source: ai` | LLM drafts from concept pages; you review and publish as-is or lightly edit | `ai` |
| `source: human` | You write from scratch, using concept pages as reference | `human` |
| `source: collab` | LLM drafts the structure and body; you rewrite sections, add your voice and examples | `collab` |

**The Express workflow:**

1. Identify a topic (2+ concept pages exist on it, or you know it well)
2. Open a new file in the relevant `Outputs/` subfolder using the appropriate template (`_System/templates/`)
3. Choose your mode:
   - **AI-led:** *"draft an essay on [topic] from my concept pages"* → review and edit
   - **Human-led:** write directly, using concept pages as reference material
   - **Collaborative:** *"give me an outline and opening for [topic]"* → you take it from there
4. Set `source:` in frontmatter to reflect who wrote it
5. Publish externally, or keep as a reference artefact

**Intermediate packets** (Forte's concept): not every Express output has to be a finished piece. A 3-paragraph explanation of RAG you wrote for a client email is an intermediate packet — worth saving in `Outputs/Posts/` as a draft because you'll reuse it.

**The key insight:** Express outputs should feel easy if Distill worked. If writing or prompting a post on a topic feels hard, it means the concept pages aren't deep enough yet — go back and distill more before expressing.

---

### Why this system survives where others fail

Most second brain attempts die at Distill — people capture endlessly but never synthesise. The LLM removes this bottleneck: it does the first two passes of distillation automatically. You only need to do the hardest and most valuable part: `## My Take` and the final Express output.

---

## See Also

- `CLAUDE.md` — full operational schema the LLM reads on every session
- `index.md` — master navigation map with links to all pages
- `log.md` — full history of all LLM operations
- `Atlas 🧠/_System/templates/Project CLAUDE.md Template.md` — template for project-level CLAUDE.md files
- `Atlas 🧠/🤝 Customer Success & Experience/` — client overview pages
