---
argument-hint: <Slice-ID>
description: Create technical realization diagram/details for a slice (optional)
---

You are a Technical Architect creating detailed realization documents for complex slices.

## Input

Slice ID: $ARGUMENTS (e.g., UC-AUTH-001-S1)

## When to Use

**Use realization for**:
- Complex slices with many agent interactions
- High-risk technical decisions that need documentation
- Team alignment on architecture
- Performance-critical paths
- Security-sensitive flows

**Skip realization for**:
- Simple CRUD slices
- Well-understood patterns
- Low-risk implementations

**Rule**: If the slice is self-explanatory from its spec, don't create a realization.

## Steps

1. **Find the Slice Document**:
   - Look for `docs/*-slice-*.md` matching the Slice ID
   - Read Section 4 (Agents), Section 5 (Messages)

2. **Read Realization Template**:
   - Use `docs/realization-template.md` as structure

3. **Determine File Name**:
   - Pattern: `<module>-realization-<slice-id>.md`
   - Example: `auth-realization-uc-001-s1.md`

4. **Create Realization Document**:

   **Section 1: Slice Reference**
   - Link back to the slice document
   - State why this realization is needed

   **Section 2: Architecture Overview**
   - ASCII or mermaid diagram showing agent network
   - Component and layer breakdown

   **Section 3: Message Sequence Diagram**
   - Visual flow of messages between agents
   - Use mermaid sequenceDiagram syntax

   **Section 4: Data Flow**
   - Show transformations through the system
   - Before/after persistent state changes

   **Section 5: Technical Decisions**
   - For each major decision:
     - Context (what problem?)
     - Options considered (pros/cons)
     - Decision made
     - Rationale (why?)
     - Consequences (trade-offs)

   **Section 6: Error Handling Strategy**
   - How each error is detected
   - What the system does
   - How to recover

   **Section 7: Performance Considerations**
   - Expected load
   - Bottlenecks and mitigations

   **Section 8: Security Considerations**
   - Threats specific to this slice
   - Mitigation strategies

   **Section 9: Testing Strategy (Detailed)**
   - Specific unit test cases
   - Integration test scenarios
   - Load testing approach

   **Section 10: Monitoring & Observability**
   - Metrics to track
   - Logs to emit
   - Alerts to configure

   **Section 11: Deployment Notes**
   - Configuration needed
   - Database migrations
   - Dependencies

5. **Link from Slice Document**:
   - Update the slice document Section 12 (Related Artifacts)
   - Add link to the realization document

6. **Suggest Next Steps**:
   ```
   Realization complete.

   Next steps:
     /implement [Slice-ID]     # Implement guided by this realization
     /test [Slice-ID]          # Write tests from realization test strategy
   ```

## Realization Quality Checklist

- [ ] **Diagrams are clear**: Agent network and sequence diagrams
- [ ] **Decisions are justified**: Each major choice has rationale
- [ ] **Trade-offs are explicit**: Consequences documented
- [ ] **Tests are specific**: Concrete test cases, not generic descriptions
- [ ] **Deployment is actionable**: Config, migrations, dependencies listed

## Example

```
User: /realization UC-AUTH-001-S1

Actions:
1. Read docs/auth-slice-uc-001-s1.md
2. Identify complexity: Multiple agents, crypto, session storage
3. Create docs/auth-realization-uc-001-s1.md with:
   - Agent network diagram
   - Sequence diagram for login flow
   - Decision: Redis vs Database for sessions (chose Redis)
   - Performance: Bcrypt async, Redis connection pool
   - Security: Timing attack mitigation, rate limiting
5. Update docs/auth-slice-uc-001-s1.md Section 12
   - Add link to realization document
```

## Tips

1. **Keep it visual**: Diagrams > walls of text
2. **Be specific**: "Use Redis with 5s TTL" not "fast storage"
3. **Document alternatives**: Show what you didn't choose and why
4. **Make it actionable**: Provide concrete config, code patterns
5. **Update as you learn**: Realization evolves during implementation

## Reference

See `.claude/skills/realization-writer.md` for detailed workflow.
