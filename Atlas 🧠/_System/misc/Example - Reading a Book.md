---
title: "Example - Reading a Book"
date: 2026-05-17
tags:
  - type/guide
  - status/evergreen
source: ai
---

# Real-World Example: Reading a Technical Book

A concrete walkthrough of how to capture a full-length book into the vault — using *AI Engineering* by Chip Huyen (O'Reilly 2025) as the example.

---

## The Goal

A book is the densest source you'll ingest. Done well, it leaves behind:

- **A structured literature note** organised by the book's chapters
- **Several concept pages** in `Atlas 🧠/💻 Product & Engineering/<domain>/` capturing transferable ideas
- **`## My Take` sections** with what you tried, what you'd push back on, what you've actually applied

Done poorly, you finish the book, write nothing, and forget 80% within a month.

---

## Phase 1: Place the file, don't bloat the vault

The PDF/EPUB does **not** need to live inside the vault — the LLM can read it from any file path.

- **Preferred:** keep the book in Zotero (`~/Zotero/storage/<key>/`) and ingest your **annotation exports**, not the raw book. Highlights + margin notes = what *you* found important.
- **Alternative:** Readwise Reader if you want zero-friction auto-sync to Obsidian.
- **Last resort:** drop the PDF in `Assets/raw/pdfs/` only if it's small and you want it co-located. Large books bloat the vault and slow sync.

See System Reference §16 for the full PDF strategy.

---

## Phase 2: Identify the topic, place the lit note

The topic is the *subject* of the book — not the book title. Examples:

| Book | Topic | Lit note location |
|---|---|---|
| *AI Engineering* (Huyen) | AI Engineering | `1-Literature Notes/AI Engineering/Books/Chip Huyen - AI Engineering.md` |
| *Foundations of Software Testing* (Rex Black) | ISTQB CTFL | `1-Literature Notes/Certifications/ISTQB CTFL/Books/Rex Black - Foundations of Software Testing.md` |
| *Designing Data-Intensive Applications* (Kleppmann) | System Design | `1-Literature Notes/Books/Kleppmann - Designing Data-Intensive Applications.md` (no topic folder yet → root) |

If a topic folder doesn't exist and the book is a one-off, drop it at the root of `1-Literature Notes/`. Move it later if a series forms.

**Filename rule:** lead with the author so multi-source topic folders stay sortable: `<Author> - <Title>.md`. Tag with `#type/source/book`.

---

## Phase 3: Read first, ingest second (the preferred order)

The strongest workflow is:

1. **Read the book in Zotero/Readwise** — highlight, annotate, leave margin notes
2. **Export annotations** to `Assets/zotero_annotations/` or let Readwise sync automatically
3. **Then ingest:**

> *"ingest Assets/zotero_annotations/huyen_AI_ENGINEERING_2025.md — create literature note at 1-Literature Notes/AI Engineering/Books/Chip Huyen - AI Engineering.md"*

The resulting note reflects your highlights, not a neutral chapter-by-chapter recap. This is the difference between a useful lit note and a glorified summary.

### If you've already written your own notes

Move your notes into `## My Take` of the literature note **before** ingesting. The LLM never writes in `## My Take`, so your voice survives the ingest. See System Reference §17 for the safe protocol.

---

## Phase 4: Spin out concept pages

For each transferable idea the book covers — not each chapter — create or update a concept page in the relevant domain folder:

> *"from the Huyen AI Engineering lit note, spin out concept pages for: evaluation-driven development, cost-aware model selection, fine-tuning vs prompting tradeoffs"*

Concept pages live in `Atlas 🧠/💻 Product & Engineering/<domain>/`, not in `1-Literature Notes/`. The literature note stays tied to the book; the concept page is source-agnostic and will absorb future sources on the same idea.

---

## Phase 5: Fill `## My Take`

The lit note's `## My Take` answers: *what did this book change about how I work?* Examples:

- "Huyen's evaluation-driven framing replaced my old 'ship and watch logs' approach in [project] — added `eval/` to the repo before week 2. `#project/myapp`"
- "I disagreed with the cost-modelling chapter; her numbers assume single-region Bedrock pricing, which doesn't reflect the EU latency reality."

The concept pages' `## My Take` accumulates across sources — keep adding as new books touch the same topic.

---

## Phase 6: Cross-reference everything

A book is rarely the first source on a topic. Before finishing, check:

- Does the relevant Topic MOC link the lit note? (`Atlas 🧠/0-Map of Content/Topics/<topic>.md`)
- Did you tag entities mentioned in the book (tools, frameworks, people) with links to their pages in `Atlas 🧠/Entities/`?
- If the book is foundational, did you reference it from the concept page's `## Connections`?

---

## The compounding benefit

A second book on the same topic costs ~40% the effort of the first. Concept pages already exist; the new lit note adds context, sharpens contrasts, and pushes any `## My Take` further. Five books on AI Engineering = an opinionated personal reference that's actually yours.

---

## See Also

- [[Example - Studying for a Certification]] — multi-source pattern for cert tracks
- [[Example - Ingesting a PDF]] — for non-book PDFs (whitepapers, slides, reports)
- `System Reference - How This Vault Works.md` — §16 (PDF strategy), §17 (ingest with existing notes), §6 (Three Note Types)
