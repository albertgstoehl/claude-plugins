# GStoehL Tools - Claude Code Plugin

Local CLI tools integration for Claude Code, providing seamless access to personal knowledge management and bookmark systems.

## Features

### Skills Included

- **local-cli-tools** - Quick reference for `km`, `bookmark`, and Paperless-ngx CLI commands

### Tools Integrated

1. **km** - Knowledge Management (Zettelkasten)
   - Create and search markdown notes
   - Git-backed with automatic syncing
   - Graph-based note browsing
   - Full-text search

2. **bookmark** - URL Bookmark Manager
   - Semantic search via embeddings
   - Automatic title extraction and AI summaries
   - Archive.org snapshots
   - Read/inbox tracking

3. **Paperless-ngx** - Document Management
   - Automatic OCR and indexing
   - Django management commands
   - Consume directory for easy uploads

## Installation

### Via Marketplace

```bash
# Add the gstoehl marketplace
claude-code plugins add-marketplace https://raw.githubusercontent.com/USERNAME/gstoehl-marketplace/main/.claude-plugin/marketplace.json

# Install this plugin
claude-code plugins install gstoehl-marketplace:gstoehl-tools
```

### Manual Installation

```bash
# Clone to Claude's plugins directory
git clone https://git.fml128.ch/albert/claude-plugins.git ~/.claude/plugins/cache/gstoehl-tools
```

## Usage

Once installed, Claude will automatically have access to the local-cli-tools skill. Trigger it by mentioning:
- "Save this bookmark"
- "Create a note about..."
- "Search my bookmarks/notes"
- "Add this to paperless"

## Requirements

These tools must be installed on your system:
- `km` at `~/.cargo/bin/km`
- `bookmark` at `~/.local/bin/bookmark`
- Paperless-ngx running at `/home/ags/paperless-ngx`

## Development

```bash
# Clone repository
git clone https://git.fml128.ch/albert/claude-plugins.git
cd claude-plugins

# Make changes to skills
vim skills/local-cli-tools/SKILL.md

# Test locally
ln -s $(pwd) ~/.claude/plugins/cache/gstoehl-tools

# Commit and push
git add .
git commit -m "Update skill"
git push
```

## Structure

```
claude-plugins/
├── .claude-plugin/
│   └── plugin.json           # Plugin manifest
├── skills/
│   └── local-cli-tools/
│       └── SKILL.md          # Main skill documentation
├── README.md                 # This file
└── LICENSE                   # MIT License
```

## License

MIT
