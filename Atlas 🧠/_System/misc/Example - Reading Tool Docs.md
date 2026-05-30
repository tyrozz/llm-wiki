---
title: "Example - Reading Tool Docs"
date: 2026-05-24
tags:
  - type/guide
  - status/evergreen
source: ai
---

# Real-World Example: Reading the Docs of a Tool or Framework

A walkthrough for ingesting the **documentation of a tool or framework** — SDK reference docs, framework user guides, CLI manuals, official tutorials. Distinct from one-shot articles because tool docs are *living* sources and they generate a 4-way split across the vault: entity facts, source notes, runnable code, and transferable concepts.

---

## When this applies

Use this workflow for:

- **SDK / API docs** (OpenAI Agents SDK, Anthropic SDK, Vercel AI SDK)
- **Framework user guides** (LangGraph, Next.js, Drizzle, tRPC)
- **CLI / tool manuals** (Claude Code, Zotero, Obsidian plugins)
- **Official tutorials** that walk through a specific tool end-to-end

Do **not** use this for:
- A one-shot article on a *concept* with no specific tool — use the standard ingest into a literature note
- A book about a tool — use [[Example - Reading a Book]] (multi-chapter structure)
- A video tutorial — use [[Example - Watching a Video]]

---

## The 4-way split

Reading tool docs always produces artefacts in up to four places. Knowing which goes where before you start prevents the most common mistake — dumping everything into a single lit note where it becomes unreusable.

