# context-sync

Audit and fix project documentation role overlaps. One command to keep all your context files healthy.

## The Problem

As projects grow, documentation sprawls across multiple files with overlapping responsibilities:

- CLAUDE.md becomes a dumping ground for architecture details, design decisions, and conventions
- README has internal implementation details that belong elsewhere
- Design decisions live in comments, PR descriptions, or nowhere at all
- Numbers in docs (module count, test count, version) silently go stale

## The Solution

`context-sync` enforces a four-role model where every piece of project knowledge lives in exactly one place:

| Role | Purpose | Examples |
|------|---------|---------|
| **Context** | How to work here | CLAUDE.md, .cursorrules |
| **Architecture** | What code looks like now | docs/CODEMAPS/, docs/architecture/ |
| **Decisions** | Why it's this way | docs/adr/ |
| **External** | What this project is | README.md |

## What It Does

1. **Discover** — Scans for context files, classifies them, identifies missing roles
2. **Overlap Detection** — Finds content in the wrong role (architecture detail in CLAUDE.md, decisions in README)
3. **Create / Migrate** — Creates missing docs (ADR, architecture), moves content, replaces with pointers
4. **Freshness Check** — Verifies numbers match code reality, flags stale files
5. **Report** — Summary of all changes

Every action requires user confirmation. Nothing is auto-modified.

## Results

**Large project** (6700 LOC, 34 modules):
- CLAUDE.md: 165 lines → 117 lines (29% reduction)
- Created 8 ADRs from embedded design decisions
- Fixed 3 stale numeric claims

**Small project** (iOS app, 591 tests):
- Correctly identified project was already healthy
- Only action: created missing ADR index + fixed stale test count

## Installation

Copy `SKILL.md` to your Claude Code skills directory:

```bash
mkdir -p ~/.claude/skills/context-sync
cp SKILL.md ~/.claude/skills/context-sync/
```

Then invoke with `/context-sync` in Claude Code.

## Part of the AI Agent Knowledge Lifecycle

This skill complements the [ECC](https://github.com/affaan-m/everything-claude-code) ecosystem:

- **context-sync** — Documentation role audit (this skill)
- [context-budget](https://github.com/affaan-m/everything-claude-code) — Token consumption audit
- [verification-loop](https://github.com/affaan-m/everything-claude-code) — Code quality verification
- [architecture-decision-records](https://github.com/affaan-m/everything-claude-code) — ADR creation and lifecycle

## ECC Contribution

Submitted as [PR #827](https://github.com/affaan-m/everything-claude-code/pull/827) to Everything Claude Code.

## License

MIT
