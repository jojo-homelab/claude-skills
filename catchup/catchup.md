# Catchup Skill

Get up to speed on a code project as fast as possible. Run a structured set of reads, then produce a concise briefing. Do not explore beyond what is listed — the goal is efficiency.

## Steps

Run all of the following in order:

### 1. Git history
```bash
git log --oneline -15
```

### 2. Current state
```bash
git status
git diff --stat HEAD
```

### 3. In-progress diff (if any uncommitted or staged changes)
```bash
git diff HEAD
```

### 4. CLAUDE.md (if present)
Read `CLAUDE.md` in the project root. Skip if absent.

### 5. README
Read `README.md` in the project root. Skip if absent.

### 6. Recent changed files
From the git log, identify the 3–5 most recently modified source files (ignore lock files, generated files, and assets). Read them.

---

## Output format

After completing the reads, produce a briefing in this exact structure — keep it tight:

---
**Project:** <name>
**Last worked on:** <date and commit message of most recent commit>

**Recent activity** (last 15 commits, grouped by theme):
- <theme>: <what changed>

**Current state:**
- <staged/unstaged changes or "clean">

**Key files reviewed:**
- `path/to/file` — <one line on what it does>

**Where things left off:**
<2–4 sentences on what was in progress, what was just completed, and what the likely next step is>

**Suggested next step:**
<one concrete action to continue the work>
---

Do not summarize file contents in full. Do not read more files than listed. After the briefing, ask the user what they want to work on.

## Usage

```
/catchup
/catchup path/to/project
```

If a path is provided, `cd` to it first. Otherwise use the current working directory.
