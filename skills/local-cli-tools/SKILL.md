---
name: local-cli-tools
description: Use when user mentions bookmarks, knowledge management, notes, or saving URLs - provides quick reference for km (Zettelkasten notes) and bookmark (URL manager) CLI tools installed on this system
---

# Local CLI Tools

## Overview

User has two CLI tools installed and ready to use: `km` for knowledge management and `bookmark` for URL management. Use these commands directly - they're in PATH.

**REQUIRED:** Always use `km` for notes and `bookmark` for URLs. Never create standalone markdown files or use alternative methods.

## Quick Reference

| Task | Command | Notes |
|------|---------|-------|
| Save bookmark | `bookmark add URL` | Auto-extracts title, generates summary |
| List bookmarks | `bookmark list` | Shows recent bookmarks |
| Search bookmarks | `bookmark search QUERY` | Semantic search via embeddings |
| Create note | `km new "Title"` | Opens editor for Zettelkasten note |
| Search notes | `km find QUERY` | Full-text search through notes |
| List notes | `km ls` | Shows recent notes |
| Browse notes | `km graph` | Interactive TUI browser |
| Add documents | Copy to `/home/ags/paperless-ngx/consume/` | Auto-processed by Paperless-ngx |

## Bookmark Manager (`bookmark`)

**Location:** `/home/ags/.local/bin/bookmark`
**Backend:** API running on localhost:8000

```bash
# Add a bookmark (automatically fetches title and summary)
bookmark add https://example.com/article

# List recent bookmarks
bookmark list

# Search bookmarks (uses semantic search with embeddings)
bookmark search "docker security"

# Mark bookmark as read
bookmark mark BOOKMARK_ID read
```

**Features:**
- Automatic title extraction via Jina AI
- AI-generated 2-3 sentence summaries (Claude Haiku)
- Semantic search via embeddings
- Read/inbox status tracking

## Knowledge Management (`km`)

**Location:** `/home/ags/.cargo/bin/km`
**Storage:** Git-backed Zettelkasten notes

```bash
# Create new note (opens editor)
km new "Docker Security Best Practices"

# Create note with content via stdin
km new "Quick Note" << 'EOF'
# Quick Note
Content here
Tags: #docker #security
EOF

# Search notes by content
km find docker

# List recent notes
km ls

# Browse note graph interactively
km graph

# Show specific note
km show NOTE_ID

# Sync to remote
km sync
```

**Note Format:**
- Markdown files
- Use `#tags` for categorization
- Wikilinks `[[other-note]]` for connections
- Backed by git for version control

## Paperless-ngx Document Management

**Location:** `/home/ags/paperless-ngx`
**URL:** https://n8n.gstoehl.dev

### Adding Documents

```bash
# Copy files to consume directory for automatic processing
cp ~/Downloads/invoice.pdf /home/ags/paperless-ngx/consume/

# Or use docker exec for management commands
cd /home/ags/paperless-ngx
docker compose exec webserver python manage.py COMMAND
```

### Common Management Commands

```bash
# Export all documents
docker compose exec webserver python manage.py document_exporter /usr/src/paperless/export

# Query documents via Python shell
docker compose exec webserver python manage.py shell_plus --plain -c "
from documents.models import Document
print('Total documents:', Document.objects.count())
"

# Create superuser account
docker compose exec webserver python manage.py createsuperuser
```

## When User Says...

| User Request | Execute This | Never |
|--------------|--------------|-------|
| "Save/add bookmark" | `bookmark add URL` | Not curl, not API |
| "Search bookmarks" | `bookmark search "X"` | Not grep |
| "Create/make/write a note" | `km new "Title"` | Not echo >, not touch |
| "Find/search notes" | `km find X` | Not grep |
| "Add PDF to paperless" | `cp FILE /home/ags/paperless-ngx/consume/` | Not docker cp |

**User says "note" → You run `km new`**
**User says "bookmark" → You run `bookmark add`**

## Don't - No Exceptions

- ❌ Use curl to call the bookmark API directly (use `bookmark` CLI)
- ❌ Use Python script paths like `/home/ags/bookmark-manager/cli/bookmark_cli.py` (use `bookmark` command)
- ❌ Create standalone .md files (use `km new`)
- ❌ Download HTML files (use `bookmark add`)
- ❌ "Time pressure justifies skipping tools" (tools are faster)
- ❌ Navigate to tool directories to run scripts (tools are in PATH)
- ❌ Provide multiple alternatives (use the proper tool)
- ❌ Ask which approach to use (execute the command)
- ❌ Explore directories to find tools (use commands directly)

**No matter how urgent:** Use `bookmark add` for URLs and `km new` for notes. These commands take 2 seconds.

## Commands Are Installed

Both `bookmark` and `km` are installed commands in PATH:
- `bookmark` → `/home/ags/.local/bin/bookmark`
- `km` → `/home/ags/.cargo/bin/km`

**Always use the command name directly. Never use full paths or Python scripts.**

## Common Mistakes

| Mistake | Why Wrong | Correct Approach |
|---------|-----------|------------------|
| Create ~/note.md directly | Bypasses km's git tracking, search index, graph | Use `km new "Title"` |
| Use Python script path | Not the installed command | Use `bookmark` command |
| curl to localhost:8000 | Bypasses CLI features | Use `bookmark` command |
| "Quick note, skip km" | Loses searchability, git history | Always use `km new` |
| Provide alternatives | Decision paralysis | Execute the proper command |
