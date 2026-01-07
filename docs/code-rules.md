# Code Rules Template

This file defines coding conventions and rules for the project. Customize for your technology stack and team preferences.

## Naming Conventions

| Element | Convention | Example |
|---------|------------|---------|
| Files | [kebab-case / snake_case] | `user-service.ts`, `user_service.py` |
| Functions | [camelCase / snake_case] | `getUserById()`, `get_user_by_id()` |
| Classes | PascalCase | `UserService`, `HttpClient` |
| Constants | SCREAMING_SNAKE_CASE | `MAX_RETRIES`, `API_BASE_URL` |
| Variables | [camelCase / snake_case] | `userName`, `user_name` |
| Database Tables | snake_case | `user_accounts`, `order_items` |
| API Endpoints | kebab-case | `/api/v1/user-accounts` |

## Code Style

### Formatting
- Indentation: [2 spaces / 4 spaces / tabs]
- Max line length: [80 / 100 / 120] characters
- Trailing commas: [yes / no]
- Quote style: [single / double]

### Linting and Formatting Tools
- Linter: [ESLint / Pylint / Clippy / etc.]
- Formatter: [Prettier / Black / rustfmt / etc.]
- Config files: [.eslintrc.js, .prettierrc, pyproject.toml, etc.]

## Error Handling

### Pattern
```
[Add your error handling pattern here]

Example for TypeScript:
- Use custom error classes extending Error
- Always include error codes for machine parsing
- Log errors with context before throwing

Example for Go:
- Return errors explicitly, don't panic
- Wrap errors with context using fmt.Errorf
- Check errors immediately after function calls
```

### Logging
- Log levels: [DEBUG, INFO, WARN, ERROR]
- Include: [timestamp, request_id, user_id, etc.]
- Framework: [Winston, Logrus, slog, etc.]

## Testing

### Framework
- Unit tests: [Jest / pytest / go test / etc.]
- Integration tests: [Supertest / httpx / etc.]
- E2E tests: [Playwright / Cypress / etc.]

### Conventions
- Test file location: [alongside source / in tests/ directory]
- Test file naming: `*.test.ts`, `*_test.py`, `*_test.go`
- Coverage minimum: [80% / per-module requirements]

### Structure
```
[Add your test structure pattern here]

Example (Arrange-Act-Assert):
- Arrange: Set up test data and dependencies
- Act: Execute the function under test
- Assert: Verify the results
```

## Architecture Patterns

### Layering
```
[Define your architecture layers]

Example:
- Handlers/Controllers: HTTP interface, validation
- Services: Business logic
- Repositories: Data access
- Models/Entities: Domain objects
```

### Dependency Injection
- Approach: [Constructor injection / DI container / etc.]
- Interface naming: [IService / ServiceInterface / etc.]

## Security Rules

- [ ] Never log sensitive data (passwords, tokens, PII)
- [ ] Validate all external input
- [ ] Use parameterized queries (no SQL string concatenation)
- [ ] Store secrets in environment variables / secret manager
- [ ] Apply principle of least privilege

## Documentation

### Code Comments
- When: [Complex logic, business rules, non-obvious decisions]
- Style: [JSDoc / docstrings / godoc / etc.]

### API Documentation
- Tool: [OpenAPI/Swagger / GraphQL schema / etc.]
- Location: [/docs, inline, generated]

## Version Control

### Branch Naming
- Feature: `feature/<description>` or `slice/<UC-ID>`
- Bugfix: `fix/<description>`
- Hotfix: `hotfix/<description>`

### Commit Messages
```
<type>: <description>

Types: feat, fix, docs, test, refactor, chore
```

---

## Project-Specific Rules

[Add any rules unique to your project here]

---

*Customize this template by replacing bracketed placeholders with your actual conventions.*
