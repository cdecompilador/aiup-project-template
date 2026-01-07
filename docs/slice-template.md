# Slice [Slice-ID] — Use Case UC-[UC-ID]

> **Slice Template - THE UNIT OF IMPLEMENTATION**
> A vertical slice delivers concrete, testable value
> Slices are independently implement able, deployable, and testable

---

## 1. Slice Objective

**What concrete value does this slice deliver?**

[Describe the specific, observable outcome this slice adds to the system]

**Example**: User can log in with email and password, receiving a session token that enables authenticated API calls.

---

## 2. Scenario Covered

> Which flows from the parent use case does this slice implement?

- [ ] **Happy Path**: [Primary success scenario]
- [ ] **Alternative Path**: [Specific alternative - e.g., "Remember me" option]
- [ ] **Error Case**: [Specific error - e.g., "Invalid credentials"]

**Scope of This Slice**:
- ✅ [What IS included in this slice]
- ❌ [What is NOT included - deferred to other slices]

**Example**:
- ✅ Basic email/password validation
- ✅ Session token generation
- ✅ Invalid credentials error handling
- ❌ Multi-factor authentication (Slice S3)
- ❌ OAuth integration (different use case)

---

## 3. Flow Description

**Step-by-step behavior** (specific to this slice):

1. [Actor action or trigger]
2. [Agent A performs responsibility]
3. [Agent B interacts or validates]
4. [Observable outcome or state change]
5. [...continue...]

**Example**:
1. User submits email and password via API
2. AuthenticationAgent retrieves user record from database
3. AuthenticationAgent validates password hash
4. SessionAgent generates JWT token
5. AuditAgent logs successful login
6. System returns token to user

---

## 4. Agents & Responsibilities

> **Multi-Agent Architecture**: Define clear boundaries and contracts

| Agent | Responsibility | Input | Output |
|-------|----------------|-------|--------|
| [Agent name] | [What it does] | [What it receives] | [What it produces] |

**Example**:
| Agent | Responsibility | Input | Output |
|-------|----------------|-------|--------|
| AuthenticationAgent | Validate credentials | LoginRequest(email, password) | AuthResult(success, userId?) |
| SessionAgent | Create session | CreateSessionCmd(userId) | SessionToken |
| AuditAgent | Record event | AuditEvent(type, userId, timestamp) | void |

---

## 5. Messages / Contracts

> Define the messages exchanged between agents

### 5.1 Input Messages

```
MessageName(payload)
  - field1: Type
  - field2: Type
```

**Example**:
```
LoginRequest(credentials)
  - email: String
  - password: String (plaintext - will be hashed)
  - rememberMe: Boolean (optional)
```

### 5.2 Output Messages

```
ResponseName(payload)
  - field1: Type
  - field2: Type
```

**Example**:
```
LoginResponse(result)
  - success: Boolean
  - sessionToken: String (JWT)
  - expiresAt: Timestamp

LoginError(error)
  - code: ErrorCode (INVALID_CREDENTIALS | ACCOUNT_LOCKED)
  - message: String
  - attempts Remaining: Integer?
```

### 5.3 Internal Messages (Agent-to-Agent)

```
InternalMessage(data)
  - ...
```

**Example**:
```
CreateSessionCommand(session)
  - userId: UUID
  - ttl: Duration (30 minutes default)

AuditEvent(log)
  - eventType: LOGIN_SUCCESS | LOGIN_FAILURE
  - userId: UUID?
  - ipAddress: String
  - timestamp: ISO8601
```

---

## 6. Business Rules

> Rules specific to this slice

- [Rule 1]
- [Rule 2]
- [Rule 3]

**Example**:
- Password must match bcrypt hash in database
- Session token expires after 30 minutes
- Failed attempts increment counter (locked at 5)
- Successful login resets failed attempt counter

---

## 7. Acceptance Criteria (BDD)

> Behavior-Driven Development style criteria

### Scenario 1: [Happy path scenario name]

```gherkin
Given [precondition]
  And [another precondition]
When [action]
Then [expected outcome]
  And [another expected outcome]
```

**Example**:

### Scenario 1: Successful login with valid credentials

```gherkin
Given a user exists with email "alice@example.com"
  And the user's password hash matches "secret123"
  And the account is not locked
When the user submits valid credentials
Then a session token is generated
  And the token is valid for 30 minutes
  And the login event is audited
  And the failed attempts counter is reset to 0
```

