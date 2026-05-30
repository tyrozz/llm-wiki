---
title: "Book Summaries"
date: 2026-05-24
tags:
  - type/concept
  - status/evergreen
source: ai
---

# Book Summaries

Auto-generated list of every literature note tagged `#type/source/book` (or any nested book subtype like `#type/source/book/aws`).

This is a Dataview query — requires the [Dataview plugin](https://github.com/blacksmithgu/obsidian-dataview) (pre-registered in `.obsidian/community-plugins.json`).

```dataview
LIST
FROM #type/source/book
SORT file.name ASC
```

---

## How this works

You don't hand-maintain this list. As soon as you ingest a book and the resulting literature note carries `#type/source/book` in its tags, it appears here.

To create a sub-category list (e.g. only AWS books):

```dataview
LIST
FROM #type/source/book/aws
SORT file.name ASC
```
