# obsidian skill

Gives Claude full context of your Obsidian vault — folder structure, daily note schema, CLI commands, and filesystem tools — so it can read, write, and search notes naturally.

## Installation

```bash
cp obsidian.md ~/.claude/skills/obsidian.md
```

## Usage

```
/obsidian <request>
```

### Examples

```
/obsidian read today's daily note
/obsidian append to my journal: "Finished the homelab refactor"
/obsidian search for notes about Kubernetes networking
/obsidian create a new project note for Echo under 02 - Projects
/obsidian mark running as 5km in today's frontmatter
```

## What it does

When invoked, the skill loads:

- **Vault root** and full folder structure
- **Daily note path formula** and frontmatter schema (habit tracker fields)
- **Obsidian CLI** commands for reading, appending, searching, and setting frontmatter properties
- **Fallback** to filesystem tools (Read/Edit/Write/Grep/Glob) when Obsidian isn't running or for structural edits

## Requirements

- Obsidian installed at `/Applications/Obsidian.app`
- Vault named `Jojo` at `/Users/joelplourde/Documents/Obsidian/Vaults/Jojo/`
- Obsidian must be running for CLI commands to work

> **Note:** Vault path and name are hardcoded for this homelab setup. Edit `obsidian.md` to point to your own vault if reusing.