### Scenario 2: [Alternative flow scenario]

```gherkin
Given [setup]
When [action]
Then [outcome]
```

**Example**:

### Scenario 2: Login failure with invalid password

```gherkin
Given a user exists with email "alice@example.com"
  And the provided password is incorrect
When the user submits credentials
Then no session token is generated
  And an error "Invalid credentials" is returned
  And the failed attempts counter increments to 1
  And the failure event is audited
```

### Scenario 3: [Error case scenario]

```gherkin
Given [error condition]
When [action]
Then [error handling]
```

**Example**:

### Scenario 3: Account locked after multiple failures

```gherkin
Given a user has failed login 4 times
  And the account is not yet locked
When the user submits incorrect credentials again
Then no session token is generated
  And the account is locked
  And an error "Account locked" is returned
  And the account lock event is audited
```

---

## 8. Technical Risks

| Risk | Severity | Mitigation |
|------|----------|-----------|
| [Risk description] | High/Med/Low | [How to address] |

**Example**:
| Risk | Severity | Mitigation |
|------|----------|-----------|
| Bcrypt performance on high load | Medium | Use async hashing, consider caching recent validations |
| JWT secret rotation | High | Implement key rotation strategy before production |
| Session storage scalability | Low | Use Redis with TTL for session storage |

---

## 9. Test Strategy

### 9.1 Unit Tests
- [Agent A behavior tests]
- [Agent B behavior tests]
- [Business rules validation]

**Example**:
- AuthenticationAgent.validatePassword() with valid/invalid hashes
- SessionAgent.generateToken() creates valid JWT
- Business rule: Account locks after 5 failed attempts

### 9.2 Integration Tests
- [End-to-end slice behavior]
- [Agent collaboration]

**Example**:
- Full login flow: API request → AuthAgent → SessionAgent → response
- Audit events are correctly recorded

### 9.3 Agent Mocks/Stubs
- [Which agents to mock in tests]
- [Test doubles strategy]

**Example**:
- Mock AuditAgent for AuthenticationAgent unit tests
- Mock database for isolated SessionAgent tests
- Use real agents for integration tests

---

## 10. Implementation Notes

### 10.1 Key Functions/Methods

| Function | Agent | Purpose |
|----------|-------|---------|
| [functionName()] | [Agent] | [What it does] |

**Example**:
| Function | Agent | Purpose |
|----------|-------|---------|
| `validateCredentials()` | AuthenticationAgent | Compares password hash |
| `createSession()` | SessionAgent | Generates JWT with user claims |
| `logEvent()` | AuditAgent | Persists audit trail |

### 10.2 Data Structures

```
StructureName {
  field: Type
}
```

**Example**:
```
User {
  id: UUID
  email: String
  passwordHash: String
  failedAttempts: Integer
  isLocked: Boolean
  lastLoginAt: Timestamp?
}

Session {
  token: String (JWT)
  userId: UUID
  createdAt: Timestamp
  expiresAt: Timestamp
}
```

### 10.3 Dependencies

- [External service dependencies]
- [Database tables required]
- [Third-party libraries]

**Example**:
- Database: users table with email, password_hash, failed_attempts, is_locked
- Library: bcrypt for password hashing
- Library: jsonwebtoken for JWT generation

---

## 11. Status

- [ ] **Planned** - Identified but not started
- [ ] **In Progress** - Currently being implemented
- [ ] **Testing** - Implementation complete, under test
- [ ] **Done** - Deployed and verified

**Current Status**: [Select one above]

**Blocked By**: [Dependencies or impediments]

**Next Steps**: [Immediate actions to progress]

---

## 12. Revision History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | [date] | [name] | Initial slice specification |

---

## Related Artifacts

- **Parent Use Case**: [Link to UC-[ID] document]
- **Technical Realization**: [Link to realization-[Slice-ID].md] (optional)
- **Implementation**: [Link to source code files]
- **Tests**: [Link to test files]
- **Other documentation**: [Here you may reference related documents needed to be loaded in context, 
since sometimes some conversations are saved in docs\*.md with resumes of specific information from 
a website/paper/debate with the ai, it can also reference related use cases/slices which context may 
be needed to complete the task properly]

---

*Slice Template - Implementation Unit for Use-Case 2.0*
*Vertical slice: Cross-cutting agents, logic, data, and observable behavior*
