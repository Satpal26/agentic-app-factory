# SKILL: RESTful API Design

## URL Rules
- Nouns not verbs: `/api/tasks` not `/api/getTasks`
- Plural: `/api/tasks` not `/api/task`
- Nested for ownership: `/api/projects/:id/tasks`
- Lowercase + hyphens: `/api/task-comments`

## Standard Response Envelope
Success:   { "success": true, "data": <payload>, "message"?: "string" }
Error:     { "success": false, "error": { "code": "SNAKE_CASE", "message": "Human readable" } }
Paginated: { "success": true, "data": [], "pagination": { "page": 1, "limit": 20, "total": 100, "pages": 5 } }

## Error Codes (use exactly these strings)
VALIDATION_ERROR | UNAUTHORIZED | FORBIDDEN | NOT_FOUND
CONFLICT | INTERNAL_ERROR | RATE_LIMITED

## Security
- Never return passwordHash in any response
- Scope all queries by userId (row-level security in controllers)
- Input validated with Zod before any DB operation
- All mutations require ownership verification