| Artefact | Where it lives | Why |
|---|---|---|
| Facts **about** the tool (what it is, version, maintainer, when to pick it, known limits) | `Atlas 🧠/Entities/Tools & Frameworks/<Tool>.md` | Entity pages accumulate facts over time across sources |
| What the docs **say** (your reading notes, structured by the docs' own sections) | `Atlas 🧠/1-Literature Notes/<topic>/<Vendor> - <Tool> Docs.md` | Source-bound; new versions can supersede |
| Runnable **code** you'd copy into a project | A concept-adjacent file in the relevant domain folder, tagged `#type/snippet` | Snippets live with their topic, not in a separate folder ([[System Reference - How This Vault Works\|System Reference §9]]) |
| Transferable **patterns** that survive the tool (e.g. "Agent Loop Pattern" outlives any specific SDK) | A concept page in the relevant domain folder | Only created if the pattern is universal — most docs don't yield one |

---

## Phase 1: Create or find the Entity page

Tool docs are *about* a specific tool. Start by locating its entity page.

| Path | Tag | Frontmatter |
|---|---|---|
| `Atlas 🧠/Entities/Tools & Frameworks/<Tool>.md` | `#type/entity` | `source: ai` (initially) |

If the entity page doesn't exist, create it with at minimum:
- One-line description
- Maintainer / vendor
- When to reach for it (vs. alternatives in the same space)
- Link to the official docs

Keep code **out** of the entity page — code goes in snippets. The entity page should read like a Wikipedia stub, not a tutorial.

---

## Phase 2: Decide the topic and place the Literature Note

Topic = the broader subject the tool belongs to, not the tool's name. The lit note lives under that topic so future related sources cluster around it.

| Tool | Topic | Lit note location |
|---|---|---|
| OpenAI Agents SDK | AI Engineering | `1-Literature Notes/AI Engineering/OpenAI - Agents SDK Docs.md` |
| LangGraph | AI Engineering | `1-Literature Notes/AI Engineering/LangChain - LangGraph Docs.md` |
| Drizzle ORM | Backend / Data Layer | `1-Literature Notes/<topic-folder>/Drizzle - ORM Docs.md` |
| Next.js App Router | (no series yet) | `1-Literature Notes/Vercel - Next.js App Router Docs.md` (root) |

**Filename rule:** `<Vendor or Org> - <Tool> Docs.md` so multiple sources on the same tool stay distinguishable (vendor docs vs. a community guide vs. a book).

**Tag:** `#type/source/article` (or use `#type/source/docs` if you want a finer-grained source tag — but check [[System Reference - How This Vault Works\|System Reference §9]] hasn't already chosen one).

Organise the body by the docs' own structure (Getting Started, Core Concepts, API Reference, etc.) — same as the docs themselves. This is faithful summarisation, not synthesis.

---

## Phase 3: Capture runnable code as snippets

For each runnable code pattern worth keeping, create a separate file alongside the concept it implements:

- Backend / API pattern → `Atlas 🧠/💻 Product & Engineering/<Pattern Name>.md`
- AI Engineering pattern → `Atlas 🧠/💻 Product & Engineering/AI Engineering/<Pattern Name>.md`
- Brand / design pattern (rare) → `Atlas 🧠/🎨 Brand & Identity/<Pattern Name>.md`

**Snippet file structure** (use `Atlas 🧠/_System/templates/Snippet Template.md`):

```markdown
---
title: "Snippet - <Name>"
date: <YYYY-MM-DD>
tags:
  - type/snippet
  - status/evergreen
  - venture/<tag>  # optional: where you've used it
source: human  # or ai if generated from docs
---

## What It Does
## When To Use
## Code
## Gotchas
## Connections
## My Take
```

**Tag** `#type/snippet` is the **only** way snippets are organised — there is no `Snippets/` folder. Discover them with `LIST FROM #type/snippet` in Dataview.

**Threshold for creating a snippet:** would you copy-paste this code into a real project? If yes, snippet. If it's only meaningful as part of the lit note's narrative, leave it in the lit note.

---

## Phase 4: Spin out Concept pages only for transferable patterns

A single tool's docs rarely justify a new concept page. Spin one out **only** when the docs introduce a pattern that survives the tool itself.

| Pattern from docs | Concept page? | Why |
|---|---|---|
| "OpenAI Agents SDK handoff syntax" | ❌ Snippet only | Tool-specific syntax — no transferable principle |
| "Agent Loop Pattern" (think → act → observe → repeat) | ✅ Concept page | Universal across SDKs (Anthropic, OpenAI, LangGraph) |
| "Drizzle `db.query.<table>.findMany`" | ❌ Snippet only | ORM-specific API |
| "Multi-tenant org-scoping rule" (always filter by `organizationId`) | ✅ Concept page | Universal multi-tenant pattern, independent of ORM |

If the docs only crystallise something **you already had a concept page for**, update that page with a `## Connections` link to the new lit note rather than creating a duplicate.

---

## Phase 5: Cross-link everything

After Phases 1–4, link the artefacts to each other:

- **Entity page** → links to the lit note (under `## Sources`) and to any snippets and concept pages spun out
- **Literature note** → links to the entity page (top of file) and to any snippets / concept pages it produced
- **Snippets** → link back to the entity in `## Connections`, and to the lit note if a specific section explains them
- **Concept pages** → link to the entity in `## Connections` (as one of N implementations); list the lit note under `## Sources`

The graph view in Obsidian should show a tight cluster around the entity. If a snippet or concept is floating disconnected, it's an orphan ([[System Reference - How This Vault Works\|System Reference §3 Lint workflow]] will flag it).

---

## Phase 6: Fill `## My Take`

The lit note's `## My Take` is usually short (1–3 lines): your honest read on whether the docs are good, what's confusing, what you'd warn another reader about.

The **entity's** `## My Take` is the high-value one — it's where you record:
- When you reach for this tool vs. alternatives
- What you've built with it (with venture/client tags)
- Where it broke or surprised you

A blank `## My Take` on an entity you've actually used is a signal to fill it in — that's where the compounding happens across projects.

---

## Worked example: OpenAI Agents SDK

Walking the full flow:

1. **Entity** → `Atlas 🧠/Entities/Tools & Frameworks/OpenAI Agents SDK.md` (already exists per [[index]] — update it with new facts from the docs).
2. **Literature note** → `Atlas 🧠/1-Literature Notes/AI Engineering/OpenAI - Agents SDK Docs.md`, tagged `#type/source/article`. Organised by the SDK's own sections: Agents, Tools, Handoffs, Guardrails, Tracing.
3. **Snippets** → likely 2–4 files in `Atlas 🧠/💻 Product & Engineering/AI Engineering/`, each tagged `#type/snippet`:
   - `OpenAI Agents SDK - Tool Definition Pattern.md`
   - `OpenAI Agents SDK - Handoff Pattern.md`
   - `OpenAI Agents SDK - Guardrails Setup.md`
4. **Concept pages** → check if existing concept pages on related topics (e.g. an `Agent Safety Patterns` page or an `Agent Loop Pattern` page) need updates. Spin out a new concept page **only** if the docs surface a universal pattern not yet captured.
5. **Cross-links** → entity ↔ lit note ↔ snippets ↔ relevant concept pages.
6. **`## My Take`** on the entity → "Used Agents SDK for X in [project]. Picked it over LangGraph because Y. Hit issue Z."

---

## See Also

- [[Example - Ingesting a PDF]] — for one-shot whitepapers and papers
- [[Example - Reading a Book]] — for full-length books
- [[Example - Watching a Video]] — for video tutorials and talks
- [[Example - Taking an Online Course]] — for multi-module courses
- [[System Reference - How This Vault Works]] — §3 (directory structure), §6 (note types), §9 (tag system — including the snippet convention)
