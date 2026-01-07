# Use Case UC-[ID] — [Name]

> **Use-Case 2.0 Template**
> Focus: Business value and promise, NOT implementation details
> Implementation happens through **Slices** (see slice-template.md)
> No need to add the 2.0 to the created file name 
---

## 1. Goal

[Business value delivered by this use case. What problem does it solve? What opportunity does it enable?]

**Example**: Enable users to authenticate securely, establishing trust and enabling personalized experiences.

---

## 2. Scope

**System/Subsystem**: [Which part of the system does this affect?]

**Boundaries**:
- **In Scope**: [What is included]
- **Out of Scope**: [What is explicitly excluded]

---

## 3. Actors

### 3.1 Primary Actor
- **Name**: [Actor name - e.g., End User, Administrator]
- **Goal**: [What they want to achieve]

### 3.2 Secondary Actors
| Actor | Role |
|-------|------|
| [Actor name] | [Their involvement in this use case] |

### 3.3 Agents (Multi-Agent Systems)
| Agent | Responsibility |
|-------|----------------|
| [Agent name] | [What this agent is responsible for] |

**Example**:
- AuthenticationAgent: Validates credentials
- SessionAgent: Manages user sessions
- AuditAgent: Records security events

---

## 4. Brief Description

[2-3 lines summarizing the behavior from a business perspective]

**Example**: User provides credentials, system validates them against stored records, and upon success, establishes an authenticated session with appropriate permissions.

---

## 5. Preconditions

- [Condition that must be true before this use case can execute]
- [Another precondition]

**Example**:
- User account exists in the system
- System is operationally available
- Network connectivity is established

---

## 6. Postconditions (Minimum Success Guarantee)

**On Success**:
- [Observable outcome 1]
- [Observable outcome 2]

**On Failure**:
- [System state after failure]
- [What is preserved/rolled back]

**Example Success**:
- User session is established
- Session token is issued
- Audit log records successful authentication

**Example Failure**:
- No session is created
- Failed attempt is logged
- User remains unauthenticated

---

## 7. Related Requirements

| Requirement ID | Description |
|----------------|-------------|
| FR-[ID] | [Functional requirement this UC satisfies] |
| NFR-[ID] | [Non-functional requirement this UC addresses] |

---

## 8. Planned Slices

> **CRITICAL**: Implementation happens through vertical slices
> Each slice delivers incremental value and can be implemented/tested independently

| Slice ID | Name | Business Value | Technical Risk | Status |
|----------|------|----------------|----------------|--------|
| [UC-ID]-S1 | [Slice name] | [Value delivered] | [High/Med/Low] | Planned |
| [UC-ID]-S2 | [Slice name] | [Value delivered] | [High/Med/Low] | Planned |
| [UC-ID]-S3 | [Slice name] | [Value delivered] | [High/Med/Low] | Planned |

**Example**:
| Slice ID | Name | Business Value | Technical Risk | Status |
|----------|------|----------------|----------------|--------|
| UC-AUTH-001-S1 | Basic password validation | Core authentication | Low | Done |
| UC-AUTH-001-S2 | Session management | Stateful interactions | Medium | In Progress |
| UC-AUTH-001-S3 | Multi-factor authentication | Enhanced security | High | Planned |

**Slice Selection Strategy**:
- Start with **high value**, **low risk** slices
- Tackle **high risk** slices early when they're unknown
- Defer **low value**, **low risk** slices

---

## 9. Business Rules

- [Rule 1: Business constraint or policy]
- [Rule 2: Validation rule]
- [Rule 3: Calculation or derivation logic]

**Example**:
- Password must be at least 12 characters
- Failed login attempts locked after 5 tries
- Session expires after 30 minutes of inactivity

---

## 10. Assumptions & Exclusions

**Assumptions**:
- [What we assume to be true]
- [Dependencies on external systems]

**Exclusions**:
- [What is explicitly NOT part of this use case]
- [Deferred to future iterations]

**Example Assumptions**:
- User database is available and synchronized
- Password hashing algorithm is bcrypt with cost 12

**Example Exclusions**:
- OAuth/SAML integration (separate use case)
- Biometric authentication (future enhancement)

---

## 11. Notes

[Additional context, constraints, or considerations]

---

## 12. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | [date] | [name] | Initial creation |

---

## 13. Related Documentation

[Here you may reference related documents needed to be loaded in context, 
since sometimes some conversations are saved in docs\*.md with resumes of specific information from 
a website/paper/debate with the ai, it can also reference related use cases/slices which context may 
be needed to complete the task properly]

---

## Next Steps

1. **Decompose into slices**: `/slice UC-[ID] S1`, `/slice UC-[ID] S2`
2. **Prioritize slices**: Order by risk and value
3. **Implement incrementally**: One slice at a time
4. **Optional**: Create technical realization diagrams with `/realization`

---

*Template based on Use-Case 2.0 (Ivar Jacobson, 2011)*
*Focus: Promise of value, not implementation prescription*
