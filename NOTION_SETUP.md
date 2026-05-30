# Notion Integration Setup (Optional)

This vault can integrate with Notion via the official `@notionhq/notion-mcp-server` MCP
server. Once configured, Claude Code can **read** your Notion databases before brainstorming
(so it avoids duplicating existing content or work) and **push** new tasks, projects, and
content pipeline cards back to Notion after a planning session.

This integration is entirely optional — the vault works without it.

---

## Step 1 — Create a Notion integration

1. Go to [notion.so/my-integrations](https://www.notion.so/my-integrations)
2. Click **+ New integration**
3. Give it a name (e.g. "LLM-Wiki") and select your workspace
4. Click **Submit** → copy the **Internal Integration Token** (starts with `secret_` or `ntn_`)

---

## Step 2 — Share your databases with the integration

In Notion, open each database you want Claude Code to access and click
**Share → Invite** → select your integration. Recommended starting point:

- **Tasks** — actionable to-dos
- **Projects** — active initiatives
- **Areas** — ongoing responsibilities
- **Content Pipeline** — editorial calendar

The integration can only see databases you explicitly share with it.

---

## Step 3 — Copy your database IDs

Open each database in Notion. The database ID is the 32-character string in the URL:

```
https://www.notion.so/<workspace>/<DATABASE_ID>?v=...
```

---

## Step 4 — Add your token to `.mcp.json`

Open `.mcp.json` at the vault root and replace `<NOTION_TOKEN>` with your token:

```json
{
  "mcpServers": {
    "notion": {
      "command": "npx",
      "args": ["-y", "@notionhq/notion-mcp-server"],
      "env": {
        "OPENAPI_MCP_HEADERS": "{\"Authorization\": \"Bearer secret_YOUR_TOKEN_HERE\", \"Notion-Version\": \"2022-06-28\"}"
      }
    }
  }
}
```

> `.mcp.json` is gitignored — your token will never be committed.

---

## Step 5 — Add your database IDs to `CLAUDE.md`

Open `CLAUDE.md` and fill in the Notion database IDs in the External Integrations section.
Database IDs are not secrets — they're safe to commit.

---

## Verify it works

Restart Claude Code in the vault and run:

```
add a test task called "Notion MCP test" to Notion
```

Claude should create the task in your Tasks database with an `Obsidian Link` field pointing
back to the vault.

---

## Adapting to your own database structure

This vault is designed around a PARA-adjacent setup (Tasks, Projects, Areas, Content
Pipeline). If your Notion workspace uses different database names or structures, update
the database IDs and field names in `CLAUDE.md` accordingly. The Workflow 7 procedure
in `CLAUDE.md` is the authoritative spec for how Claude interacts with Notion — edit it
to match your setup.
