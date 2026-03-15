# AGENTS.md - Agentic Coding Guidelines

This document provides agentic coding guidelines for Next.js projects using this configuration template.

---

## Tech Stack

| Category   | Technology               |
| ---------- | ------------------------ |
| Framework  | Next.js 14 (App Router)  |
| Language   | TypeScript (Strict mode) |
| Database   | Supabase (PostgreSQL)    |
| Validation | Zod                      |
| Styling    | Tailwind CSS             |
| UI Library | Shadcn/ui                |
| Testing    | Vitest                   |

---

## Project Structure

```
app/                  # Next.js App Router - routing only
├── api/              # API routes
components/           # Reusable UI components
├── ui/               # Shadcn/UI primitives
└── modules/          # Business components

lib/                  # Utilities and configurations
├── supabase/         # Database clients
├── utils.ts          # Helper functions
actions/              # Server Actions

types/                # Global TypeScript definitions
schemas/              # Zod validation schemas
```

---

## Available Commands

```bash
# Development
pnpm run dev           # Start development server
pnpm run build         # Build for production
pnpm run start         # Start production server

# Linting & Formatting
npx eslint .                    # Lint all files
npx eslint --fix .              # Fix auto-fixable issues
npx prettier --write .          # Format files

# TypeScript
npx tsc --noEmit               # Type check only

# Testing
npx vitest                     # Run tests
npx vitest --run               # Run tests once

# Database
npx supabase gen types typescript  # Generate TypeScript types
```

---

## Coding Standards

### Naming

- Components: `PascalCase` (`Button.tsx`)
- Functions: `camelCase` (`fetchPosts`)
- Files: `kebab-case` (`api-utils.ts`)
- Constants: `SCREAMING_SNAKE_CASE` (`MAX_RETRIES`)

### Import Order

1. React/Next.js built-ins
2. External libraries
3. Internal aliases (`@/`)
4. Relative imports

### TypeScript

- Use `interface` for object shapes
- Use `type` for unions and tuples
- NO `any` - use `unknown` if uncertain
- Avoid `!` - use optional chaining

---

## Supabase Guidelines

```typescript
// Client Components
import { createBrowserClient } from "@/lib/supabase/client";

// Server Components / Actions
import { createServerClient } from "@/lib/supabase/server";
```

- Always select specific columns (avoid `SELECT *`)
- Use RLS policies for security
- Never expose Service Role key on client

---

## Validation (Zod)

```typescript
import { z } from "zod";

const CreatePostSchema = z.object({ title: z.string().min(5).max(100), content: z.string().min(10) });
```

---

## Server Actions

- Prefer over API routes for form mutations
- Use `useActionState` for loading states
- Revalidate cache after mutations

---

## JSDoc Requirements

Add JSDoc to:

- Exported functions and hooks
- Complex utility functions
- Types and interfaces

Skip for:

- Obvious props (`className`, `children`)
- Simple interfaces
