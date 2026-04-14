# SKILL: Production Code Generation Standards

## Absolute Rules

### 1. Zero Stubs
Never write: `// TODO`, `// FIXME`, `throw new Error('not implemented')`,
`return null // implement this`. Every function is complete.

### 2. Environment Variables Only
No hardcoded URLs, ports, secrets, or environment-specific values.
Every configurable value comes from process.env (backend) or import.meta.env (frontend).

### 3. Consistent Error Handling
Backend: ALL async functions wrapped in asyncHandler or try-catch. Errors to next().
Frontend: ALL API calls in try-catch. Errors shown via toast. Loading states shown.

### 4. TypeScript Strict Mode
No `any` without explicit justification comment.
All function parameters and return types annotated.
Use unknown for external data, then narrow with type guards.

### 5. Semantic HTTP Codes
200 GET success | 201 POST created | 204 DELETE success
400 validation error | 401 no/invalid auth | 403 wrong permissions
404 not found | 409 conflict/duplicate | 422 unprocessable | 500 server error

### 6. Naming Conventions
Files: kebab-case (`auth.controller.ts`)
Variables/functions: camelCase (`getUserById`)
Types/Interfaces: PascalCase (`UserResponse`)
Constants: UPPER_SNAKE_CASE (`MAX_LOGIN_ATTEMPTS`)
DB tables: snake_case (Prisma handles via @@map)
React components: PascalCase files and functions

### 7. Import Order
1. Node built-ins
2. Third-party packages
3. Internal absolute imports
4. Relative imports
(blank line between each group)