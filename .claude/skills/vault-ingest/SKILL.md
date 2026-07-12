---
name: vault-ingest
description: When the user wants to ingest a source, process inbox notes, process clippings, add a new article or book or video to the vault, or expand a fleeting note. Also use when the user says "ingest this", "add this to the vault", "process the inbox", "process clippings", or "create a lit note for". Use this skill for all knowledge capture workflows in this Obsidian vault.
---

# Vault Ingest

You are the maintainer of this LLM-Wiki Obsidian vault. Follow the ingest workflow precisely.

## Step 0 — Read the vault index

Always read `index.md` first to understand existing pages before creating anything new.

Product context: !`cat index.md 2>/dev/null | head -80`

Today's date: !`date +%Y-%m-%d`

## Step 1 — Identify the source

Determine what is being ingested:
- **Fleeting note** in `00-Inbox/` root — your own rough jottings
- **Clipping** in `00-Inbox/Clippings/` — Obsidian Webclipper article (externally authored)
- **External source** — PDF, URL, Zotero annotation, book, video, course

For clippings: prefer reading the clipping file directly over fetching the URL again.

## Step 2 — Placement decision

Ask: is this **general knowledge** (→ `Atlas 🧠/` domain) or **source-bound** (→ `1-Literature Notes/`)?

**Literature Note placement:**
- Identify the **topic** (not the medium). E.g. a Udemy Python course → topic is `Python`
- Topic folder exists? → drop note there
- No folder, topic will grow (≥3 sources)? → create topic folder
- Otherwise → place at `1-Literature Notes/` root
- Name with a source signal: `Chip Huyen - AI Engineering.md`
- Tag: `#type/source/<book|course|video|article|paper|podcast>`

**Concept page placement (if promoting directly):**
- Domain: `💻 Product & Engineering`, `🎨 Brand & Identity`, `✍️ Content & Marketing`, `📈 Business & Growth`, `🤝 Customer Success & Experience`, `⚙️ Operations & Admin`
- Prefer updating an existing concept page over creating a new one

## Step 3 — Write the note

Use templates from `Atlas 🧠/_System/templates/`:
- `Literature Note Template.md` — for source-bound notes
- `Fleeting Note Template.md` — for rough inbox jottings being formalised

Standard frontmatter:
```yaml
tags:
  - type/source/<medium>          # for lit notes
  - domain/<domain>               # for concept pages
  - type/concept                  # for concept pages
status: evergreen                 # or stub
source: ai
```

## Step 4 — Update vault index and log

- Add a one-liner entry to `index.md` for any **new** pages created
- If a concept page grew significantly (≥1 new H2 or major rewrite), update its one-liner in `index.md`
- Append to `log.md`: `## [YYYY-MM-DD] ingest | Description`
- Update the relevant Topic MOC in `Atlas 🧠/0-Map of Content/Topics/` if one exists

## Step 5 — Dispose of the source

| Source type | Action |
|---|---|
| Fleeting note (own jottings) | Delete the inbox file |
| Clipping / Webclipper article | Move to `Archive/Clippings/` |
| Authored reference doc / roadmap | Move to appropriate `Archive/` subfolder |
| External source (PDF, URL) | Leave in place — no file to move |

## Project & client tags

Apply the relevant tag from your `CLAUDE.md` **Projects** table when knowledge is project/client-specific (e.g. `#project/myapp`, `#client/acme`). Leave untagged when the knowledge is universal.

## Key principle

Knowledge in `Atlas 🧠/` is **cross-project by default**. Ask: is this a universal principle or a project-specific implementation? Universal → concept page. Project-specific → add the relevant tag to an existing or new concept page.
