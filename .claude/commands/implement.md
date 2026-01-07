---
argument-hint: <slice-id>
description: Implement a vertical slice (preferred) or use case
---

You are an Expert Programmer implementing vertical slices following project conventions with integrated Git workflow.

## Input

Slice ID or Use Case ID: $ARGUMENTS

**Preferred**: Slice ID (e.g., UC-AUTH-001-S1)
**Legacy**: Use Case ID (e.g., UC-AUTH-001) - will implement entire use case

## Philosophy

**Use-Case 2.0 Workflow**:
- ✅ **Implement slices**, not entire use cases
- ✅ Each slice is independently deployable and testable
- ✅ Each slice is developed in its own Git branch
- ❌ Avoid implementing entire use cases at once (high risk, delayed value)

## Git Workflow Integration

**BEFORE implementing**, set up the Git branch:

1. **Ensure on develop branch**:
   ```bash
   git checkout develop
   git pull origin develop
   ```

2. **Create slice branch**:
   ```bash
   git checkout -b slice/<Slice-ID>
   # Example: git checkout -b slice/UC-AUTH-001-S1
   ```

3. **Verify branch created**:
   ```bash
   git branch --show-current
   # Should show: slice/<Slice-ID>
   ```

## Steps

### If implementing a SLICE (Recommended):

0. **Set up Git branch** (see above)

1. **Read Slice Document**: Find `docs/*-slice-*.md` for the Slice ID
   - Section 1: Slice Objective (what value it delivers)
   - Section 3: Flow Description (step-by-step behavior)
   - Section 4: Agents & Responsibilities
   - Section 5: Messages / Contracts
   - Section 6: Business Rules
   - Section 10: Implementation Notes

2. **Optional: Read Realization**: If `docs/*-realization-*.md` exists, use it for:
   - Architecture diagrams
   - Technical decisions
   - Performance considerations

3. **Read Project CLAUDE.md**: Understand coding conventions

4. **Implement the Slice**:
   - Create/modify agent implementations
   - Implement message handlers
   - Add business rule validations
   - Handle error cases from Section 7 (Acceptance Criteria)

5. **Focus on Vertical Slice**:
   - Implement across all layers: API → Logic → Data
   - Make it deployable (even if behind feature flag)
   - Ensure it's independently testable

### If implementing a USE CASE (Legacy):

1. **Check for Slices First**: Look for planned slices in UC Section 8
2. **If slices exist**: Implement them one-by-one instead
3. **If no slices**: Read use case document and implement as a whole (not recommended for new work)

## Agent-Based Implementation

For multi-agent systems:

1. **Identify Agent Boundaries**:
   - Each agent has clear responsibility
   - Agents communicate via messages (not direct calls)

2. **Implement Message Contracts**:
   - Define message types from Section 5
   - Use typed messages (structs/classes/interfaces)

3. **Agent Implementation Pattern**:
   ```
   Agent {
     handleMessage(msg) {
       // Validate
       // Execute business logic
       // Send response/events
     }
   }
   ```

4. **Avoid Tight Coupling**:
   - Agents don't know about each other's internals
   - Communication only through messages

## Code Quality Checklist

- [ ] No compiler warnings or lint errors
- [ ] Follows project coding style (see CLAUDE.md)
- [ ] Memory management follows project patterns
- [ ] Error handling from Acceptance Criteria implemented
- [ ] All scenarios from Section 7 (BDD) covered
- [ ] Agent boundaries respected (message-based communication)
- [ ] Slice is independently deployable
- [ ] Business rules from Section 6 enforced

## Incremental Delivery

After implementing a slice:

1. **Commit changes** with meaningful messages:
   ```bash
   git add .
   git commit -m "feat(<Slice-ID>): <description>"
   # Example: git commit -m "feat(UC-AUTH-001-S1): implement basic password login"
   ```

2. **Run tests** (from `/test` command)

3. **Merge to develop** (after tests pass):
   ```bash
   git checkout develop
   git merge --no-ff slice/<Slice-ID> -m "Merge slice <Slice-ID>: <description>"
   git branch -d slice/<Slice-ID>
   git push origin develop
   ```

4. **Update slice status** to "Done" in the slice document

5. **Check for release** (run `/progress` to see if release is suggested)

## Git Commit Guidelines

Use conventional commits within slice branches:

| Type | Purpose | Example |
|------|---------|---------|
| `feat` | New feature | `feat(UC-AUTH-001-S1): add password validation` |
| `fix` | Bug fix | `fix(UC-AUTH-001-S1): handle empty password` |
| `test` | Tests | `test(UC-AUTH-001-S1): add login failure tests` |
| `refactor` | Refactoring | `refactor(UC-AUTH-001-S1): extract validation logic` |
| `docs` | Documentation | `docs(UC-AUTH-001-S1): update implementation notes` |

## Reference

See `.claude/skills/slice-implementer.md` for detailed workflow.
See `CLAUDE.md` for project-specific rules and Git workflow details.
