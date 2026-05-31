# AGENTS.md

## Project Overview

This is a full-stack monorepo using **npm workspaces** with two packages:

- `frontend/` — Next.js 16 application (App Router, Tailwind CSS, TypeScript)
- `backend/` — AWS CDK v2 infrastructure-as-code (TypeScript)

## Monorepo Structure

```
├── frontend/            Next.js application
│   └── src/app/         App Router (layouts, pages, components)
├── backend/             AWS CDK infrastructure
│   ├── bin/app.ts       CDK app entry point
│   └── lib/             Stack and construct definitions
├── eslint.config.mjs    Root ESLint flat config (TypeScript + Prettier)
├── .prettierrc          Prettier configuration
├── .husky/pre-commit    Pre-commit hook (lint-staged)
└── package.json         Root workspace config and shared dev tooling
```

## Key Rules

- **Always install dependencies from root** using `npm install`. Never run `npm install` inside `frontend/` or `backend/` directly.
- **Add workspace dependencies** with `npm install <pkg> -w frontend` or `npm install <pkg> -w backend`.
- **Root devDependencies** are for shared tooling only (ESLint, Prettier, Husky, lint-staged).
- Each workspace has its **own tsconfig.json** — they are independent.
- The frontend has its **own eslint.config.mjs** with Next.js-specific rules. The root ESLint config covers the backend and any root-level files.

## Commands

All commands run from the project root:

| Command              | Purpose                            |
| -------------------- | ---------------------------------- |
| `npm run dev`        | Start Next.js dev server           |
| `npm run build`      | Build the frontend for production  |
| `npm run cdk synth`  | Synthesize CloudFormation template |
| `npm run cdk deploy` | Deploy CDK stack to AWS            |
| `npm run lint`       | Lint the entire repo               |
| `npm run format`     | Format all files with Prettier     |

## Frontend Guidelines

- Pages and layouts live in `frontend/src/app/`
- Uses Tailwind CSS for styling (v4, configured via PostCSS)
- App Router conventions: `page.tsx`, `layout.tsx`, `loading.tsx`, `error.tsx`
- Check `frontend/node_modules/next/dist/docs/` for up-to-date Next.js API docs if unsure about conventions

## Backend Guidelines

- CDK stacks are defined in `backend/lib/`
- The app entry point is `backend/bin/app.ts`
- Uses `ts-node` to run TypeScript directly (no build step needed for synth/deploy)
- Always run `npm run cdk diff` before deploying to review changes
- Prefer L2 constructs over L1 (raw CloudFormation)
- Stateful resources (databases, S3 buckets) should have `removalPolicy` explicitly set

## Code Style

- ESLint + Prettier enforced via pre-commit hook
- Double quotes, semicolons, trailing commas, 100 char line width
- All TypeScript — no plain JavaScript files
