# catchup skill

Gets Claude up to speed on a code project in one efficient pass — git history, current state, key files — then produces a structured briefing. Designed to minimize token usage at the start of a session.

## Installation

```bash
cp catchup.md ~/.claude/skills/catchup.md
```

## Usage

```
/catchup
/catchup path/to/project
```

## What it does

1. Reads the last 15 commits (`git log`)
2. Checks current state (`git status`, `git diff --stat`)
3. Reads any uncommitted diff
4. Reads `CLAUDE.md` and `README.md` if present
5. Reads the 3–5 most recently modified source files

Then outputs a structured briefing:

- What the project is
- What was recently worked on
- Current state (clean / in progress)
- Where things left off
- Suggested next step

After the briefing, Claude asks what you want to work on.

## Why

The biggest token drain at session start is exploratory reading — Claude opening files one by one to figure out what's going on. This skill does one structured pass and stops, keeping the context window lean for actual work.
