---
name: notion-sync
description: Pull context from Notion and/or push actions (tasks, projects, content pipeline cards) from the vault to Notion. Use when the user says "add to Notion", "create a Notion task", "add to content pipeline", "sync this to Notion", "create tasks from this", "brainstorm content", "plan [X] for [period]", or any planning prompt tied to a specific hat. Reads the relevant Notion database(s) first for context, then — after user approval — creates Notion records with obsidian:// backlinks. Does NOT push knowledge or concept pages — those stay in Obsidian.
---

## Procedure

Follow Workflow 7 in `CLAUDE.md` exactly. Summary:

### Pull phase (always run first)
1. Identify the hat the request belongs to.
2. Read the relevant Notion database(s) via MCP:
   - ✍️ Content → Content Pipeline
   - 🎨 Brand / 💻 Product → Tasks + Projects
   - 📈 Growth → Content Pipeline + Tasks
   - ⚙️ Ops → Tasks + Projects + Areas
3. Summarise what already exists: published, in draft, planned. Only then brainstorm.

### Push phase (after user approval)
1. Identify the vault page(s) involved. Construct the `obsidian://` deep link:
   `obsidian://open?vault=<your-vault-name>&file=<URL-encoded-relative-path>`
2. Project resolution:
   - Search Projects DB for a match.
   - Found → use it. Not found → propose creating it (ask for name, Area, status).
   - Ambiguous → present options, ask user to pick.
3. Create Notion records:
   - Task: title, Area link, Project link, Obsidian Link, Status = "To Do"
   - Content Pipeline card: title, type, hat/domain, Obsidian Link, Status = "Idea"
4. Return Notion record URLs.
5. Append to `log.md`.
