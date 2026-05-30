# Setup Guide — Personalising Your LLM-Wiki

Follow these steps after cloning. Takes about 20 minutes.

---

## Step 0: Remove demo content (optional)

The repo ships with a small Deep Work walkthrough so you can see how a finished ingest looks (1 literature note + 1 concept page + 1 entity + 1 MOC + 1 log entry). Once you've reviewed it:

```bash
find . -name "*(demo).md" -delete
```

Then open `log.md` and delete the single demo entry.

---

## Step 1: Open in Obsidian

1. Download [Obsidian](https://obsidian.md) if you don't have it.
2. `File → Open folder as vault` → select the cloned folder.
3. The bundled `.obsidian/` config pre-registers **Dataview** and **Templater** — accept the install prompts when Obsidian asks.

If you want extras:

| Plugin | Purpose | When to install |
|---|---|---|
| **Excalidraw** | Inline diagrams (`.excalidraw.md` files) | If you sketch architecture |
| **Obsidian Web Clipper** | Sends web articles directly to `00-Inbox/Clippings/` | If you save articles from the browser |
| **Zotero Integration** | Import Zotero annotation exports | If you read academic papers |

---

## Step 2: Install Claude Code

```bash
npm install -g @anthropic-ai/claude-code
```

Open a terminal in the vault folder. Run `claude` — it reads `CLAUDE.md` automatically on start.

---

## Step 3: Personalise CLAUDE.md

Open `CLAUDE.md` and update the `## About This Vault` section:

**Owner line** — replace with your name and role:

```
The owner is **[Your Name]**, a [your role] operating across [your context].
```

**Projects table** — one row per project, venture, client, or area of work:

```markdown
| Tag             | Name    | Description                  |
|-----------------|---------|------------------------------|
| `#project/myapp`| My App  | One-line description         |
| `#client/acme`  | Acme Inc| What they do                 |
```

Keep all **workflows** (Ingest, Query, Lint, MOC, Log Rotation, Promotion) exactly as-is — they are fully generic.

**Tag convention:** the slug in each row (e.g. `myapp`) is used consistently across every note. A note tagged `#project/myapp` is understood by Claude Code as specific to that project.

---

## Step 4: Personalise index.md

Replace the placeholder entries in:

- `📈 Business & Growth` → add wikilinks to your project / venture overview pages
- `🤝 Customer Success & Experience` → add wikilinks to your client pages

To create a project overview page:

1. Create `Atlas 🧠/📈 Business & Growth/My App.md`
2. Use `Permanent Note Template` from `Atlas 🧠/_System/templates/`
3. Add the project tag in frontmatter: `tags: [type/concept, "#project/myapp"]`

---

## Step 5: Run Your First Ingest

Two streams feed the vault, with different disposal rules:

| Source | Where it lands | After ingest |
|---|---|---|
| Your own jottings | `00-Inbox/Fleeting Notes/` (manual) | Deleted |
| Web article via Webclipper | `00-Inbox/Clippings/` (automatic) | Archived to `Archive/Clippings/` |
| Standalone source (PDF, paste) | `00-Inbox/` root | Disposed per type |

Drop a source in, then:

```
process the inbox
```

or for a single file:

```
ingest 00-Inbox/Clippings/[your-file].md
```

Claude Code will create the appropriate literature note or concept page, update `index.md` and the relevant topic MOC, log the operation, and dispose of the inbox file.

---

## Step 6: Run a Lint Pass

```
lint the vault
```

Six checks: orphan pages, broken wikilinks, index coverage, stale one-liners, contradiction scan, missing MOCs.

---

## Recommended First Week

| Day | Action |
|---|---|
| 1 | Personalise `CLAUDE.md` and `index.md`. Create your first project page. |
| 2 | Ingest one source you're actively studying. |
| 3 | Ask Claude Code a question — it synthesises from vault content. |
| 4 | Drop 3 fleeting notes from real work into the inbox. Process them. |
| 7 | Run a lint pass. Promote one lit note to a concept page. |

---

## Useful Commands

```
ingest [path]               # Process a single source into the vault
process the inbox           # Process everything in 00-Inbox/Fleeting Notes/ + Clippings/
promote [lit-note-path]     # Extract concept pages from a literature note
lint the vault              # Run all 6 health checks
rotate the log              # Move >30 oldest entries from log.md to Archive/archived-logs.md
what is [concept]?          # Query — synthesises from vault content
create an MOC for [topic]   # Build a topic Map of Content
```

---

## Step 7: Connect Notion (Optional)

If you use Notion for tasks, projects, or content planning, you can wire the vault to it so
Claude Code reads your databases before brainstorming and pushes tasks back with
`obsidian://` backlinks. Follow `NOTION_SETUP.md` — takes about 5 minutes.

---

## Going Deeper

For the full system design rationale, conventions, and integration patterns (Notion, Zotero, Readwise, external code projects), read:

- `Atlas 🧠/_System/misc/System Reference - How This Vault Works.md` — human-readable spec
- `Atlas 🧠/_System/misc/Example - *.md` — 6 step-by-step walkthroughs for ingesting different source types
