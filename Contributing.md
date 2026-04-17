# Contributing Guide

Welcome to the team! Read this fully before writing a single line of code.

---

## Tech Stack
- Frontend: React + TypeScript (Vite)
- Backend: Node.js + Express + TypeScript
- Database: Supabase (PostgreSQL) + Prisma ORM
- Auth: Supabase Auth

---

## Branch Naming
Always create a new branch from `main`. Never work directly on `main`.

| Type | Pattern | Example |
|---|---|---|
| New feature | `feature/short-description` | `feature/equipment-dispatch` |
| Bug fix | `fix/short-description` | `fix/calendar-overlap` |
| Refactor | `chore/short-description` | `chore/cleanup-routes` |
| Database change | `db/short-description` | `db/add-worker-table` |

---

## Commit Message Format
We follow Conventional Commits. Every commit must follow this pattern:


| Type | When to use |
|---|---|
| `feat` | Adding new functionality |
| `fix` | Fixing a bug |
| `chore` | Config, deps, cleanup |
| `db` | Prisma schema or migration changes |
| `docs` | README or documentation updates |

**Examples:**
- `feat: add equipment dispatch form`
- `fix: resolve worker salary calculation`
- `db: add freelancer table to schema`
- `chore: update express dependencies`

---

## Daily Workflow — Follow This Every Time

```bash
# 1. Start from fresh main
git checkout main
git pull origin main

# 2. Create your branch
git checkout -b feature/your-feature-name

# 3. Write code and commit in small chunks
git add .
git commit -m "feat: describe what you did"

# 4. Push your branch
git push origin feature/your-feature-name

# 5. Open a Pull Request on GitHub and request review from the lead
```

---

## Pull Request Rules
- Every PR must be linked to a GitHub Issue (`Closes #12`)
- Fill the PR template completely — no empty PRs
- Never merge your own PR — the lead reviews and merges
- Your branch must be up to date with `main` before requesting review
- One feature per PR — don't mix unrelated changes

---

## Code Rules
- All code must be in **TypeScript** — no plain `.js` files
- No `any` types — define proper interfaces
- All env variables go in `.env` — never hardcode secrets
- Copy `.env.example` to `.env` locally — never commit `.env`
- Run `npm run lint` before pushing — don't push code with lint errors

---

## Database Rules
- All schema changes go through **Prisma** — never edit the DB directly
- After changing `schema.prisma`, run:
  ```bash
  npx prisma migrate dev --name describe-your-change
  ```
- Commit both `schema.prisma` and the generated migration file
- Never delete or modify existing migration files

---

## Local Setup
1. Clone the repo: `git clone <repo-url>`
2. Install dependencies: `cd client && npm install` and `cd server && npm install`
3. Copy env files: `cp client/.env.example client/.env` and `cp server/.env.example server/.env`
4. Fill in your Supabase credentials in both `.env` files
5. Run migrations: `cd server && npx prisma migrate dev`
6. Start dev servers: frontend `npm run dev`, backend `npm run dev`

---

## Questions?
Reach out to the lead before making assumptions. A 2-minute chat saves hours of wrong code.

## The Folder Structure To Follow !!

av-manager/
│
├── client/                          # React + TypeScript (Vite)
│   └── src/
│       ├── assets/                  # Images, icons, fonts
│       ├── components/              # Reusable UI components
│       │   ├── ui/                  # Generic components (Button, Modal, Table)
│       │   ├── inventory/           # Inventory specific components
│       │   ├── events/              # Events specific components
│       │   └── workforce/           # Workforce specific components
│       ├── pages/                   # One folder per module
│       │   ├── inventory/
│       │   ├── events/
│       │   └── workforce/
│       ├── hooks/                   # Custom React hooks
│       ├── services/                # API call functions (axios)
│       ├── store/                   # Global state management
│       ├── types/                   # Shared TypeScript interfaces
│       └── utils/                   # Frontend helper functions
│
├── server/                          # Node.js + Express + TypeScript
│   ├── prisma/
│   │   └── schema.prisma            # Database schema (single source of truth)
│   └── src/
│       ├── index.ts                 # Entry point — mounts all route prefixes
│       ├── modules/                 # One folder per feature module
│       │   ├── inventory/
│       │   │   ├── inventory.routes.ts      # Route definitions only
│       │   │   ├── inventory.controller.ts  # Handles req/res only, no logic
│       │   │   ├── inventory.service.ts     # All business logic lives here
│       │   │   └── inventory.middleware.ts  # Joi/Zod validation schema
│       │   ├── events/
│       │   │   ├── events.routes.ts
│       │   │   ├── events.controller.ts
│       │   │   ├── events.service.ts
│       │   │   └── events.middleware.ts
│       │   └── workforce/
│       │       ├── workforce.routes.ts
│       │       ├── workforce.controller.ts
│       │       ├── workforce.service.ts
│       │       └── workforce.middleware.ts
│       ├── config/                  # Supabase client, env config, DB connection
│       └── utils/                   # Shared helpers (apiResponse.ts etc.)
│
├── .gitignore
├── README.md
└── CONTRIBUTING.md


## Folder Rules
- **Routes** — only route definitions, no logic
- **Controllers** — only handle req/res, call service, send response
- **Services** — all business logic and DB queries live here only
- **Middleware** — request validation (Joi/Zod) runs before controller
- **Config** — DB connection, Supabase client, environment setup
- **Utils** — shared helpers used across multiple modules

> When in doubt where something goes — it goes in the Service. 👆
