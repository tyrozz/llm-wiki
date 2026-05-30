---
title: "Example - Taking an Online Course"
date: 2026-05-17
tags:
  - type/guide
  - status/evergreen
source: ai
---

# Real-World Example: Taking an Online Course

A walkthrough of how to capture a structured online course (Udemy, Coursera, YouTube playlist, bootcamp) — using *AI Agents & AI Automation — The Practical Agentic AI Guide* (Udemy) as the example.

---

## The Goal

Online courses are structured (modules, lessons) but ephemeral — you finish the course, your video access stays, but the *learning* often evaporates. The vault captures:

- **A folder of module notes** — one per lesson or module, while you're studying
- **Concept pages** in `Atlas 🧠/💻 Product & Engineering/<domain>/` for transferable ideas (not course-specific implementations)
- **Cross-references** to other sources on the same topic — courses often overlap with books, papers, and your existing concept pages

---

## Phase 1: Identify the topic, create the course sub-folder

Topic = the *subject* of the course, not the course title.

| Course | Topic | Sub-folder location |
|---|---|---|
| Udemy: *AI Agents & AI Automation — Practical Agentic AI Guide* | AI Engineering / Agents | `1-Literature Notes/AI Engineering/Courses/Udemy - Practical Agentic AI Guide/` |
| Udemy: *ISTQB Certified Tester Foundation Level* | ISTQB CTFL | `1-Literature Notes/Certifications/ISTQB CTFL/Courses/` (single file: `Udemy - ISTQB CTFL Course.md`) |
| Coursera: *Andrew Ng - ML Specialisation* | Machine Learning | `1-Literature Notes/Machine Learning/Courses/Coursera - Andrew Ng ML Specialisation/` |

**Decision: folder vs single file?**

- **Sub-folder** if you'll take a separate note per module/lesson (most multi-hour courses)
- **Single file** if the course is short or you'll only write one consolidated summary (e.g. a 1-hour overview course)

**Naming convention:** `<Platform> - <Course Title>` (e.g. `Udemy - Practical Agentic AI Guide`). Avoid the course author's name in the folder unless it's a signature course (Karpathy, Andrew Ng).

---

## Phase 2: Module-level notes

For each module/lesson, create a note inside the course folder:

```
1-Literature Notes/AI Engineering/Courses/Udemy - Practical Agentic AI Guide/
├── Module 1 - Foundations of Agentic AI.md
├── Module 2 - Single-Agent Patterns.md
├── Module 3 - Multi-Agent Orchestration.md
├── Module 4 - Tool Use and Function Calling.md
├── ...
└── Course - Final Notes & My Take.md   ← consolidated takeaways
```

**Per-module frontmatter:**

```yaml
---
title: "Module N - <Lesson Title>"
date: 2026-05-17
tags:
  - type/source/course
  - status/wip
source: ai          # if LLM-drafted from your raw notes
resource: <Udemy/Coursera URL to the section>
course: "[[Udemy - <Course Title>]]"
---
```

The `course:` field gives Dataview a clean way to roll up all modules of one course.

---

## Phase 3: Write, ingest, or both

Three valid modes — pick by what's faster for you on a given module:

| Mode | What you do | What the LLM does | When to use |
|---|---|---|---|
| **You write** | Bullet-point notes during the lesson | Nothing | Short modules, simple content |
| **LLM ingests** | Drop raw transcript or your scrappy notes in `00-Inbox/` | Expands into a clean module note | Dense lessons where you want to focus on watching, not transcribing |
| **Collaborative** | You write the structure; LLM fills sections | Fleshes out sections you started | Modules with practical exercises you want to document carefully |

Trigger:

> *"ingest 00-Inbox/practical-agentic-module-3-rough-notes.md — create module note at 1-Literature Notes/AI Engineering/Courses/Udemy - Practical Agentic AI Guide/Module 3 - Multi-Agent Orchestration.md"*

---

## Phase 4: Spin out concept pages from cross-cutting themes

After ~3 modules, patterns emerge. The course will teach implementations of bigger ideas (e.g. "ReAct loops", "tool retry", "agent handoffs") that already have or deserve a concept page in `Atlas 🧠/💻 Product & Engineering/AI Engineering/`.

> *"the last 3 module notes for Practical Agentic AI Guide all touch on tool-call retry — does Agent Safety Patterns cover this? If not, expand it; if yes, add a Connections link from each module note."*

**Rule:** concept pages are source-agnostic. Module notes describe *how this course taught it*; concept pages describe *what you know about it* across all sources.

---

## Phase 5: `## My Take` per module + a final consolidated take

Each module note's `## My Take` answers: *did I actually try this? what worked?* Tag with venture/client when applicable.

When the course is done, write a `Course - Final Notes & My Take.md` file at the course folder root:

- **What it claimed vs. delivered** — courses often over-promise; rate by what was actually useful
- **Best modules** — for future re-reference
- **Skip the rest** — modules you wouldn't recommend to past-you
- **What you applied** — which projects benefited
- **Comparison to other sources** on the same topic — *"X book covers this deeper", "Y blog post is the better intro"*

This file is what makes the course **compound** beyond the moment.

---

## Phase 6: Tag completion + update MOC

Two final touches:

1. Change frontmatter status from `status/wip` to `status/evergreen` on module notes
2. Update the topic MOC: `Atlas 🧠/0-Map of Content/Topics/<topic>.md` should link the course folder under a "Courses" or "Literature Notes" section

If the course warrants it (high signal, often referenced), also add the course folder to `index.md` under the relevant Literature Notes domain section.

---

## Anti-patterns

- **Transcribing word-for-word** while watching — pause, summarise, write *what mattered*
- **A note per video** when videos are 4 minutes — batch related videos into one module note
- **Skipping `## My Take`** — without it, course notes become a Netflix recap nobody re-reads
- **Concept pages titled after the course module** — keep concept pages course-agnostic; rename if you slipped

---

## See Also

- [[Example - Studying for a Certification]] — cert tracks combine a syllabus + a Udemy course in the same topic folder
- [[Example - Watching a Video]] — for one-off video notes outside a course
- `System Reference - How This Vault Works.md` — §6 (Three Note Types), §17 (ingest with existing notes)
- `CLAUDE.md` Directory Rule #3 — lit note placement rules
