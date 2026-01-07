---
argument-hint: <UC-ID> <Slice-ID>
description: Create a vertical slice - the unit of implementation
---

You are a Systems Architect creating implementation-ready vertical slices.

## Input

- Use Case ID: First argument (e.g., UC-AUTH-001)
- Slice ID: Second argument (e.g., S1, S2, S3)
- Combined: UC-AUTH-001 S1 or UC-AUTH-001-S1

## Task

Create a **vertical slice** document - THE unit of implementation for Use-Case 2.0.

A slice is:
- ✅ **Vertical**: Cuts through all layers (UI/API → logic → data)
- ✅ **Independently valuable**: Delivers observable business value
- ✅ **Independently testable**: Can be tested in isolation
- ✅ **Increment ally deliverable**: Can be deployed separately
- ❌ **NOT a layer**: Not just "database layer" or "API layer"
- ❌ **NOT atomic**: Don't try to implement the whole use case at once

## Steps

1. **Read Parent Use Case**:
   - Find `docs/*-uc-*.md` for the UC-ID
   - Understand Section 8 (Planned Slices)
   - Identify which slice you're creating

2. **Read Slice Template**:
   - Use `docs/slice-template.md` as the structure

3. **Determine File Name**:
   - Pattern: `<module>-slice-<uc-id>-<slice-id>.md`
   - Example: `auth-slice-uc-001-s1.md` for UC-AUTH-001-S1

4. **Fill Out Slice Document**:

   **Section 1: Slice Objective**
   - What concrete, testable value does this slice add?
   - Must be specific, not "implement authentication"
   - Good: "User can log in with email/password and receive a session token"

   **Section 2: Scenario Covered**
   - Happy path / Alternative / Error case
   - What's IN this slice vs deferred to other slices

   **Section 3: Flow Description**
   - Step-by-step behavior specific to this slice
   - Use actors and agents

   **Section 4: Agents & Responsibilities**
   - In multi-agent systems: Which agents are involved?
   - What is each agent's responsibility?
   - Define clear boundaries

   **Section 5: Messages / Contracts**
   - Input messages
   - Output messages
   - Agent-to-agent internal messages
   - Use structured format (fields and types)

   **Section 6: Business Rules**
   - Rules specific to THIS slice

   **Section 7: Acceptance Criteria (BDD)**
   - Given/When/Then scenarios
   - Make them executable
   - Cover happy path, alternatives, errors

   **Section 8: Technical Risks**
   - What could go wrong?
   - How severe?
   - How to mitigate?

   **Section 9: Test Strategy**
   - Unit tests (agent level)
   - Integration tests (slice level)
   - Which agents to mock

   **Section 10: Implementation Notes**
   - Key functions/methods
   - Data structures
   - Dependencies (DB, libraries)

   **Section 11: Status**
   - Mark as "Planned"
   - Note any blockers

5. **Update Parent Use Case**:
   - Go to parent use case document Section 8
   - Update the slice status from "Planned" to "Documented"
   - Add link to the new slice document

6. **Suggest Next Steps**:
   ```
   Next steps:
     /implement UC-[ID]-S[N]         # Implement this slice
     /test UC-[ID]-S[N]              # Write tests for this slice
     /realization UC-[ID]-S[N]       # (Optional) Create technical deep-dive
   ```

## Slice Design Principles

### 1. Start with High Value, Low Risk

Prioritize slices that:
- Deliver core functionality first
- Have well-understood technology
- Can be built with existing skills

### 2. Address High Risk Early

For unknown/risky slices:
- Tackle them early when you can still pivot
- Consider a spike/proof-of-concept first

### 3. Keep Slices Independent

Each slice should:
- Be deployable without other slices
- Have its own tests
- Be reversible if needed

### 4. Avoid Layer Slicing

❌ **Bad** (horizontal layers):
- Slice 1: Database schema
- Slice 2: API endpoints
- Slice 3: UI components

✅ **Good** (vertical features):
- Slice 1: Basic login (DB + API + UI)
- Slice 2: Session management (DB + API + UI)
- Slice 3: MFA (DB + API + UI)

## Example

```
User: /slice UC-AUTH-001 S1

Actions:
1. Read docs/auth-uc-login.md Section 8
2. Create docs/auth-slice-uc-001-s1.md with:
   - Objective: User can log in with email/password
   - Scenario: Happy path + invalid credentials error
   - Agents: AuthAgent, SessionAgent, AuditAgent
   - BDD: Given valid credentials, When login, Then token returned
   - Status: Planned
3. Update docs/auth-uc-login.md Section 8:
   - Change UC-AUTH-001-S1 status to "Documented"
   - Add link to slice document
```

## Reference

See `.claude/skills/slice-writer.md` for detailed workflow.
