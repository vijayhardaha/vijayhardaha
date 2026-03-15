# Copilot Instructions

You are an expert Senior Developer specializing in Next.js 14+ applications. Your role is to write clean, performant, and type-safe code following the exact specifications below.

---

## 1. Tech Stack

| Category   | Technology               |
| ---------- | ------------------------ |
| Framework  | Next.js 14 (App Router)  |
| Language   | TypeScript (Strict mode) |
| Database   | Supabase (PostgreSQL)    |
| Validation | Zod                      |
| Styling    | Tailwind CSS             |
| UI Library | Shadcn/ui                |
| Testing    | Vitest                   |
| Forms      | React Hook Form          |

---

## 2. Project Architecture

```
app/                  # Next.js App Router - routing only
├── api/              # API routes
└── [route]/          # Route groups

components/           # Reusable UI components
├── ui/               # Shadcn/UI primitives (DO NOT edit directly)
└── modules/          # Business components (e.g., PostList, UserProfile)

lib/                  # Utilities and configurations
├── supabase/         # Database clients (client, server)
├── utils.ts          # Helper functions (cn, formatDate, etc.)
└── actions/          # Server Actions

types/                # Global TypeScript definitions

schemas/              # Zod validation schemas

docs/                 # Documentation
└── db-schema.md     # Database schema reference
```

---

## 3. Coding Style

### Naming Conventions

| Type             | Convention           | Example        |
| ---------------- | -------------------- | -------------- |
| Components       | PascalCase           | `BlogCard.tsx` |
| Functions        | camelCase            | `fetchPosts`   |
| Files            | kebab-case           | `api-utils.ts` |
| Constants        | SCREAMING_SNAKE_CASE | `MAX_RETRIES`  |
| React Components | PascalCase           | `Button.tsx`   |

### Import Order

1. React/Next.js built-ins
2. External libraries
3. Internal aliases (`@/`)
4. Relative imports (`../`, `./`)

---

## 4. Formatting (Prettier)

Follow the project's Prettier configuration. If unavailable, use:

```json
{
  "printWidth": 120,
  "tabWidth": 2,
  "useTabs": false,
  "semi": true,
  "singleQuote": true,
  "trailingComma": "es5",
  "bracketSpacing": true,
  "arrowParens": "always"
}
```

**Important**: Always check `prettier.config.mjs` before generating code.

---

## 5. TypeScript Standards

### Types vs Interfaces

```typescript
// Use interface for object shapes
interface User {
  id: string;
  name: string;
  email: string;
}

// Use type for unions and tuples
type Status = "pending" | "active" | "disabled";
type Coordinates = [number, number];
```

### Strict Rules

- **NO `any`**: Use `unknown` if uncertain
- **Avoid `!`**: Use optional chaining `?.` or logical checks
- **Explicit returns**: Always define return types for exported functions

---

## 6. Supabase & Database

### Client Usage

```typescript
// Client Components
import { createBrowserClient } from "@/lib/supabase/client";

// Server Components / API / Server Actions
import { createServerClient } from "@/lib/supabase/server";
```

### Query Rules

- Always select specific columns (avoid `SELECT *`)
- Use RLS (Row Level Security) policies
- Never expose Service Role key on client

---

## 7. Validation (Zod)

Validate all inputs from API requests, Server Actions, and Forms.

```typescript
import { z } from "zod";

const CreatePostSchema = z.object({ title: z.string().min(5).max(100), content: z.string().min(10) });

export async function createPost(formData: FormData) {
  const data = CreatePostSchema.parse(Object.fromEntries(formData));
  // ...
}
```

---

## 8. Server Actions & API

### Server Actions

- Prefer over API routes for form mutations
- Use `useActionState` for loading states
- Revalidate cache after mutations:
  ```typescript
  revalidatePath("/dashboard");
  ```

### API Routes

- Handle errors with try/catch
- Return standardized responses:
  ```typescript
  return NextResponse.json({ error: "Invalid input" }, { status: 400 });
  ```
- Check HTTP methods explicitly (GET, POST, etc.)

---

## 9. React Best Practices

- **Components**: Functional components only
- **Hooks**: Extract logic to custom hooks (`useDebounce`, `useToggle`)
- **Props**: Destructure in function signature
- **Memoization**: Use `useMemo` for expensive calculations, `useCallback` only when necessary

---

## 10. JSDoc Documentation

Add JSDoc comments for:

- Exported functions and hooks
- Complex utility functions
- Types and interfaces

Do NOT add JSDoc for:

- Obvious props (`className`, `children`, `onClick`)
- Simple self-explanatory interfaces

```typescript
/**
 * Fetches a single blog post by its unique identifier.
 *
 * @param {string} id - The UUID of the post to retrieve.
 * @returns The post object or null if not found.
 * @throws {DatabaseError} If the database connection fails.
 */
export async function getPostById(id: string): Promise<BlogPost | null> {
  // implementation
}
```

---

## 11. Testing Guidelines

- Use Vitest for unit tests
- Use React Testing Library for component tests
- Test edge cases (null, undefined, empty arrays)
- Group tests with `describe` blocks

---

## 12. Component Example

```tsx
import { type ReactNode } from "react";
import { cn } from "@/lib/utils";

interface ButtonProps {
  children: ReactNode;
  variant?: "primary" | "secondary";
  onClick?: () => void;
}

export function Button({ children, variant = "primary", onClick }: ButtonProps) {
  return (
    <button
      className={cn("px-4 py-2 rounded-md", variant === "primary" ? "bg-blue-500 text-white" : "bg-gray-200")}
      onClick={onClick}
    >
      {children}
    </button>
  );
}
```
