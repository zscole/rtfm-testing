# RTFM Testing

> "If an amnesiac can't follow your docs, your docs suck."

A methodology and agent skill for testing documentation quality by spawning fresh agents with zero context.

## What It Does

Spawns an isolated agent that attempts to complete a task using **only** your documentation. Every point of confusion becomes a specific, actionable gap report.

## Installation

### As an Agent Skill

```bash
# Clone to your skills directory
git clone https://github.com/zscole/rtfm-testing ~/.claude/skills/rtfm-testing
```

### Manual

Copy the directory to your agent's skills location.

## Usage

Trigger the skill with:
- `/rtfm`
- "test my docs"
- "validate documentation"
- "rtfm test this README"

## Gap Types

| Type | Description |
|------|-------------|
| `MISSING_STEP` | A required action is not documented |
| `MISSING_PREREQ` | A prerequisite is not listed |
| `UNCLEAR` | Instructions are ambiguous |
| `INCORRECT` | Documentation is wrong or outdated |
| `MISSING_CONTEXT` | Assumes undocumented knowledge |
| `ORDERING` | Steps are in wrong sequence |

## Files

```
rtfm-testing/
├── SKILL.md              # Core skill definition
├── README.md             # This file
└── references/
    ├── TESTER.md         # Fresh agent system prompt
    └── GAPS.md           # Gap report specification
```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Test your changes
4. Submit a pull request

## License

MIT
