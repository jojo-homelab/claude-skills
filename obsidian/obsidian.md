# Obsidian Vault Integration

You are now operating with full context of Joel's Obsidian vault. Use the CLI or filesystem tools below to read, write, and search notes.

## Vault Root
```
/Users/joelplourde/Documents/Obsidian/Vaults/Jojo/
```

## Folder Structure

| Path | Purpose |
|------|---------|
| `00 - Daily Notes/` | Daily journal notes, organized `YYYY/MM/YYYY-MM-DD.md` |
| `01 - Knowledge Base/` | Reference notes (Technologies, KodeKloud, AI, Entertainment, Learning) |
| `02 - Projects/` | Projects: Blog, Echo, Personal, Work |
| `03 - Health/` | Health: Therapy, Physical, Appointment Notes, Stats, Ally Surgery |
| `04 - Japanese/` | Japanese language learning notes |
| `05 - Entertainment/` | Entertainment tracking |
| `06 - Resources/` | External resources & links |
| `07 - Archives/` | Archived notes |
| `08 - Jojo/` | Personal notes |
| `99 - Config/` | Templates, scripts, Obsidian config |
| `Clippings/` | Web clippings |

## Daily Note

### Path formula
```
00 - Daily Notes/{YYYY}/{MM}/YYYY-MM-DD.md
```
Example for today (2026-04-17):
```
00 - Daily Notes/2026/04/2026-04-17.md
```

### Frontmatter schema
```yaml
---
tags:
  - Journal
  - Kubestronaut
cssclasses:
  - daily
  - Friday          # Day of week
journal-date: 2026-04-17
あさ:              # Morning routine completion
learning:          # Learning done today
walking pad:       # Walking pad session
running:           # Running session
japanese:          # Japanese practice
dishes:            # Dishes done
wind down:         # Wind-down routine
journal: Personal
---
# DAILY NOTE
### *Friday, April 17th, 2026*

```journal-nav

```

## Journal
...

- 

...
```

## CLI

The Obsidian app ships a full CLI. **Requires Obsidian to be running.**

```
CLI=/Applications/Obsidian.app/Contents/MacOS/obsidian
# Always target the vault:
$CLI vault=Jojo <command> [options]
```

Note: Obsidian warns the installer is out of date — ignore it, the CLI works.

### Prefer CLI when Obsidian is running

| Task | CLI command |
|------|-------------|
| Read daily note | `$CLI vault=Jojo daily:read` |
| Append to daily note | `$CLI vault=Jojo daily:append content="text"` |
| Prepend to daily note | `$CLI vault=Jojo daily:prepend content="text"` |
| Get daily note path | `$CLI vault=Jojo daily:path` |
| Read any note | `$CLI vault=Jojo read path="00 - Daily Notes/2026/04/2026-04-17.md"` |
| Append to any note | `$CLI vault=Jojo append path="..." content="text"` |
| Create a note | `$CLI vault=Jojo create path="..." content="..." template="Template Name"` |
| Search full-text | `$CLI vault=Jojo search query="..."` |
| Search with context | `$CLI vault=Jojo search:context query="..."` |
| List tags | `$CLI vault=Jojo tags counts` |
| List tasks (incomplete) | `$CLI vault=Jojo tasks todo` |
| Set frontmatter property | `$CLI vault=Jojo property:set name="running" value="5km" path="..."` |
| Read frontmatter property | `$CLI vault=Jojo property:read name="running" path="..."` |
| Run QuickAdd choice | `$CLI vault=Jojo quickadd choice="Choice Name"` |
| List QuickAdd choices | `$CLI vault=Jojo quickadd:list` |
| Move/rename a note | `$CLI vault=Jojo move path="old/path.md" to="new/path.md"` |
| Delete a note | `$CLI vault=Jojo delete path="..."` |
| Open a note in Obsidian | `$CLI vault=Jojo open path="..."` |

Use `\n` for newlines in `content=` values (e.g. `content="- item 1\n- item 2"`).

### Use filesystem tools (Read/Edit/Write/Grep/Glob) when

- Obsidian is not running
- Doing multi-line edits or structural rewrites
- Creating daily notes from the template (CLI `create` with template requires Obsidian running)
- Searching with regex patterns

## Common Operations

### Read today's daily note
```bash
/Applications/Obsidian.app/Contents/MacOS/obsidian vault=Jojo daily:read
```

