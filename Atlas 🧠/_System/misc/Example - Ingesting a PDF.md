---
title: "Example - Ingesting a PDF"
date: 2026-05-17
tags:
  - type/guide
  - status/evergreen
source: ai
---

# Real-World Example: Ingesting a Non-Book PDF

A walkthrough for PDFs that aren't books — whitepapers, research papers, slide decks, internal reports, conference handouts. Lighter-weight than a book ingest because the source is shorter and less structured.

---

## When this applies

Use this workflow for:

- **Academic papers** (arXiv, ACM, IEEE) — usually 6–20 pages
- **Whitepapers** (vendor architecture documents, e.g. Anthropic's "Building Effective Agents")
- **Slide decks** from conference talks
- **Internal reports** (your own or shared by collaborators)
- **Standards documents** (RFCs, OWASP guides, NIST publications)

For a full-length book, use [[Example - Reading a Book]] instead — books deserve multi-chapter structured lit notes; PDFs usually fit in one file.

---

## Phase 1: Decide where the PDF lives

Same rule as books: the file doesn't need to live in the vault.

| Where | When |
|---|---|
| Zotero (`~/Zotero/storage/...`) | Academic papers, anything with a citation chain you'll re-read |
| `Assets/raw/pdfs/` | Short reference PDFs (< 20 pages) you want co-located in the vault |
| Readwise Reader | Articles-as-PDF, anything you read in a phone/tablet flow |
| `Assets/raw/articles/` | Web articles you saved as PDF |

---

## Phase 2: Identify topic + place the lit note

Topic = what the PDF is *about*. One-file lit note unless the PDF is unusually structured (e.g. a multi-section standards doc).

| PDF | Topic | Lit note location | Tag |
|---|---|---|---|
| Anthropic "Building Effective Agents" | AI Engineering / Agents | `1-Literature Notes/AI Engineering/Anthropic - Building Effective Agents.md` | `#type/source/article` |
| arXiv ReAct paper (Yao et al. 2022) | AI Engineering / Agents | `1-Literature Notes/AI Engineering/Papers/Yao 2022 - ReAct.md` | `#type/source/paper` |
| OWASP LLM Top 10 (2025) PDF | AI Testing & Security | `1-Literature Notes/AI Engineering/OWASP - LLM Top 10 (2025).md` | `#type/source/paper` |
| One-off whitepaper, no series | (no folder) | `1-Literature Notes/<Author> - <Title>.md` (root) | `#type/source/article` |

**Filename rule:** `<Author or Org> - <Short Title>` (+ year if useful). Avoid generic names like `Paper.md`.

---

## Phase 3: Ingest

For PDFs in the vault:

> *"ingest Assets/raw/pdfs/anthropic-building-effective-agents.pdf"*

For external PDFs:

> *"ingest ~/Zotero/storage/ABC123/yao-react-2022.pdf, pages 3–8 are the core"*

If you've highlighted in Zotero, export annotations first and ingest those instead — same as the book workflow. Highlights > raw text.

---

## Phase 4: Spin out concept pages (only when warranted)

A single PDF rarely justifies a new concept page on its own. Spin one out when:

- The PDF introduces a **new transferable idea** not yet covered in the vault
- The PDF **contradicts** an existing concept page (concept page needs revision + the contradiction should be captured)
- The PDF crystallises a pattern you've seen across multiple sources

Otherwise: update existing concept pages with a `## Connections` link to the new lit note and move on.

> *"the Anthropic Building Effective Agents lit note has new patterns for tool-call retry — update Agent Safety Patterns and add a Connections link back"*

---

## Phase 5: Tag entities

Papers and whitepapers usually name specific tools, frameworks, companies, or people. Hyperlink them to entity pages in `Atlas 🧠/Entities/`:

- Tools/frameworks → `Entities/Tools & Frameworks/`
- Companies/products → `Entities/Companies & Products/`
- People (authors of foundational papers) → `Entities/People/`

If an entity doesn't have a page yet but is referenced repeatedly across the vault, create one. Otherwise just mention the name in plain text.

---

## Phase 6: Fill `## My Take`

For a one-shot PDF, `## My Take` is often 2–4 lines:

- One sentence on whether the central claim held up against your experience
- One on what you'd apply (or what you've already tried)
- A tag connecting it to a venture/client

If the PDF didn't change anything for you, leave `## My Take` blank — that's also a signal (worth noting why a hyped paper turned out to be vapour).

---

## Quick-fire variant: collected articles

If you've read 3–4 short PDFs/articles on the same narrow topic and none individually justifies its own lit note, batch them into a single note:

```
1-Literature Notes/AI Engineering/Notes - Tool-Call Retry Patterns (2026 sweep).md
```

Each source gets a short subsection. Reference them collectively from the relevant concept page.

---

## See Also

- [[Example - Reading a Book]] — for full-length books (multi-chapter structure)
- [[Example - Studying for a Certification]] — for syllabus-driven multi-source learning
- `System Reference - How This Vault Works.md` — §16 (PDF strategy)
