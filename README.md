# AIUP Project Template

A project template for AI-driven, requirements-focused software development using Claude Code. This template implements **Use-Case 2.0** methodology with vertical slicing for incremental delivery.

## What This Template Provides

- **Claude Code Integration**: Pre-configured slash commands (`/progress`, `/implement`, `/test`, `/slice`, etc.) that guide you through a formal requirements engineering process
- **Use-Case 2.0 Workflow**: Lightweight use cases focused on business value, decomposed into independently implementable vertical slices
- **Document Templates**: Ready-to-use templates for requirements specs, use cases, slices, and technical realizations
- **Branch-per-Slice Git Workflow**: Integrated Git workflow where each slice gets its own branch, merged to `develop`, with release suggestions

## Quick Start

1. **Copy this template** to your project directory
2. **Customize `CLAUDE.md`** with your project's build commands, tech stack, and coding conventions
3. **Run `/progress`** at the start of each session to see project status and suggested next actions

## Development Workflow

```bash
# Check project status
/progress

# Create requirements specification
/requirements auth-service

# Generate use cases list from spec
/use-cases specs/auth-spec.md

# Create a use case (lightweight, business value)
/use-case UC-AUTH-001

# Decompose into vertical slices
/slice UC-AUTH-001 S1
/slice UC-AUTH-001 S2

# Implement slice-by-slice (creates branch, implements, merges)
/implement UC-AUTH-001-S1
/test UC-AUTH-001-S1

# Check progress (will suggest releases when ready)
/progress
```

## Directory Structure

```
project/
├── .claude/
│   ├── commands/       # Slash commands (/progress, /implement, etc.)
│   └── skills/         # Detailed workflow implementations
├── docs/
│   ├── *-template.md   # Document templates
│   ├── *-use-cases.md  # Use cases lists
│   ├── *-uc-*.md       # Individual use case documents
│   └── *-slice-*.md    # Vertical slice documents
├── specs/              # Requirements specifications
├── CLAUDE.md           # Project instructions for Claude Code
└── README.md           # This file
```

## Available Commands

| Command | Description |
|---------|-------------|
| `/progress [module]` | Track progress, identify gaps, suggest next actions |
| `/requirements <module>` | Create requirements specification |
| `/use-cases <spec>` | Generate prioritized use cases list |
| `/use-case <UC-ID>` | Create Use-Case 2.0 document |
| `/slice <UC-ID> <S#>` | Create a vertical slice |
| `/implement <Slice-ID>` | Implement a slice with Git workflow |
| `/test <Slice-ID>` | Write tests from BDD acceptance criteria |
| `/realization <Slice-ID>` | (Optional) Technical deep-dive document |

## Key Concepts

### Vertical Slices
Instead of implementing entire use cases at once, work is broken into **vertical slices** that:
- Cut through all layers (UI/API → Logic → Data)
- Deliver observable business value independently
- Can be deployed and tested in isolation
- Enable incremental delivery and early risk reduction

### Use-Case 2.0
Based on Ivar Jacobson's Use-Case 2.0 (2011):
- Use cases are **promises of value**, not implementation specs
- Implementation happens through **slices**
- Focus on business outcomes, not technical details

### Branch-per-Slice Git Workflow
```
main              # Production releases only
  └─ develop      # Integration branch
       └─ slice/UC-AUTH-001-S1    # Feature branch per slice
```

## Customization

Edit `CLAUDE.md` to add:
- Build and test commands for your tech stack
- Project-specific coding conventions
- Architecture patterns and constraints
- Technology stack details

See `docs/code-rules.md` for a template of coding conventions.

## License

[Add your license here]
