# Next.js + AWS CDK Monorepo Template

A full-stack monorepo template with a **Next.js 16** frontend and **AWS CDK** (TypeScript) backend, managed with npm workspaces.

## What's Included

- **Frontend** — Next.js 16 with App Router, Tailwind CSS, TypeScript, `src/` directory
- **Backend** — AWS CDK v2 with TypeScript, empty stack ready to build on
- **Tooling** — ESLint (flat config), Prettier, Husky pre-commit hooks with lint-staged
- **npm workspaces** — all dependencies installed from root

## Getting Started

```bash
# Install all dependencies (from root)
npm install

# Start the frontend dev server
npm run dev

# Synthesize the CDK stack
npm run cdk synth
```

## Project Structure

```
├── frontend/          Next.js application
│   └── src/app/       App Router pages and layouts
├── backend/           AWS CDK infrastructure
│   ├── bin/           CDK app entry point
│   └── lib/           Stack definitions
├── eslint.config.mjs  Root ESLint config
├── .prettierrc        Prettier config
└── .husky/            Git hooks (pre-commit: lint-staged)
```

## Scripts

| Command                | Description                          |
| ---------------------- | ------------------------------------ |
| `npm install`          | Install all workspace dependencies   |
| `npm run dev`          | Start Next.js dev server             |
| `npm run build`        | Build the frontend for production    |
| `npm run cdk synth`    | Synthesize CloudFormation template   |
| `npm run cdk deploy`   | Deploy the CDK stack                 |
| `npm run lint`         | Lint the entire repo                 |
| `npm run format`       | Format the entire repo with Prettier |
| `npm run format:check` | Check formatting without writing     |

## Customisation

After creating a repo from this template:

1. Update `"name"` in the root `package.json`
2. Rename `BackendStack` in `backend/lib/backend-stack.ts` and `backend/bin/app.ts`
3. Start adding your infrastructure in `backend/lib/` and pages in `frontend/src/app/`

## Prerequisites

- Node.js 20+
- npm 10+
- AWS CLI configured (for CDK deployments)
- AWS CDK bootstrapped in your target account/region (`cdk bootstrap`)
