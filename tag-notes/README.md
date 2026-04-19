# tag-notes skill

Scans a folder of Markdown notes and applies relevant frontmatter tags based on file path and content. Replaces generic tags (like `KB`) with specific concept tags. Designed for Obsidian vaults but works on any folder of `.md` files.

## Installation

```bash
cp tag-notes.md ~/.claude/skills/tag-notes.md
```

## Usage

```
/tag-notes [folder]
```

- **No argument** — Claude will ask which folder to process
- **Relative path** — resolved against the vault root (`/Users/joelplourde/Documents/Obsidian/Vaults/Jojo/`)
- **Absolute path** — used as-is

### Examples

```
/tag-notes
/tag-notes 01 - Knowledge Base/02 - AI
/tag-notes 02 - Projects
/tag-notes /Users/joelplourde/Documents/Obsidian/Vaults/Jojo/03 - Health
```

## What it does

1. Finds all `.md` files in the target folder (recursively)
2. Reads each file's content
3. Determines 2–6 core concept tags from the folder path and content
4. Updates the `tags:` block in frontmatter — replacing generic tags, keeping good ones
5. Adds frontmatter if the file has none
6. Reports a summary of what changed

## Tag philosophy

- Core concepts only: `Kubernetes`, `Docker`, `Terraform`, `networking`, `security`, `DevOps`, etc.
- No one-off or overly specific tags
- 2–6 tags per file maximum
- Files that already have appropriate specific tags are skipped
