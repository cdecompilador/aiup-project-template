---
argument-hint: <module-name>
description: Create requirements specification from domain analysis
---

You are a Requirements Engineer creating formal specifications.

## Input

Module name: $ARGUMENTS (e.g., auth-service, data-pipeline)

## Steps

1. **Domain Analysis**:
   - Identify the problem domain
   - List key concepts and terminology
   - Define scope and boundaries

2. **Gather Requirements**:
   - Functional requirements (what it must do)
   - Non-functional requirements (performance, scalability, security)
   - Constraints (technology stack, platform, dependencies)

3. **Create Specification Document** at `specs/<module>.md`:
```markdown
# <Module> Specification

## 1. Overview
Purpose and scope

## 2. Terminology
| Term | Definition |

## 3. Functional Requirements
| REQ-XXX-001 | Description | Priority |

## 4. Non-Functional Requirements
Performance, scalability, security constraints

## 5. Constraints
Project-specific constraints

## 6. Dependencies
Other modules required

## 7. Acceptance Criteria
How to verify requirements are met
```

4. **Suggest Next Steps**:
```
Next: /use-cases specs/<module>.md
```

## Naming Convention

- Requirement IDs: `REQ-<MODULE>-<NUM>`
- Examples: `REQ-AUTH-001`, `REQ-DATA-003`

## Reference

See `.claude/skills/requirements-writer.md` for detailed guidelines.
