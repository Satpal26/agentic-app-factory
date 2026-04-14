# 🤖 Agentic Application Factory
### **Autonomous Multi-Agent System for Full-Stack Generation**

> **One Prompt. Zero Human Intervention. A Production-Ready App.**

---

## 🌟 Overview
The **Agentic Application Factory** is a sophisticated, specification-driven multi-agent orchestration system built to transform high-level natural language prompts into fully functional, deployable full-stack applications. 

Unlike standard "chat-and-code" prompts, this system utilizes a **10-Phase Pipeline** where specialized agents collaborate through a **Single Source of Truth (SSOT)** protocol.

---

## 🧠 The Architecture: "Spec-First" Logic
The core philosophy of this factory is **Strict Specification**. 
1. **The Orchestrator** parses the prompt into a `blueprint.json`.
2. **The Architect** converts that blueprint into a comprehensive `architecture.json`.
3. **The Workers** (Database, Backend, Frontend) build only what is defined in the architecture.

This ensures that the frontend and backend are perfectly synced, eliminating the "hallucination gap" common in simpler AI coding workflows.

---

## 👥 Meet the Agent Roster

| Agent | Responsibility | Primary Output |
| :--- | :--- | :--- |
| **👑 Orchestrator** | Master coordination & Phase 10 validation | `.generated/blueprint.json` |
| **📐 Architect** | Technical spec & API Contract design | `.generated/architecture.json` |
| **🗄️ Database** | Prisma schema & context-aware seeding | `backend/prisma/schema.prisma` |
| **⚙️ Backend** | Express.js, JWT Auth, & Zod Validation | `backend/src/**` |
| **🎨 Frontend** | React, shadcn/ui, & TanStack Query | `frontend/src/**` |
| **🔍 Reviewer** | Security audit & Logic verification | `.generated/review-report.json` |
| **🧪 Tester** | Vitest & Supertest suite generation | `tests/**` |
| **🐳 DevOps** | Dockerization & CI/CD Pipelines | `docker-compose.yml` |

---

## 🛠️ The 10-Phase Pipeline

1.  **PARSE:** Orchestrator extracts explicit and implicit requirements.
2.  **ARCHITECT:** Detailed system design including Prisma models and API endpoints.
3.  **DATABASE:** Prisma initialization and realistic seeding (15+ records per table).
4.  **BACKEND:** Generation of a robust, JWT-protected Express API.
5.  **FRONTEND:** Building a responsive UI using `shadcn/ui` and modern state management.
6.  **REVIEW:** An autonomous quality gate auditing code for security and consistency.
7.  **PATCH:** Re-spawning agents to fix CRITICAL/HIGH issues found during review.
8.  **TEST:** Generating a full test suite for the API and UI components.
9.  **DEVOPS:** Creating Docker configurations and professional documentation.
10. **ASSEMBLE:** Final verification and project health check.

---

## 🚀 Getting Started

### **Prerequisites**
* [Claude Code CLI](https://code.claude.com/) installed (`npm install -g @anthropic-ai/claude-code`)
* An Anthropic account with active API credits.

### **Execution**
1. Clone this repository.
2. Navigate to the root folder: `cd agentic-app-factory`.
3. Initialize Claude: `claude`.
4. Paste the **Initial Prompt** (e.g., the FlowBoard SaaS prompt).

# Example Prompt Initiation
> Build a full-stack SaaS project management application called "FlowBoard"...

🛡️ Built-in Quality Standards
Zero-Stub Policy: No // TODO comments. Every function is fully implemented.

Security-First: JWT Refresh Token rotation, httpOnly cookies, and password hashing (bcrypt).

Modern Stack: React 18, Vite, TypeScript, Prisma, PostgreSQL, Tailwind CSS, shadcn/ui.

Resilient Logic: Automatic retry mechanisms and post-mortem logging for pipeline failures.

[Prompt] ──► [Orchestrator] ──► [blueprint.json]
                                     │
                               [Architect] ──► [architecture.json]
                                                     │
               ┌─────────────────────────────────────┼──────────────────────────────────┐
               │                                     │                                  │
       [Database Agent]                      [Backend Agent]                    [Frontend Agent]
       (schema.prisma)                       (Express / JWT)                    (React / shadcn)
               │                                     │                                  │
               └─────────────────────────────────────┼──────────────────────────────────┘
                                                     ▼
                                             [Reviewer Agent] ◄── Audit & Patch Loop
                                                     │
                                             [DevOps & Tester] ──► [Final App]

Developed by Satpal Singh for the CBC Agentic Development Challenge.
