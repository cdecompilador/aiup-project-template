---
argument-hint: [module-filter]
description: Track project progress, identify gaps, suggest next actions
---

You are a Project Manager tracking requirements-driven development progress.

## Task

Generate a progress report for this project. If a module filter is provided ($ARGUMENTS), focus on that module only.

## Steps

1. **Scan Specifications**: Find all `specs/*.md` files and extract requirement IDs (REQ-*)

2. **Scan Use Cases List**: Read `docs/*-use-cases.md` and extract all use case IDs (UC-*)

3. **Check Use Case Documents**: For each UC-* in the list, check if `docs/*-uc-*.md` exists. If exists, read Section 12 and count test cases by status (Pending vs Implemented)

4. **Scan Test Files**: Read test files and count test cases

5. **Generate Report** in this format:
```
═══════════════════════════════════════════════════════════════
PROGRESS REPORT: <Module or "Full Project">
═══════════════════════════════════════════════════════════════

USE CASES COVERAGE
──────────────────────────────────────────────────────────────
| ID           | Name                  | Doc | Tests         | Status       |
|--------------|------------------|-----|---------------|--------------|
| UC-XXX-001   | Name Here             | Y/N | impl/total    | Complete/Pending |

TEST SUMMARY
──────────────────────────────────────────────────────────────
Total Test Cases:    XXX
Implemented:         XXX (XX%)
Pending:             XXX (XX%)

GAPS IDENTIFIED
──────────────────────────────────────────────────────────────
1. UC-XXX: N test cases pending
```

6. **Suggest Next Actions**:
```
SUGGESTED NEXT ACTIONS
══════════════════════════════════════════════════════════════

Priority 1 - Missing Tests:
  /test UC-XXX-001
  /test UC-XXX-002

Priority 2 - Missing Use Case Documents:
  /use-case UC-YYY-001

BULK COMMAND:
  /test UC-XXX-001 && /test UC-XXX-002
```

## Reference

See `.claude/skills/progress-tracker.md` for detailed workflow.