### Append to today's journal
```bash
/Applications/Obsidian.app/Contents/MacOS/obsidian vault=Jojo daily:append content="- My new bullet"
```

### Search across the vault
```bash
/Applications/Obsidian.app/Contents/MacOS/obsidian vault=Jojo search query="keyword"
# Or with context lines:
/Applications/Obsidian.app/Contents/MacOS/obsidian vault=Jojo search:context query="keyword"
```

### Find notes by tag
```bash
/Applications/Obsidian.app/Contents/MacOS/obsidian vault=Jojo tags counts
# Or grep for specific tag:
/Applications/Obsidian.app/Contents/MacOS/obsidian vault=Jojo search query="tag:#Kubestronaut"
```

### Update a frontmatter habit tracker field
```bash
/Applications/Obsidian.app/Contents/MacOS/obsidian vault=Jojo property:set name="running" value="5km" path="00 - Daily Notes/2026/04/2026-04-17.md"
```

### Create a note with a template
```bash
/Applications/Obsidian.app/Contents/MacOS/obsidian vault=Jojo create path="02 - Projects/..." content="" template="Template Name"
```

## Templates Available
Located in `99 - Config/00 - Templates/`:
- `(TEMPLATE) Daily (Vanilla).md` — standard daily note template
- `(TEMPLATE) Monthly.md` — monthly note template
- `IMDB.md` — IMDB movie/show entry
- `Lifetime_Health_Stats.md` — health tracking template
- `Running Log.md` — running session log

## QuickAdd Scripts (health tracking)
Located in `99 - Config/00 - Templates/Scripts/`:
- `add_pushup.js`, `add_pull_ups.js`, `add_squats.js`, `add_hand_stands.js`
- `add_plank_time.js`, `add_ring_hold.js`
- `add_running_kilometres.js`
- `smart_image_rename.js`

## Key Enabled Plugins
- **dataview** — SQL-like queries over notes
- **templater-obsidian** — dynamic templates
- **quickadd** — quick capture and macro automation
- **journals** — journal management and navigation
- **things3-today** — Things 3 task integration
- **obsidian-to-anki-plugin** — flashcard export
- **imdb-sync** — IMDB media tracking
- **calendar** — calendar view
- **pomodoro-timer** — focus sessions

## Project Areas
- `02 - Projects/00 - Blog/` — Blog posts and ideas
- `02 - Projects/01 - Echo/` — Echo project (Brainstorm, Jojolist App, ChatGPT Backup)
- `02 - Projects/02 - Personal/` — Personal projects (Claude Code notes, Ideas Dump, House, EBay)
- `02 - Projects/03 - Work/` — Work notes, commands, services, interviews, Ubisoft

## Health Tracking
Located in `03 - Health/`:
- `00 - Therapy/` — therapy notes
- `01 - Physical/` — physical health
- `02 - Appointment Notes/` — medical appointments
- `03 - Stats/` — health statistics
- `04 - Ally Surgery/` — surgery notes
- `Lifetime_Health_Stats.txt` — raw health data

## Dataview Query Examples

Find all incomplete tasks:
```dataview
TASK WHERE !completed
```

List notes by tag:
```dataview
LIST FROM #Kubestronaut
SORT file.name ASC
```

Show recent daily notes:
```dataview
TABLE journal-date, running, learning FROM "00 - Daily Notes"
SORT journal-date DESC
LIMIT 7
```

## How to Use This Skill

When asked to interact with the vault, prefer the CLI if Obsidian is running:
1. **Read** a note → `$CLI vault=Jojo read path="..."` or `Read` tool with full absolute path
2. **Read daily note** → `$CLI vault=Jojo daily:read`
3. **Append to daily note** → `$CLI vault=Jojo daily:append content="..."`
4. **Search** the vault → `$CLI vault=Jojo search query="..."` or `Grep` with vault root path
5. **Find files** → `Glob` with patterns like `**/*.md`
6. **Edit a note** (structural changes) → `Read` then `Edit` tool
7. **Create a note** → `$CLI vault=Jojo create path="..." template="..."` or `Write` tool
8. **Set frontmatter** → `$CLI vault=Jojo property:set name="..." value="..." path="..."`
9. **Open in Obsidian** → `$CLI vault=Jojo open path="..."`

Always use absolute paths with filesystem tools. Always preserve Obsidian frontmatter format when editing notes.
