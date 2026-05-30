# LLM-Wiki Operations Schema

You are the maintainer of this Obsidian vault. Your job is to incrementally build and maintain a persistent wiki — a structured, interlinked collection of markdown files.

## About This Vault

The owner is **[Your Name]**, a [your role — e.g. "solo founder", "software engineer", "researcher"] operating across [your context — e.g. "multiple projects", "a software team", "a research program"]. The 6 knowledge domains map to your primary areas of focus.

### Projects
<!-- Add one row per project, venture, client, or area of work. Add/remove rows as needed. -->
| Tag | Name | Description |
|---|---|---|
| `#project/myapp` | My App | One-line description of what it does |

### Key principle
Knowledge in `Atlas 🧠/` is **cross-project by default**. A concept page explains a universal principle. Venture/client tags mark where it has been specifically applied. When ingesting, ask: is this a general principle (goes in the domain) or a project-specific implementation (add the relevant tag)?

## Directory Rules

1. **Raw Sources (`Assets/` and external paths):** Immutable. Read from them, never modify them. PDFs do **not** need to be inside the vault — point to external paths (e.g. `~/Zotero/storage/`) when ingesting large files to keep the vault lean. Sub-structure of `Assets/`:
   - `Assets/raw/pdfs/` — short reference PDFs only; large books/papers stay in Zotero
   - `Assets/raw/articles/` — saved web articles
   - `Assets/raw/data/` — CSVs, JSON, structured files
   - `Assets/raw/writing/` — drafts before they become Outputs
   - `Assets/zotero_annotations/` — Zotero annotation exports (preferred ingest source)
   - `Assets/zotero_attachments/` — Zotero file attachments
   - `Assets/` root — Obsidian auto-pasted images (leave here)
2. **The Wiki (`Atlas 🧠/`):** You own this layer. Domain folders contain **permanent concept pages only** — synthesized, source-independent knowledge written in the owner's own words. These are the *output* layer: distilled understanding that stands alone without reference to any single source. Literature notes (source-bound) live in `1-Literature Notes/`, not in domain folders. Ensure all concept pages are categorized into one of the six primary domains:
   - `💻 Product & Engineering` — reusable code snippets live alongside the concept they implement (no `Snippets/` subfolder) and are tagged `#type/snippet`; discover them with `LIST FROM #type/snippet`
   - `🎨 Brand & Identity`
   - `✍️ Content & Marketing`
   - `📈 Business & Growth` — project / venture overview pages live here
   - `🤝 Customer Success & Experience` — client and volunteer overview pages live here
   - `⚙️ Operations & Admin`
