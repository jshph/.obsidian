# Obsidian Vault Configuration Guide

This guide helps AI agents understand and replicate the essential configuration of this Obsidian vault.

## Core Philosophy

This is a Personal Knowledge Management (PKM) vault focused on:
- Daily note-taking and reflection
- Knowledge synthesis and connection
- Task management and productivity
- Reading and research integration

## Essential Plugins

These plugins are critical for the vault's core functionality and should be installed when replicating:

### 1. **templater-obsidian** (REQUIRED)
- Powers template system for daily notes and quick captures
- Configuration stored in: `plugins/templater-obsidian/data.json`
- Templates folder: `templates/`

### 2. **quickadd** (REQUIRED)
- Enables quick note creation workflows
- Particularly the "Personal Reflection" choice for timestamped notes
- Configuration: `plugins/quickadd/data.json`

### 3. **dataview** (REQUIRED)
- Provides database-like queries across notes
- Essential for MOCs and dynamic content aggregation
- Configuration: `plugins/dataview/data.json`

### 4. **obsidian-tasks-plugin** (RECOMMENDED)
- Task management with due dates and queries
- Integrates with daily notes workflow
- Configuration: `plugins/obsidian-tasks-plugin/data.json`

### 5. **calendar** (RECOMMENDED)
- Visual daily notes navigation
- Quick access to past/future daily notes
- Configuration: `plugins/calendar/data.json`

### 6. **readwise-official** (OPTIONAL - if user uses Readwise)
- Syncs highlights from books and articles
- Only needed if migrating Readwise integration
- Configuration: `plugins/readwise-official/data.json`

### 7. **obsidian-excalidraw-plugin** (OPTIONAL)
- Visual thinking and diagramming
- Install if user needs drawing capabilities
- Configuration: `plugins/obsidian-excalidraw-plugin/data.json`

## Plugins to SKIP

These plugins are installed but not essential for core functionality:

- **obsidian-bible-reference** - Domain-specific, skip unless needed
- **obsidian-canvas-conversation** - Experimental feature
- **obsidian-caterpillage** - Niche use case
- **reason** - Not essential for PKM workflow
- **obsidian-annotation-context-menu** - Minor enhancement
- **chat-stream** - Deprecated/experimental
- **obsidian-annotator** - Only if PDF annotation is critical
- **media-extended** - Only if heavy media usage
- **ghost-fade-focus** - Cosmetic enhancement
- **obsidian-focus-mode** - Cosmetic enhancement
- **obsidian-fullscreen-plugin** - Cosmetic enhancement

## Folder Structure

```
.obsidian/
├── inbox/              # Quick captures and new notes (timestamped)
├── daily/              # Daily notes
├── templates/          # Note templates
├── attachments/        # Images and files
├── MOCs/              # Maps of Content
├── projects/          # Active projects
└── archive/           # Archived content
```

## Key Configurations

### Core Settings (app.json)
```json
{
  "attachmentFolderPath": "attachments",
  "alwaysUpdateLinks": true,
  "showLineNumber": true,
  "defaultViewMode": "source",
  "promptDelete": false
}
```

### Daily Notes
- Folder: `daily/`
- Format: `YYYY-MM-DD`
- Template: `templates/daily-note.md`

### Quick Add Workflow
The `new-note.sh` script triggers QuickAdd to create timestamped notes in `inbox/`.

## Migration Instructions for AI Agents

### Step 1: Create Vault Structure
```bash
VAULT_PATH="[target_path]"
mkdir -p "$VAULT_PATH/.obsidian"
mkdir -p "$VAULT_PATH"/{inbox,daily,templates,attachments,MOCs,projects,archive}
```

### Step 2: Copy Core Configurations
```bash
# Copy essential config files
cp app.json "$VAULT_PATH/.obsidian/"
cp core-plugins.json "$VAULT_PATH/.obsidian/"
cp hotkeys.json "$VAULT_PATH/.obsidian/"
cp workspace.json "$VAULT_PATH/.obsidian/"
```

### Step 3: Install Essential Plugins
1. Copy plugin manifests and data:
```bash
# For each essential plugin
PLUGINS="templater-obsidian quickadd dataview obsidian-tasks-plugin calendar"
for plugin in $PLUGINS; do
  mkdir -p "$VAULT_PATH/.obsidian/plugins/$plugin"
  cp "plugins/$plugin/manifest.json" "$VAULT_PATH/.obsidian/plugins/$plugin/"
  cp "plugins/$plugin/data.json" "$VAULT_PATH/.obsidian/plugins/$plugin/" 2>/dev/null || true
done
```

2. Create community-plugins.json with essentials:
```bash
cat > "$VAULT_PATH/.obsidian/community-plugins.json" << 'EOF'
[
  "templater-obsidian",
  "quickadd",
  "dataview",
  "obsidian-tasks-plugin",
  "calendar"
]
EOF
```

### Step 4: User Instructions
After creating the vault structure:

1. Open the vault in Obsidian
2. Go to Settings → Community Plugins
3. Enable community plugins
4. Install the plugins listed in community-plugins.json
5. Restart Obsidian to apply configurations

## Hotkey Highlights

Key shortcuts configured in this vault:
- `Cmd+Shift+N`: QuickAdd - New note
- `Cmd+T`: Create new note from template
- `Cmd+P`: Command palette
- `Cmd+Shift+F`: Search in all files

## Custom Scripts

- `scripts/new-note.sh`: Creates timestamped note via QuickAdd automation

## Notes for Agents

- Focus on core PKM functionality, not cosmetic plugins
- Preserve folder structure and naming conventions
- Template system is critical - ensure templates folder exists
- Daily notes workflow is central to the vault's use
- Plugin data.json files contain user-specific settings that should be preserved when possible