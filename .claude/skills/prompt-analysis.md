# SKILL: Deep Prompt Analysis

## Purpose
Transform natural language into a precise, complete blueprint.json.

## 6-Step Process

### Step 1: Surface Extraction
List every explicitly mentioned: feature, entity, user type, tech preference

### Step 2: Implicit Requirement Injection (ALWAYS apply)
| Trigger word/phrase         | Automatically add                                        |
|-----------------------------|----------------------------------------------------------|
| users / accounts / login    | Full auth: register, login, logout, refresh, /me, JWT    |
| teams / workspaces / orgs   | Multi-tenancy + RBAC (owner/admin/member roles)          |
| dashboard                   | Stats cards, Recharts charts, date-range filter          |
| real-time / live / instant  | Socket.io backend + React event context                  |
| upload / files / attachments| Multer + file type validation + storage config           |
| search                      | Full-text search param ?q=, debounced input (300ms)      |
| payments / billing          | Stripe scaffolding (checkout session, webhook)           |
| admin                       | /admin routes + isAdmin middleware + admin UI views      |
| Any entity list/view        | Pagination (?page&limit), sort (?sortBy&order), filter   |
| Any entity create/edit      | React Hook Form + Zod validation                         |
| notifications               | Notification model + mark-read endpoints + badge count   |
| export                      | CSV export endpoint + frontend download button           |

### Step 3: Tech Stack Decision
- SEO-heavy or marketing site → Next.js + NextAuth
- ML/data processing → Python FastAPI backend
- Unstructured/flexible data → MongoDB + Mongoose
- Default (everything else) → React+Vite + Express + PostgreSQL+Prisma

### Step 4: Entity Identification
Every noun the app "manages" is an entity.
Every entity gets: id, createdAt, updatedAt, full CRUD endpoints, list page, detail/edit modal.

### Step 5: API Endpoint Derivation
Standard for every entity:
GET /api/{entities}       list (paginated, searchable, sortable)
GET /api/{entities}/:id   single
POST /api/{entities}      create
PUT /api/{entities}/:id   update (owner only)
DELETE /api/{entities}/:id delete (soft preferred)
Plus: custom actions derived from features

### Step 6: UI Screen Derivation
Per entity: list page + create/edit modal or page
Per feature: dedicated page
Always: /login, /register, /dashboard, /settings/profile

## Output: Complete blueprint.json (zero placeholders)