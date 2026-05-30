---
title: "Example - Watching a Video"
date: 2026-05-17
tags:
  - type/guide
  - status/evergreen
source: ai
---

# Real-World Example: Watching a Video

A walkthrough for capturing one-off videos — YouTube talks, conference recordings, podcast episodes (audio with transcripts), tutorials. Distinct from a structured course (see [[Example - Taking an Online Course]]).

---

## When to actually write a video note

Videos are cheap to consume and expensive to process. Be selective:

- **Write a note** if the video introduces a new mental model, contradicts your existing thinking, or includes a concrete pattern you'll reuse
- **Don't bother** if it's a how-to you already understood, a recap of something you've read, or background noise

A vault full of 30 video notes you never re-open is worse than three notes you re-read every quarter.

---

## Phase 1: Place the note in the topic folder

Topic folder, then `Videos/` sub-folder:

| Video | Topic | Note location | Tag |
|---|---|---|---|
| YouTube: "What are AI agents?" | AI Engineering | `1-Literature Notes/AI Engineering/Videos/What are ai agents?.md` | `#type/source/video` |
| Conference talk: Hamel Husain — *Your AI App is a Black Box* | AI Engineering / Evals | `1-Literature Notes/AI Engineering/Videos/Hamel Husain - Your AI App is a Black Box (NeurIPS 2025).md` | `#type/source/video` |
| Podcast: Latent Space — Ep N on RAG eval | AI Engineering | `1-Literature Notes/AI Engineering/Podcasts/Latent Space - Ep N - RAG Eval.md` | `#type/source/podcast` |
| One-off video, no topic folder yet | (root) | `1-Literature Notes/<Speaker> - <Title> (Conf YYYY).md` | `#type/source/video` |

**Filename rule:** `<Speaker or Channel> - <Title> (Source/Conf/Year if useful).md`. Avoid the video's clickbait title — paraphrase to what it's actually about.

---

## Phase 2: Note template

Videos benefit from a tight structured template — they're easier to abandon mid-watch otherwise:

```markdown
---
title: "<Speaker> - <Title>"
date: 2026-05-17
tags:
  - type/source/video
  - status/evergreen
resource: https://www.youtube.com/watch?v=...
authors: <Speaker(s)>
duration: <e.g. 42 min>
topics: "[[<relevant topic MOC>]]"
---

# <Title>

**One-sentence summary:** <what's the core claim or insight?>

## Why I watched

<Was it recommended? Researching something specific? Random discovery?>

## Key Takeaways

- <3–7 bullets — the specific things worth remembering>

## Quotes / Timestamps

- `[02:14]` <verbatim quote or paraphrase>
- `[15:42]` <key example or counterargument>

## Connections

- [[<Concept page>]] — <how this video relates>
- [[<Other lit note>]] — <agreement/contradiction>

## My Take

> Did you actually try this? Did it change your approach? Tag with venture/client where applied.
```

Keep it short. A 40-minute video shouldn't produce a 600-line note.

---

## Phase 3: Ingest path (when LLM-drafted)

If you'd rather just dump notes and have the LLM structure them:

1. Watch the video, jot scrappy notes in `00-Inbox/<topic>-video-notes.md` (or a Readwise highlight export if you used the Reader for the transcript)
2. Trigger:

> *"ingest 00-Inbox/hamel-husain-eval-talk-notes.md — create video lit note at 1-Literature Notes/AI Engineering/Videos/Hamel Husain - Your AI App is a Black Box (NeurIPS 2025).md, tag with #type/source/video"*

The LLM expands your bullets into the template above. You only need to write `## My Take`.

---

## Phase 4: Spin out a concept page only when justified

Most videos don't justify a new concept page. Update an existing one with a `## Connections` link to the video instead.

Spin out when:

- The video introduces a **named pattern** you'll reference (e.g. *eval-driven development*, *evaluator-optimiser loop*) and no concept page exists yet
- The video contradicts an existing concept page (worth capturing the contrast)

---

## Phase 5: Dataview rollup (the Videos MOC payoff)

Because every video note is tagged `#type/source/video`, the [[Ai Videos]] Dataview MOC at `Atlas 🧠/0-Map of Content/Videos/` auto-includes the new note. No manual list maintenance.

If the topic warrants its own video sub-MOC (e.g. 10+ videos on AI Engineering), narrow the query with a more specific tag like `#type/source/video/ai-llms` — same pattern as the existing video Dataview list.

---

## Phase 6: Podcasts (same pattern, different tag)

Podcast episodes follow this exact workflow with three differences:

1. Tag with `#type/source/podcast`
2. Location: `<Topic>/Podcasts/<Show> - Ep N - <Episode Title>.md`
3. Include the **transcript URL** in `resource:` if available — much faster than re-listening

---

## Anti-patterns

- **Note per video for binge-watching** — if you watched 6 videos on the same topic in a row, write one consolidated note titled "Notes — <topic> video sweep (date)" with sections per video
- **Transcribing instead of summarising** — paraphrase to your own vocabulary so retrieval works later
- **Empty `## My Take`** — if you can't say *anything*, you didn't actually learn from it (or you're not done processing yet — that's also a signal)
- **Skipping the topic folder** — videos at `1-Literature Notes/` root sprawl over time; always put them in a `Videos/` sub-folder of a topic

---

## See Also

- [[Example - Taking an Online Course]] — for structured multi-video courses, not one-off videos
- [[Example - Ingesting a PDF]] — for talk slide decks (if they're more useful than the recording)
- [[Ai Videos]] — the Dataview MOC that auto-aggregates video notes
- `System Reference - How This Vault Works.md` — §6 (Three Note Types)
