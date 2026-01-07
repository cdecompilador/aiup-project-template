# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Quick Start

```bash
# Always start with progress check
/progress

# Build the project (customize for your stack)
[your build command]

# Run tests (customize for your stack)
[your test command]
```

**ALWAYS run `/progress` at the start of each session** to see project status and suggested next actions.

## Build Commands

**IMPORTANT**: Customize this section for your project's technology stack.

```bash
# Build (examples - customize for your stack)
npm run build        # Node.js
cargo build          # Rust
./gradlew build      # Java
dotnet build         # .NET

# Run tests (examples - customize for your stack)
npm test             # Node.js
cargo test           # Rust
pytest               # Python
./gradlew test       # Java
```

## Project Overview

[Describe your project here - what it does, its purpose, and main components]

## Project Structure

```
project/
├── [customize for your project structure]
├── specs/              # Requirements specifications
├── docs/               # Use case documents and templates
├── .claude/            # Claude Code commands and skills
│   ├── commands/       # Slash commands
│   └── skills/         # Workflow implementations
└── [your source directories]
```

## Code Rules

[Customize this section for your project. See `docs/code-rules.md` for a template.]

**Include**:
- Naming conventions (files, functions, classes, constants)
- Code style and formatting rules
- Error handling patterns
- Testing requirements

## Technology Stack

[Customize this section]

- **Language**: [e.g., TypeScript, Python, Rust]
- **Runtime**: [e.g., Node.js 20+, Python 3.11+]
- **Framework**: [e.g., Express, FastAPI, Actix]
- **Database**: [e.g., PostgreSQL, MongoDB]
- **Testing**: [e.g., Jest, pytest, cargo test]
- **Build Tool**: [e.g., npm, poetry, cargo]

## Development Environment Setup

[Customize with your setup instructions]

```bash
# Example setup
npm install
cp .env.example .env
npm run migrate
npm run dev
```

---

## Use-Case 2.0 Development Workflow

This project uses **Use-Case 2.0** methodology with vertical slicing.

### Core Concepts

- **Use Case** = Promise of business value (lightweight, 2-3 pages)
- **Slice** = Unit of implementation (vertical, independently valuable)
- **Vertical Slices** cut through all layers (UI/API → Logic → Data)

### Development Pipeline

```
Requirements Spec → Use Cases List → Use Case → Slices → Implement → Tests
    specs/*.md    docs/*-use-cases.md  docs/*-uc-*.md  docs/*-slice-*.md
```

### Available Commands

| Command | Purpose |
|---------|---------|
| `/progress [filter]` | Track progress, identify gaps, suggest next actions |
| `/requirements <module>` | Create requirements specification |
| `/use-cases <spec>` | Generate prioritized use cases list |
| `/use-case <UC-ID>` | Create Use-Case 2.0 document |
| `/slice <UC-ID> <S#>` | Create a vertical slice - THE unit of implementation |
| `/implement <Slice-ID>` | Implement a slice with Git workflow |
| `/test <Slice-ID>` | Write tests from BDD acceptance criteria |
| `/realization <Slice-ID>` | (Optional) Technical deep-dive document |

### Typical Workflow

```bash
/requirements auth-service           # Create spec
/use-cases specs/auth-spec.md        # Generate use cases list
/use-case UC-AUTH-001                # Create use case
/slice UC-AUTH-001 S1                # Create vertical slice
/implement UC-AUTH-001-S1            # Implement (creates branch)
/test UC-AUTH-001-S1                 # Write tests
/progress                            # Check status, get release suggestions
```

### Naming Conventions

| Type | Pattern | Example |
|------|---------|---------|
| Use Case ID | `UC-<MODULE>-<NUM>` | `UC-AUTH-001` |
| Slice ID | `UC-<MODULE>-<NUM>-S<N>` | `UC-AUTH-001-S1` |
| Use Case Doc | `<module>-uc-<name>.md` | `auth-uc-login.md` |
| Slice Doc | `<module>-slice-<uc>-<s>.md` | `auth-slice-uc-001-s1.md` |
| Spec Doc | `<module>-spec.md` | `auth-spec.md` |

### Document Templates

| Template | Purpose | Location |
|----------|---------|----------|
| Requirements | IEEE 830-style spec | `docs/requirements-template.md` |
| Use Cases List | Prioritized UC list | `docs/use-cases-list-template.md` |
| Use-Case 2.0 | Lightweight UC document | `docs/use-case-2.0-template.md` |
| Slice | Implementation unit | `docs/slice-template.md` |
| Realization | Technical deep-dive | `docs/realization-template.md` |
| Code Rules | Coding conventions | `docs/code-rules.md` |

---

## Git Workflow

Branch-per-slice workflow integrated with `/implement` command.

### Branch Strategy

```
main              # Production releases only
  └─ develop      # Integration branch
       └─ slice/UC-AUTH-001-S1    # Feature branch per slice
```

### Slice Workflow

1. `/implement UC-AUTH-001-S1` creates branch `slice/UC-AUTH-001-S1` from `develop`
2. Implement and commit changes
3. Merge back to `develop` after tests pass
4. `/progress` suggests releases when conditions are met

### Commit Message Types

- `feat`: New feature (slice implementation)
- `fix`: Bug fix
- `test`: Adding or updating tests
- `docs`: Documentation changes
- `refactor`: Code refactoring without behavior change

### Release Triggers

`/progress` suggests a release when:
- A use case is fully completed (all slices merged)
- 3+ slices merged since last release
- All high-priority slices in a module are done

---

## Before Implementing Changes

1. Read the relevant **SPEC file** in `specs/` if it exists
2. Read the related files you'll modify
3. Ask if something is unclear - don't assume
4. Propose a plan before writing code
5. Follow project coding standards

---

*Customize all sections marked with [brackets] for your specific project.*
