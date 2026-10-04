# Next.js App Boilerplate

A general-purpose application bootstrap. Copy this directory to start a new
project with a working Next.js foundation already configured.

## Stack

- **Next.js 16** (App Router) + **React 19**
- **TypeScript** in strict mode with an `@/*` import alias to `src/`
- **Tailwind CSS 4** + **daisyUI 5**
- **ESLint 9** (Next.js core-web-vitals and TypeScript configs) + **Prettier**
- **pnpm** as the package manager (pinned via `packageManager`)
- **Node.js 22** development baseline (`.nvmrc`)

## Requirements

- Node.js 22 or newer (`.nvmrc`).
- pnpm, pinned in `package.json`. If it is not on your PATH, enable it with
  Corepack:

  ```sh
  corepack enable pnpm
  pnpm --version
  ```

  Corepack uses the project's pinned package-manager version. On a system where
  you cannot enable shims, run `corepack pnpm` in place of `pnpm` in the
  commands below. Corepack must be installed separately if your Node.js
  distribution does not include it.

## Getting started

After copying this directory into a new project, update the package name in
`package.json` and the title and description in `src/app/layout.tsx`, then
replace `src/app/page.tsx` with your own content.

```sh
pnpm install --frozen-lockfile
pnpm dev
```

Open <http://localhost:3000>.

## Commands

```sh
pnpm dev          # Start the development server
pnpm build        # Production build
pnpm start        # Serve the production build
pnpm lint         # ESLint, fails on any warning
pnpm typecheck    # Next.js route types + tsc --noEmit
pnpm format       # Prettier write
pnpm format:check # Prettier check
```

`typecheck` generates Next.js route types before checking TypeScript, so it
also works before the first build.

## Verification

```sh
pnpm lint
pnpm typecheck
pnpm format:check
pnpm build
```

To run the production build locally:

```sh
pnpm build
pnpm start
```

Use `pnpm install` when intentionally changing dependencies and commit the
updated `pnpm-lock.yaml`. Use `pnpm install --frozen-lockfile` for clean
checkouts and CI. The project uses a single pnpm lockfile; do not generate
lockfiles with other package managers.

`pnpm-workspace.yaml` explicitly allows the native resolver dependency's
installation script (`unrs-resolver`); other dependency build scripts remain
blocked by pnpm's default policy. This configuration does not make the app a
monorepo.

## Structure

```text
src/app/
├── globals.css  # Tailwind CSS 4 and daisyUI 5
├── layout.tsx   # Required root layout and metadata
└── page.tsx     # Placeholder home page
```

Config files at the root cover TypeScript (`tsconfig.json`), ESLint
(`eslint.config.mjs`), PostCSS/Tailwind (`postcss.config.mjs`), Prettier
(`.prettierrc.json`, `.prettierignore`), and pnpm (`pnpm-workspace.yaml`).

## Dependency audits

```sh
pnpm audit --prod
pnpm audit
```

The production dependency audit reports no vulnerabilities. The full audit may
report advisories in development-only dependency chains (for example `braces`
and its dependents under the Next.js ESLint plugins). These are development-only
and do not affect the production build.

ESLint 9 is used because the installed React and accessibility lint plugins do
not declare support for ESLint 10. ESLint 9 is marked unsupported upstream.
These development tooling limitations need review as upstream packages are
updated.
