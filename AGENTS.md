<!-- BEGIN:nextjs-agent-rules -->

# This is NOT the Next.js you know

This version has breaking changes — APIs, conventions, and file structure may all differ from your training data. Read the relevant guide in `node_modules/next/dist/docs/` before writing any code. Heed deprecation notices.
<!-- END:nextjs-agent-rules -->

## Conventions

- **Package manager:** bun (not npm/pnpm). Use `bun run`, `bunx`, never `npm run` or `npx`.
- **App Router only.** No Pages Router.
- **Tailwind v4:** CSS-first — no `tailwind.config.ts`. No `@apply`; use `@theme inline` or plain CSS.
- **`@/*`** maps to `./src/*` — all code lives under `src/`.
- **shadcn/ui (base-nova):** `style: base-nova`, primitives: `@base-ui/react`, icons: `hugeicons`. Components in `src/components/ui/` are auto-generated — never manually edit.
- **Server Components** by default. Add `"use client"` only when using hooks/event handlers.
- **Props** must be typed with interfaces. No `any`.
- **`env.mjs`** at root — always import `env` from `@/env.mjs`, never read `process.env` directly.

## Tooling

- **Prettier** with `@trivago/prettier-plugin-sort-imports` (import order: react → next → third-party → `@/components` → `@/lib` → `./relative`).
- **commitlint** conventional commits (`feat:`, `fix:`, `chore:`, etc.).
- **lint-staged** runs `eslint --fix` then `prettier --write` on staged files.
- **Testing:** Vitest (unit), Playwright (e2e). Both use `bun run`.
- **Monitoring (Sentry)** is deferred — add when you have users.

## Scripts

| Command                | What it does         |
| ---------------------- | -------------------- |
| `bun run dev`          | Dev server           |
| `bun run build`        | Production build     |
| `bun run lint`         | ESLint               |
| `bun run lint:fix`     | ESLint with auto-fix |
| `bun run format`       | Prettier write all   |
| `bun run format:check` | Prettier check only  |
| `bun run typecheck`    | `tsc --noEmit`       |
| `bun run test`         | Vitest watch         |
| `bun run test:run`     | Vitest single-run    |
| `bun run test:e2e`     | Playwright           |

## File Structure

```
src/
├── app/          → App Router pages
├── components/
│   ├── layout/   → Header, Footer, MobileMenu, etc.
│   ├── sections/ → Page-specific sections
│   └── ui/       → shadcn/base-nova (auto-generated)
├── lib/          → Utilities, constants, metadata
└── types/        → Shared TypeScript types (add as needed)
```

## Apply the full preflight checklist

```bash
/claude-code-skills webapp-preflight
```

This runs preflight, CI, testing, env-validation, security-headers, and SEO setup in sequence.
