---
name: vault-lint
description: When the user wants to health-check, audit, or lint the vault, find broken links, find orphan pages, check index coverage, or check for missing MOCs. Also use when the user says "lint the vault", "health check", "orphan pages", "broken links", "check the vault", or "what's missing from the index".
---

# Vault Lint

You are the maintainer of this LLM-Wiki Obsidian vault. Run the following checks in order and produce a prioritised report.

Today's date: !`date +%Y-%m-%d`

Run all commands from the vault root.

## Check 1 — Orphan pages

Find every `.md` file in `Atlas 🧠/` (excluding `_System/`) and check whether anything links to it.

```bash
# For each page, check if its basename appears as a wikilink anywhere
find "Atlas 🧠" -name "*.md" -not -path "*/_System/*" | while read f; do
  base=$(basename "$f" .md)
  count=$(grep -rl "\[\[$base" . --include="*.md" 2>/dev/null | grep -v "^./$f" | wc -l)
  if [ "$count" -eq 0 ]; then echo "ORPHAN: $f"; fi
done
```

For each orphan: suggest which `index.md` section or Topic MOC should link it.

## Check 2 — Broken wikilinks

Extract all `[[targets]]` from live `.md` files and verify each resolves to an existing file.

```bash
grep -roh "\[\[[^|\]#]*" . --include="*.md" | sed 's/.*\[\[//' | sort -u | while read target; do
  result=$(find . -name "${target}.md" 2>/dev/null | head -1)
  if [ -z "$result" ]; then echo "BROKEN: [[$target]]"; fi
done
```

Flag each broken link with the file(s) it appears in.

## Check 3 — index.md coverage

List all concept pages in `Atlas 🧠/` domain folders (excluding `_System/` and `1-Literature Notes/`) and confirm each appears in `index.md`.

```bash
find "Atlas 🧠" -name "*.md" \
  -not -path "*/_System/*" \
  -not -path "*/1-Literature Notes/*" \
  -not -path "*/0-Map of Content/*" \
  -not -path "*/Entities/*" | while read f; do
  base=$(basename "$f" .md)
  if ! grep -q "\[\[$base" index.md 2>/dev/null; then
    echo "MISSING FROM INDEX: $f"
  fi
done
```

## Check 4 — Stale index one-liners

For a sample of concept pages listed in `index.md`, read the page and compare its actual scope against the one-liner. Flag any where the page has grown significantly beyond what the one-liner describes.

Focus on pages that have been edited recently or have many H2 sections.

## Check 5 — Contradiction scan

For pairs of concept pages that cross-link to each other, check for conflicting definitions, metrics, or claims. Flag conflicts for the owner to resolve. Focus on explicitly cross-linked pages only.

## Check 6 — Missing MOCs

Count concept pages + lit notes per topic area. Flag any topic with ≥ ~4 pages that lacks a Topic MOC in `Atlas 🧠/0-Map of Content/Topics/`.

```bash
# List existing MOCs
ls "Atlas 🧠/0-Map of Content/Topics/"
```

## Output format

Produce a prioritised report:

```
## Vault Health Report — YYYY-MM-DD

### 🔴 Critical
- Broken wikilinks (readers hit dead ends)

### 🟡 Moderate  
- Orphan pages (exist but unreachable)
- Missing index entries

### 🟢 Low / Optional
- Stale one-liners
- Missing MOCs
- Contradiction candidates

### ✅ All clear
(list any checks that passed cleanly)
```

After the report, offer to fix each issue automatically.
