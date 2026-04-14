# REVIEW CYCLE PROTOCOL

## Severity Levels

| Level    | Definition                          | Action                        |
|----------|-------------------------------------|-------------------------------|
| CRITICAL | Security hole or broken app         | Must fix — pipeline blocked   |
| HIGH     | Feature incomplete or error-prone   | Fix in Phase 7                |
| MEDIUM   | Poor practice, missing handling     | Fix in Phase 7 if quick       |
| LOW      | Style, minor naming, console.log    | Log only                      |

---

## Backend Review Checklist

### Security
- [ ] No passwords stored in plaintext (bcrypt only)
- [ ] JWT secret loaded from process.env (not hardcoded)
- [ ] Auth middleware on EVERY protected route
- [ ] Zod validation BEFORE any controller logic
- [ ] No raw SQL with user input (Prisma prevents this, verify)
- [ ] CORS origin from environment variable, not wildcard in production

### Completeness
- [ ] Every endpoint in architecture.json has a route + controller function
- [ ] Every route file imported in routes/index.ts
- [ ] Every controller function is async with try-catch
- [ ] Global error handler registered last in app.ts
- [ ] All errors passed to next(error) — never res.send() for errors

### Correctness
- [ ] HTTP status codes semantically correct (201 create, 204 delete, etc.)
- [ ] Ownership check: users only access their own resources
- [ ] Paginated list endpoints accept ?page and ?limit
- [ ] JWT expiry matches .env.example documentation

---

## Frontend Review Checklist

### Security
- [ ] JWT stored in memory (Zustand) not localStorage
- [ ] 401 response triggers token refresh, then redirect to /login
- [ ] No API keys or secrets in frontend code

### Completeness
- [ ] Every page in architecture.json has a .tsx file
- [ ] Every page has: loading state + error state + empty state + content state
- [ ] Protected routes wrapped in ProtectedRoute component
- [ ] All forms use React Hook Form + Zod resolver
- [ ] All API calls handle errors with toast notification

### Integration
- [ ] Every frontend API call path matches backend route exactly
- [ ] TypeScript types match Prisma model field names and types
- [ ] VITE_API_URL used as base URL — never hardcoded localhost

---

## review-report.json Schema
```json
{
  "timestamp": "2024-01-01T00:00:00Z",
  "overallScore": 8.2,
  "totalIssues": 7,
  "critical": 0,
  "high": 2,
  "medium": 3,
  "low": 2,
  "issues": [
    {
      "id": "R001",
      "file": "app/backend/src/routes/tasks.ts",
      "line": 12,
      "severity": "HIGH",
      "description": "Auth middleware not applied to DELETE endpoint",
      "fix": "Add authMiddleware to router.delete('/:id', authMiddleware, controller.delete)",
      "resolved": false
    }
  ]
}
```