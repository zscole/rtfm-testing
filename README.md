# RTFM Testing

A documentation quality methodology that spawns fresh agents to validate whether docs are actually usable.

> "If an amnesiac can't follow your docs, your docs suck."

## The Problem

Documentation written by the person who built the thing is almost always incomplete. They fill in gaps unconsciously. They assume context. They skip "obvious" steps.

RTFM Testing fixes this by spawning a fresh agent with zero context and asking: can you complete this task using only the docs?

## How It Works

1. **Identify the task** — What should someone be able to do after reading the docs?
2. **Bundle the docs** — Collect all relevant documentation (and nothing else)
3. **Spawn a fresh tester** — Use the TESTER.md prompt with `sessions_spawn`
4. **Analyze failures** — Every confusion point is a doc bug
5. **Fix and repeat** — Update docs, respawn, retest until clean

## Quick Start

```
sessions_spawn(
  task: "Complete the following task using ONLY the provided documentation.\n\nTASK: [describe what user should accomplish]\n\n---\n\nDOCUMENTATION:\n\n[paste your docs here]"
)
```

The tester will:
- Attempt the task literally, using only provided docs
- Report every gap with type, location, impact, and suggested fix
- Return SUCCESS, PARTIAL, or FAILURE

## Gap Types

| Type | Description |
|------|-------------|
| `MISSING_STEP` | A required action is not documented |
| `MISSING_PREREQ` | A prerequisite is not listed |
| `UNCLEAR` | Instructions are ambiguous |
| `INCORRECT` | Documentation is wrong or outdated |
| `MISSING_CONTEXT` | Assumes undocumented knowledge |
| `ORDERING` | Steps are in wrong sequence |

## Metrics

- **Cold Start Score** — Number of spawn cycles until SUCCESS (lower = better)
- **Gap Count** — Total gaps per run
- **RTFM Certified** — Docs pass when fresh tester succeeds with zero blocking gaps

## Files

- `SKILL.md` — Detailed methodology guide
- `TESTER.md` — System prompt for fresh agent spawn
- `GAPS.md` — Gap report format specification

## Installation

### ClawHub (recommended)

Available on [ClawHub](https://clawhub.com/skills/rtfm-testing):

```bash
clawhub install rtfm-testing
```

### Manual

Copy `SKILL.md`, `TESTER.md`, and `GAPS.md` to your OpenClaw skills directory:

```bash
cp -r . ~/.openclaw/skills/rtfm-testing
```

## License

MIT
