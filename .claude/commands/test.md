---
argument-hint: <slice-id>
description: Write tests for a slice from its acceptance criteria (BDD)
---

You are a Test Engineer writing comprehensive tests based on slice specifications.

## Input

Slice ID or Use Case ID: $ARGUMENTS

**Preferred**: Slice ID (e.g., UC-AUTH-001-S1)
**Legacy**: Use Case ID (e.g., UC-AUTH-001)

## Steps

### If testing a SLICE (Recommended):

1. **Find the Slice Document**: Look for `docs/*-slice-*.md` matching the slice ID

2. **Read Section 7 (Acceptance Criteria)**: Extract BDD scenarios:
   - Given/When/Then statements
   - Happy path scenarios
   - Alternative flow scenarios
   - Error case scenarios

3. **Read Section 9 (Test Strategy)**:
   - Unit tests (agent-level)
   - Integration tests (slice-level)
   - Which agents to mock/stub

4. **Write Tests Following BDD**:
   - Map each Given/When/Then to test code
   - Use project's test framework patterns
   - Follow agent testing guidelines (Section 4)

5. **Test Layers**:
   - **Unit**: Individual agent behavior
   - **Integration**: Agent collaboration, full slice behavior
   - **Contract**: Message format validation

6. **Build and Run**: Follow project test commands

7. **Update Slice Document**: Change status from "Planned" to "Testing" or "Done"

### If testing a USE CASE (Legacy):

1. **Check for Slices First**: Look for slice documents
2. **If slices exist**: Test them individually instead
3. **If no slices**: Read use case Section 12 for test cases (legacy approach)

## Agent Testing Guidelines

For multi-agent systems:

### Unit Tests (Agent Level)

```
Test: AuthenticationAgent.validatePassword()
  - Mock UserStore, return predefined user
  - Call validatePassword with correct password
  - Assert returns true

Test: AuthenticationAgent handles invalid credentials
  - Mock UserStore, return user with different hash
  - Call validatePassword with wrong password
  - Assert returns false
  - Assert no session created
```

### Integration Tests (Slice Level)

```
Test: Full login flow (Slice S1)
  - Given: User exists in database
  - When: POST /api/login with valid credentials
  - Then: Receives session token
    And: Token is valid JWT
    And: Audit log has LOGIN_SUCCESS event
```

### Contract Tests (Message Validation)

```
Test: LoginRequest message format
  - Assert has required fields: email, password
  - Assert email is valid format
  - Assert password is non-empty string

Test: LoginResponse message format
  - Assert has fields: success, sessionToken
  - Assert sessionToken is valid JWT structure
```

## BDD to Test Code Mapping

### Example from Slice:

```gherkin
Given a user exists with email "alice@example.com"
  And the user's password hash matches "secret123"
When the user submits valid credentials
Then a session token is generated
  And the token is valid for 30 minutes
```

### Becomes:

```javascript
test('successful login with valid credentials', async () => {
  // Given
  await createUser({ email: 'alice@example.com', password: 'secret123' });

  // When
  const response = await request(app)
    .post('/api/login')
    .send({ email: 'alice@example.com', password: 'secret123' });

  // Then
  expect(response.status).toBe(200);
  expect(response.body.sessionToken).toBeDefined();

  const decoded = jwt.decode(response.body.sessionToken);
  expect(decoded.exp - decoded.iat).toBe(1800); // 30 minutes
});
```

## Test Quality Checklist

- [ ] All scenarios from Section 7 (Acceptance Criteria) covered
- [ ] Unit tests for each agent's responsibilities
- [ ] Integration tests for full slice behavior
- [ ] Message/contract validation tests
- [ ] Error cases tested (failure scenarios)
- [ ] Mock/stub strategy follows Section 9
- [ ] Tests are independent and repeatable
- [ ] Tests use project's test framework patterns

## Reference

See `.claude/skills/slice-test-writer.md` for detailed patterns.
See `CLAUDE.md` for project-specific test commands.
