---
argument-hint: <use-case-id>
description: Create Use-Case 2.0 document (lightweight, value-focused)
---

You are a Use Case Author creating Use-Case 2.0 documents following Ivar Jacobson's methodology.

## Important Philosophy Change

**Use-Case 2.0 is NOT implementation specification**.

- ✅ **Use Case** = Promise of business value
- ❌ **Use Case** ≠ Implementation blueprint

**Implementation happens through Slices** (created with `/slice`).

## Input

Use case ID: $ARGUMENTS (e.g., UC-AUTH-001)

## Steps

1. **Gather Context**:
   - Read `docs/*-use-cases.md` to find the UC by ID
   - Read related `specs/*.md` for requirements
   - Read `docs/use-case-2.0-template.md` for structure

2. **Determine File Name**: `<module>-uc-<short-name>.md`
   - Example: `auth-uc-login.md` for UC-AUTH-001

3. **Write Use-Case 2.0 Document** - LIGHTWEIGHT, BUSINESS-FOCUSED:

   **Section 1: Goal**
   - What business value does this deliver?
   - What problem does it solve?
   - Keep it to 2-3 sentences

   **Section 2: Scope**
   - System/subsystem affected
   - In scope / Out of scope explicitly

   **Section 3: Actors**
   - Primary actor and goal
   - Secondary actors
   - Agents (in multi-agent systems)

   **Section 4: Brief Description**
   - 2-3 lines summarizing behavior
   - Business perspective, not technical

   **Section 5: Preconditions**
   - What must be true before

   **Section 6: Postconditions**
   - Success: Observable outcomes
   - Failure: What is preserved

   **Section 7: Related Requirements**
   - Link to FR-* and NFR-* from specs

   **Section 8: Planned Slices** ⭐ CRITICAL
   - Identify 3-5 vertical slices
   - For each slice:
     - ID: UC-[ID]-S1, UC-[ID]-S2, etc.
     - Name: Descriptive, value-focused
     - Business Value: What it delivers
     - Technical Risk: High/Medium/Low
     - Status: Planned

   **Slice Prioritization**:
   - High Value + Low Risk = Do first
   - High Value + High Risk = Do early (when you can pivot)
   - Low Value + Low Risk = Do later or defer
   - Low Value + High Risk = Question if needed

   **Section 9: Business Rules**
   - Business constraints and policies
   - Keep them domain-focused

   **Section 10: Assumptions & Exclusions**
   - What we assume
   - What is explicitly excluded

4. **Update Use Cases List**: Add link to new document

5. **Suggest Next Steps**:
   ```
   Use case created. Next steps:

   Create slices:
     /slice UC-[ID] S1    # First vertical slice
     /slice UC-[ID] S2    # Second vertical slice
     ...

   Then implement slices:
     /implement UC-[ID]-S1
     /test UC-[ID]-S1
   ```

## Key Differences from Old RUP Template

| Old (RUP 1.0) | New (Use-Case 2.0) |
|---------------|-------------------|
| Detailed flows | High-level description |
| All test cases upfront | Tests in slices |
| Implementation notes | Deferred to slices |
| Monolithic | Decomposed into slices |
| 10-15 pages | 2-3 pages |

## Example Slices for UC-AUTH-001 (User Login)

```
| Slice ID | Name | Business Value | Technical Risk | Status |
|----------|------|----------------|----------------|--------|
| UC-AUTH-001-S1 | Basic password auth | Core login functionality | Low | Planned |
| UC-AUTH-001-S2 | Session management | Stateful interactions | Medium | Planned |
| UC-AUTH-001-S3 | Account lockout | Security against brute force | Low | Planned |
| UC-AUTH-001-S4 | Multi-factor auth | Enhanced security | High | Planned |
| UC-AUTH-001-S5 | "Remember me" | User convenience | Low | Deferred |
```

**Implementation order**: S1 → S4 → S2 → S3 → S5
(Core first, high risk early, convenience last)

## Reference

See `.claude/skills/use-case-2.0-writer.md` for detailed workflow.