3. **Literature Notes (`Atlas 🧠/1-Literature Notes/`):** Source-bound notes tied to a specific book, course, video, or article — the *input* layer. They capture what a source says, not synthesized understanding. They may eventually be promoted into permanent concept pages in the relevant domain folder. **Organise by topic, not by source type** (medium goes in tags). Use the templates in `Atlas 🧠/_System/templates/` — specifically `Literature Note Template.md` and `Fleeting Note Template.md`. Placement decision tree when ingesting a new source:
   - **Identify the topic** (the subject you'll return to across multiple sources), not the source title or medium. Example: a Udemy course on Python has the topic `Python`, not `Udemy` and not the course title.
   - **Topic folder exists?** → drop the note there. Use a sub-folder per source if the source has multiple parts (course modules, book chapters); use a single file otherwise.
   - **No topic folder?** → if the topic is likely to grow into a series (≥3 sources), create one (e.g. `AI Engineering/`, `Certifications/AWS Solutions Architect/`). Otherwise, place the note at `1-Literature Notes/` root.
   - **Name the file with a source signal** to keep multiple sources on the same topic distinguishable: `Chip Huyen - AI Engineering.md`, `Udemy - Python Bootcamp.md`, `AWS SAA-C03 Official Guide - Ch1-2.md`.
   - **Tag with `#type/source/<medium>`** (`book`, `course`, `video`, `article`, `paper`, `podcast`) — the medium lives in tags, not folders.
   - **Avoid duplicate basenames across the vault** — Obsidian's `[[Wiki Link]]` resolves by basename. If a name like `Roadmap.md` would collide with another file (e.g. an archived version), rename one (e.g. `Roadmap - 10-Week Bootcamp.md`).
   - **Superseded sources** → move to `Archive/` (at vault root), add `status/archived` tag + `superseded_by:` frontmatter field pointing to the replacement. Then grep for the old source's display text across all live `.md` files (excluding `Archive/` and `log.md`) and update every wikilink and description that names it. Example: `grep -rl "Old Title" . --include="*.md" | grep -v Archive/ | grep -v log.md` — then replace each stale reference with the new title.
4. **Entities (`Atlas 🧠/Entities/`):** First-class pages for tools, frameworks, companies, and people. Three sub-folders: `Tools & Frameworks/`, `Companies & Products/`, `People/`. Entities are distinct from concepts — they accumulate facts over time rather than explaining an idea.
5. **Maps of Content (`Atlas 🧠/0-Map of Content/`):** Topic-level entry pages for human navigation in Obsidian (graph view, "start here" landing pages). Distinct from `index.md`, which is the LLM's flat master map. Three sub-folders:
   - `Topics/` — one MOC per topic (e.g. `ai engineering.md`, `testing.md`). Links to all related concept pages, lit notes, templates, and outputs in a curated narrative order.
   - `Books/` — Dataview `LIST` queries over `#type/source/book*` tags.
   - `Videos/` — Dataview `LIST` queries over `#type/source/video*` tags.
   Create a Topic MOC when a topic accumulates ≥ ~4 concept pages or lit notes. Always cross-link MOCs from `index.md`.
6. **The Inbox (`00-Inbox/`):** Two purpose-built subfolders for the two input streams:
   - `00-Inbox/Fleeting Notes/` — your own rough jottings and scratch thinking, created manually.
   - `00-Inbox/Clippings/` — web articles saved via **Obsidian Webclipper**. Externally authored; land here automatically.

   The `00-Inbox/` root itself is a transient drop zone for files that don't yet have a home — process and relocate quickly.

   When asked to "process the inbox," read notes in BOTH subfolders (plus anything loose at root), expand them into the `Atlas 🧠/` domains, then dispose of each original per its type:
   - **Fleeting notes** (own rough jottings, scratch thinking) → **delete** — value fully transferred into the vault.
   - **Clippings / saved articles** (from `00-Inbox/Clippings/`, tagged `#clippings`, sourced from a URL, or externally authored) → **archive** to `Archive/Clippings/` — original wording and source metadata retain independent reference value.
   - **Roadmaps, reference docs, or structured files you authored** → **archive** to an appropriate `Archive/` subfolder.
7. **Outputs (`Outputs/`):** Final deliverables (essays, scripts, reports). Do not treat these as wiki source material.

## Core Workflows

### 1. Ingest Workflow
When asked to ingest a new source or process an inbox note:
- Read the source. This may be a file inside the vault, a Zotero annotation export (`Assets/zotero_annotations/`), or an external file path (e.g. `~/Zotero/storage/.../file.pdf`). **Prefer ingesting annotation exports over raw PDFs** — they reflect what the owner found important.
- Create a Literature Note (if external media) or integrate the knowledge directly into the relevant `Atlas 🧠/` domain folder. If a literature note for this source already exists, update it rather than creating a duplicate.
- Update existing concept pages if the new source adds detail, context, or contradictions. If you significantly expand an existing concept page (adding ≥1 new H2 section or substantially rewriting scope), also update its one-liner in `index.md` to reflect the current content.
- Append a timestamped entry to `log.md`.
- Update `index.md` with a link and a one-line summary of any new pages created.
- **Update the relevant Topic MOC** in `Atlas 🧠/0-Map of Content/Topics/` if one exists for the topic. If the topic now has ≥ ~4 concept pages or lit notes and no MOC exists, create one (see Workflow #4).
- **Dispose of the source file:** delete fleeting notes (own rough jottings); move clippings/saved articles (`#clippings` tag or external URL source) to `Archive/Clippings/`; move authored reference docs to an appropriate `Archive/` subfolder.

### 2. Query Workflow
When asked a question:
- Read `index.md` first to locate relevant concept pages in `Atlas 🧠/`.
- Synthesize an answer citing those pages.
- If the answer generates new, valuable insights or connections, write that insight back into the vault as a new concept page and update `index.md` and `log.md`.

### 3. Lint Workflow
When asked to "health-check" or "lint" the vault, run these checks in order:

1. **Orphan pages** — for each `.md` file in `Atlas 🧠/` (excluding `_System/`), take its basename and grep all other `.md` files for `[[<basename>`. If nothing links to it, it is orphaned. Command: `grep -rl "\[\[<basename>" . --include="*.md"` for each page. Flag orphans and suggest which `index.md` section or MOC should link them.

2. **Broken wikilinks** — extract all link targets from all live `.md` files and confirm each target exists as a `.md` file in the vault:
   `grep -roh "\[\[[^|\]]*" . --include="*.md" | sed 's/.*\[\[//' | sort -u`
   For each name, run `find . -name "<name>.md"`. Flag any that resolve to nothing.

3. **index.md coverage** — list all concept pages in `Atlas 🧠/` domain folders (excluding `_System/` and `1-Literature Notes/`) and confirm each has an entry in `index.md`. Flag any concept page missing a one-liner.

4. **Stale index one-liners** — for a representative sample of concept pages in `index.md`, read the page and check whether the one-liner still reflects the page's actual scope. If the page has grown significantly since it was first indexed, rewrite the one-liner.

5. **Contradiction scan** — for pairs of concept pages that cross-link to each other, check for conflicting definitions, metrics, or claims about the same topic. Flag conflicts for the owner to resolve. (Requires LLM judgment; focus on explicitly cross-linked pages.)

6. **Missing MOCs** — count concept pages + lit notes per topic. Any topic with ≥ ~4 pages lacking a Topic MOC in `Atlas 🧠/0-Map of Content/Topics/` should be flagged.

### 4. MOC Workflow
When asked to "create an MOC for [topic]" or when a topic crosses the ~4-page threshold during ingest:

- Create the file in `Atlas 🧠/0-Map of Content/Topics/[topic].md` with `type/concept` + `status/evergreen` (or `status/stub` if still thin) tags.
- Group links by section: Concept Pages, Templates, Literature Notes, Outputs, Related MOCs. Mirror the structure used in existing MOCs under `Atlas 🧠/0-Map of Content/Topics/`.
- Add a link to the MOC under the relevant domain section of `index.md`.
- For Book/Video lists, use Dataview `LIST FROM #type/source/<type>` queries inside `Books/` or `Videos/` rather than hand-maintained lists.

### 5. Log Rotation Workflow
When `log.md` exceeds 30 entries (check with `grep -c "^## \[" log.md`):

- Copy the oldest entries (everything beyond the newest 30) into `Archive/archived-logs.md`, appending below any existing content there. Preserve the exact entry text.
- Remove those same entries from `log.md`, keeping the header (first 5 lines) and the newest 30 entries.
- Append a rotation entry to `log.md`: `## [YYYY-MM-DD] maintenance | Log rotation. Moved N oldest entries to Archive/archived-logs.md. Active log reset to 30 entries.`

### 6. Promotion Workflow
When asked to "promote [lit note]" or "extract concept pages from [lit note]":

- Read the literature note in full.
- Identify 1–N distinct, universal concepts worth standing alone — knowledge that would be useful without knowing it came from this source. Exclude source-specific observations (quotes, page references, course-specific framing) — those stay in the lit note.
- For each identified concept:
  - **Concept page exists?** → enrich it with the new synthesized knowledge. Do not duplicate sections; integrate.
  - **No concept page?** → create one in the relevant `Atlas 🧠/` domain folder with standard frontmatter (`type/concept`, `status/evergreen`, `source: ai`).
- Add a `promotes:` field to the lit note's frontmatter listing the concept pages created or updated (e.g. `promotes: ["Branch Coverage", "Test Design Techniques"]`). The lit note itself is **not deleted** — it remains as the source record.
- Update `index.md` for any newly created concept pages.
- Update the relevant Topic MOC.
- Append a log entry: `## [YYYY-MM-DD] promote | Promoted [N] concept pages from [lit note title]: [list].`

## Conventions

- Use `[[WikiLinks]]` for all internal references.
- Every new page should have a `tags:` frontmatter property with at least one domain tag.
- Prefer updating existing pages over creating new ones when the concept already exists.
- Log format: `## [YYYY-MM-DD] action | Description`
- `source:` field values: `ai` (LLM wrote it), `human` (owner wrote it), `collab` (LLM drafted, owner significantly edited — mainly for `Outputs/`).
- Outputs in `Outputs/` can be written by the LLM, the owner, or both. When asked to draft an output, pull from existing concept pages in `Atlas 🧠/` and set `source: ai`. The owner edits and changes source to `collab` or `human` as appropriate.

---

## External Integrations

*This section is optional. See `NOTION_SETUP.md` to enable it.*

### Notion Databases

Notion is the team execution layer. The vault is the solo thinking layer. Only push *actions*
(tasks, projects, pipeline cards) to Notion — never knowledge or concept pages.

Fill in your database IDs after completing `NOTION_SETUP.md`:

| Database | ID | Use |
|---|---|---|
| Tasks | `<paste-id>` | All actionable tasks |
| Projects | `<paste-id>` | Active projects and initiatives |
| Areas | `<paste-id>` | Ongoing areas of responsibility |
| Content Pipeline | `<paste-id>` | Editorial calendar |

### Workflow 7 — Notion Sync

Triggered when the user says "add to Notion", "create a task", "brainstorm content",
"plan [X] for [period]", "sync to Notion", "add to content pipeline", or any planning
prompt tied to a specific hat.

**Pull phase** — run at the start of every planning/brainstorm session:
- Identify which hat the request belongs to and read the relevant Notion database(s) via MCP:
  - ✍️ Content hat → read Content Pipeline (all statuses: published, draft, planned)
  - 🎨 Brand / 💻 Product hat → read Tasks + Projects
  - 📈 Growth hat → read Content Pipeline + Tasks
  - ⚙️ Ops hat → read Tasks + Projects + Areas
- Summarise what already exists before generating anything new.

**Push phase** — after the user approves the plan:
1. Identify the relevant vault page(s) (concept page, blog draft, planning note).
2. Construct the `obsidian://` deep link:
   `obsidian://open?vault=<vault-name>&file=<URL-encoded-relative-path>`
3. **Project resolution** — before creating tasks, check if a matching Project exists:
   - Query Projects DB. If found → use it.
   - If not found → propose creating the project. Confirm name, Area link, and status
     (default: "In Progress") with the user. Create it, then link tasks to the new project.
   - If ambiguous (multiple partial matches) → present candidates, ask user to pick.
4. Create Notion records via MCP:
   - **Task**: title, Area link, Project link (resolved above), Obsidian Link, Status = "To Do"
   - **Content Pipeline**: title, type (Blog/Thread/Video/etc.), hat/domain, Obsidian Link, Status = "Idea"
5. Return the Notion record URLs so the user can share with the team.
6. Append to `log.md`.
