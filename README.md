# Specs-Driven Development Skill

A skill that guides any compatible AI agent through specs-driven development (SDD): producing a complete, reviewed specification and multi-agent implementation plan before any code is written.

Compatible with **GitHub Copilot** and **Claude Code** (and any other agent that supports the [Agent Skills open standard](https://agentskills.io)).

## What it Does

All output is written into a `specs/` directory in your project:

```
specs/
├── specs.md                  # problem statement, requirements, acceptance criteria, design
├── implementation-plan.md    # atomic task registry with wave-based parallel execution schedule
└── contracts/
    ├── interfaces.md         # web API contracts, service/repository interfaces, external integrations
    ├── events.md             # event contracts with embedded schemas
    └── domain.md             # domain model, aggregates, invariants
```

## Setup

The skill files live in `specs-driven-dev-skill/`. To make them discoverable by GitHub Copilot and Claude Code, symlink that directory into each tool's expected location:

```bash
# GitHub Copilot
mkdir -p .github/skills
ln -s ../../specs-driven-dev-skill .github/skills/specs-driven-dev

# Claude Code
mkdir -p .claude/skills
ln -s ../../specs-driven-dev-skill .claude/skills/specs-driven-dev
```

> **One symlink covers both.** Skills placed in `.claude/skills/` are also picked up automatically by Copilot, so if you only use one symlink, use the Claude Code one.

Commit everything — the `specs-driven-dev-skill/` directory and the symlinks — so the skill is available to anyone who clones the repo.

---

## How to Use

The skill activates automatically when you describe a feature you want to build. No explicit invocation needed in most cases.

You can also invoke it manually:

```
# GitHub Copilot (VS Code chat)
/specs-driven-dev

# Claude Code
/specs-driven-dev
```

### What to expect

1. The agent runs a short intake interview (7 questions) to understand the problem, success criteria, and scope before writing anything.
2. It produces `specs/specs.md` section by section, pausing to ask yes/no questions whenever anything is ambiguous.
3. Once you've reviewed and accepted the spec, it produces `specs/implementation-plan.md`: a wave-based task breakdown optimised for parallel agent execution.
4. You review and approve each wave before the next one begins.

### Hard constraints (built into the skill)

- **Never runs git.** All source control is left to you.
- **Never assumes.** Every ambiguity triggers a clarifying question before the agent proceeds.

---

## Verify

Check the skill loaded correctly with the commands below.

```bash
# GitHub Copilot — type /skills in the VS Code Copilot chat panel.
# specs-driven-dev should appear in the list.

# Claude Code
/skills
# specs-driven-dev should appear in the output.
```
