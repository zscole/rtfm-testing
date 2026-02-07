---
name: rtfm-testing
description: |
  Test documentation quality by spawning fresh agents with zero context.
  Validates that docs are complete, clear, and usable by newcomers.
  Use when testing READMEs, tutorials, setup guides, or API docs before publishing.
  Trigger with "rtfm test", "test docs", "validate documentation", "/rtfm".
allowed-tools: "Read,Glob,Grep,Bash(git:*),Task,AskUserQuestion"
version: 1.0.0
---

# RTFM Testing

Test documentation by spawning fresh agents that know nothing except what the docs provide.

## Overview

Documentation written by builders is almost always incomplete—they fill gaps unconsciously, assume context, and skip "obvious" steps. RTFM Testing fixes this by asking: **can a fresh agent complete the task using only the docs?**

## When to Use

- Before publishing docs, READMEs, tutorials, or setup guides
- When users report confusion but you can't see why
- After major refactors to validate docs still work
- As part of CI for documentation-heavy projects

## Workflow

### Step 1: Gather Test Parameters

Collect from the user:

1. **Task description** — What should someone accomplish after reading the docs?
2. **Documentation source** — File paths, URLs, or inline content
3. **Success criteria** — What defines a passing test?

### Step 2: Load Documentation

Read the target documentation files. For multiple files, glob for relevant patterns (e.g., `**/*.md`).

### Step 3: Spawn Fresh Tester Agent

Spawn an isolated agent with no prior context using the TESTER prompt from `{baseDir}/references/TESTER.md`.

Provide the agent with:
```
TASK: {task_description}

---

DOCUMENTATION:

{documentation_content}
```

The fresh agent will:
- Attempt the task literally, using only provided docs
- Report every gap with type, location, impact, and suggested fix
- Return SUCCESS, PARTIAL, or FAILURE

### Step 4: Analyze Results

Review the gap report. Each gap type indicates a specific doc problem:

| Type | Description |
|------|-------------|
| `MISSING_STEP` | A required action is not documented |
| `MISSING_PREREQ` | A prerequisite is not listed |
| `UNCLEAR` | Instructions are ambiguous |
| `INCORRECT` | Documentation is wrong or outdated |
| `MISSING_CONTEXT` | Assumes undocumented knowledge |
| `ORDERING` | Steps are in wrong sequence |

### Step 5: Fix and Repeat

Update documentation to address gaps, then spawn a new tester and repeat until clean.

## Metrics

- **Cold Start Score** — Number of spawn cycles until SUCCESS (lower = better)
- **Gap Count** — Total gaps per run
- **RTFM Certified** — Docs pass when fresh tester succeeds with zero blocking gaps

## Key Principles

1. **No hints** — Don't help the tester. Let it fail.
2. **Literal reading** — Tester must not infer or guess.
3. **Docs only** — No external knowledge, no "common sense."
4. **Failures are signal** — Every stumble is actionable feedback.

## Reference Files

- `{baseDir}/references/TESTER.md` — System prompt for the fresh agent
- `{baseDir}/references/GAPS.md` — Gap report format specification
