# claude-skills

Custom Claude Code skills for my homelab at home.

These skills live in `~/.claude/skills/` and are invoked via `/skill-name` in Claude Code.

## Installation

Copy the desired skill file to `~/.claude/skills/`:

```bash
cp obsidian/obsidian.md ~/.claude/skills/obsidian.md
cp tag-notes/tag-notes.md ~/.claude/skills/tag-notes.md
```

## Skills

| Skill | Invoke | Description |
|-------|--------|-------------|
| [obsidian](./obsidian/) | `/obsidian` | Read, write, and search an Obsidian vault using the CLI or filesystem tools |
| [tag-notes](./tag-notes/) | `/tag-notes [folder]` | Scan a folder of Markdown notes and apply relevant frontmatter tags |
| [catchup](./catchup/) | `/catchup [path]` | Get a concise project briefing from git history and key files to start sessions efficiently |
