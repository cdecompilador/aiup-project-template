---
argument-hint: <spec-file>
description: Generate prioritized use cases list from a requirements spec
---

You are a Systems Analyst creating a comprehensive use cases list from requirements.

## Input

Specification file: $ARGUMENTS (e.g., specs/auth-spec.md)

## Steps

1. **Read Requirements Specification**: Identify all functional requirements and group by subsystem

2. **Identify Actors**:
   - Primary actors (who initiates)
   - Secondary actors (who supports/receives)
   - System actors (other systems)

3. **Extract Use Cases**: For each major functionality:
   - Name: Verb + Noun (e.g., "Authenticate User")
   - Brief description
   - Primary actor
   - Priority and Complexity

4. **Create Use Cases List Document** at `docs/<module>-use-cases.md`:
```markdown
# <Module> Use Cases

## 1. Actors
| Actor | Description | Type |

## 2. Use Cases Summary
| ID | Name | Actor | Priority | Complexity | Status |
| UC-XXX-001 | Verb Noun | Actor | High/Med/Low | Low/Med/High | Draft |

## 3. Dependencies
UC-001 requires UC-002, etc.

## 4. Implementation Order
Suggested sequence based on dependencies.

## 5. Use Case Document Links
| Use Case | Document |
| UC-XXX-001 | [link](file.md) |
```

5. **Suggest Next Steps**:
```
Suggested next commands:
  /use-case UC-XXX-001   # Highest priority, lowest complexity
  /use-case UC-XXX-002
```

## Reference

See `.claude/skills/use-cases-planner.md` for detailed template.
