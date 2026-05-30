---
title: "Example - Studying for a Certification"
date: 2026-05-10
tags:
  - type/guide
  - status/evergreen
source: ai
---

# Real-World Example: Studying for the ISTQB CTFL Certification

A concrete walkthrough of how to use this vault system to prepare for a structured exam — using the ISTQB Foundation Level certification as the example.

---

## The Goal

Turn a dense certification syllabus into a living knowledge base that:
- Survives the exam (permanent concept pages, not throwaway revision notes)
- Compounds into your engineering work (tagged and linked to real projects)
- Uses the LLM to do the heavy lifting so you spend time understanding, not transcribing

---

## Phase 1: Ingest the syllabus chapter by chapter

The ISTQB syllabus PDF is your primary source. Work through it in chunks — one chapter or section per ingest:

> *"ingest Assets/raw/pdfs/ISTQB_CTFL_Syllabus_v4.0.1.pdf, pages 32–60"*

Each ingest creates or updates a literature note in:
`Atlas 🧠/1-Literature Notes/Certifications/ISTQB CTFL/`

After all chapters are done you have a complete structured summary of the syllabus — organized by the syllabus's own structure.

### Multi-source: supplementing the syllabus

For most certifications you'll have **more than one source** — the official syllabus plus a Udemy course, a book by a recognised author, sample exams, etc. Keep them all under the same topic folder, with subfolders by source type:

```
1-Literature Notes/Certifications/ISTQB CTFL/
├── Ch1-2 - Fundamentals & Testing Throughout SDLC.md  ← syllabus chapters at root
├── Ch3 - Static Testing.md
├── Ch4 - Test Analysis and Design.md
├── Ch5 - Managing the Test Activities.md
├── Ch6 - Test Tools.md
├── Courses/                                            ← supplementary courses
│   └── Udemy - ISTQB CTFL Course.md
└── Books/                                              ← supplementary books (if any)
    └── Rex Black - Foundations of Software Testing.md
```

This way concepts taught differently by different sources stay distinguishable — and the contrast between them lives in the notes themselves, not your head. See the lit-note placement rule in [[CLAUDE.md]] Directory Rule #3 for the general principle.

---

## Phase 2: Spin out concept pages for key terms

ISTQB exams test precise definitions. A dedicated concept page per term forces clarity and creates a personal glossary:

> *"create concept pages for: test levels, test types, equivalence partitioning, boundary value analysis, decision tables, state transition testing"*

These go in `Atlas 🧠/💻 Product & Engineering/Testing & QA/`.

Over time this folder becomes a permanent testing reference — useful long after the exam.

---

## Phase 3: Use your highlights as the ingest source (preferred)

Read the PDF in Zotero or Readwise Reader. Highlight what confuses you, what seems exam-critical, what contradicts your assumptions. Then ingest the annotation export:

> *"ingest Assets/zotero_annotations/ISTQB_CTFL_annotations.md"*

The resulting literature note reflects *your* focus areas, not a neutral summary of everything. This is more valuable than ingesting the raw PDF cold.

---

## Phase 4: Fill `## My Take` as you study

After each chapter, go to the relevant concept pages and write in `## My Take`:
- What surprised you
- What you'd apply at work
- Which principle you've already violated on a real project

Writing forces retrieval. A blank `## My Take` means you've read but not processed. Tag with the relevant project or client (e.g. `#project/myapp`, `#client/acme`) when you can connect it to real work.

---

## Phase 5: Use the LLM as a study partner

Ask questions directly against the vault:

> *"explain the difference between verification and validation"*
> *"what are the four test levels and when is each used?"*
> *"quiz me on equivalence partitioning"*

The LLM reads your concept pages and answers from *your* notes. Gaps in the answers reveal gaps in the vault — which reveal gaps in your understanding.

---

## Phase 6: Maintain the Exam Prep page

`Atlas 🧠/💻 Product & Engineering/Testing & QA/ISTQB CTFL Exam Prep.md` is your single revision checklist:
- All syllabus sections with K-levels (K1 = remember, K2 = understand, K3 = apply)
- Common exam traps and misconceptions
- Cross-links to every concept page

Update it as you work through chapters. Use it as your final review before the exam.

---

## The compounding benefit

Everything built for this exam stays in the vault permanently. When testing matters on a future project, the concept pages are already there — tagged, linked, and enriched with real experience in `## My Take`. Exam prep becomes a long-term engineering asset, not throwaway revision notes.

---

## Applies to any certification or structured course

This workflow works for any syllabus-driven learning:
- AWS / GCP / Azure certifications
- Scrum / PMP / PRINCE2
- Security certifications (CISSP, CEH)
- Any Udemy/Coursera course with a clear structure

The pattern is always: ingest by section → spin out concept pages → highlights over raw PDF → fill My Take → query to test understanding → maintain a master prep page.

---

## See Also

The three artefacts produced by this workflow (using ISTQB CTFL as the running example) would land at:

- `Atlas 🧠/💻 Product & Engineering/Testing & QA/ISTQB CTFL Exam Prep.md` — the master exam prep page
- `Atlas 🧠/1-Literature Notes/Certifications/ISTQB CTFL/Ch1-2 - Fundamentals & Testing Throughout SDLC.md` — first literature note
- `Atlas 🧠/💻 Product & Engineering/Testing & QA/The Seven Testing Principles (ISTQB).md` — first concept page spun from the lit note

Plus: `Atlas 🧠/_System/misc/System Reference - How This Vault Works.md` — Section 16 (PDF strategy), Section 17 (ingesting when you have notes).
