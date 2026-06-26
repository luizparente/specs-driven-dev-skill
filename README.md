# Specs-Driven Development Skill

A skill that guides any compatible AI agent through specs-driven development (SDD): producing a complete, reviewed specification and multi-agent implementation plan before any code is written.

Compatible with **GitHub Copilot** and **Claude Code** (and any other agent that supports the [Agent Skills open standard](https://agentskills.io)).

## What it produces

All output is written into a `specs/` directory:

```
specs/
├── specs.md                  # problem statement, requirements, acceptance criteria, design
├── implementation-plan.md    # atomic task registry with wave-based parallel execution schedule
└── contracts/
    ├── interfaces.md         # web API contracts, service/repository interfaces, external integrations
    ├── events.md             # event contracts with embedded schemas
    └── domain.md             # domain model, aggregates, invariants
```

## Install

### Personal install

Copy this directory into the personal skills folder for your tool. The skill will be available across all projects.

| Tool | Location |
|---|---|
| GitHub Copilot | `~/.copilot/skills/specs-driven-dev-skill/` |
| Claude Code | `~/.claude/skills/specs-driven-dev-skill/` |

### Project install

To share the skill with a team via a repo, copy this directory into `.claude/skills/` or `.github/skills/` at the repo root and commit it:

```bash
# Works for both Claude Code and Copilot
cp -r specs-driven-dev-skill/ .claude/skills/specs-driven-dev/

# Copilot only
cp -r specs-driven-dev-skill/ .github/skills/specs-driven-dev/
```

> **Note:** `.claude/skills/` is picked up automatically by both Claude Code and Copilot, so it's the simpler single option if your team uses both tools.

## Use

The skill activates automatically when describing a feature to build. It can also be invoked manually:

```
# GitHub Copilot (VS Code chat)
/specs-driven-dev

# Claude Code
/specs-driven-dev
```

### What to expect

1. The agent runs a short intake interview to clarify the problem, success criteria, and scope before writing anything.
2. It produces `specs/specs.md` section by section, pausing to ask clarifying questions whenever anything is ambiguous.
3. Once the spec is reviewed and accepted, it produces `specs/implementation-plan.md`: a wave-based task breakdown optimised for parallel agent execution.
4. Each wave requires human review and approval before the next begins.

### Hard constraints (built into the skill)

- **Never runs git.** All source control is left to the developer.
- **Never assumes.** Every ambiguity triggers a clarifying question before proceeding.

---

## Verify

Check the skill loads correctly:

```
# GitHub Copilot — type /skills in the VS Code Copilot chat panel.
# specs-driven-dev should appear in the list.

# Claude Code
/skills
# specs-driven-dev should appear in the output.
```
