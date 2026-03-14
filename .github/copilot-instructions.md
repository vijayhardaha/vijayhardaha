**Purpose**

This repository is primarily a curated collection of project configuration templates (NextJS, Parcel, Svelte) and developer-tooling presets rather than a single runnable application. These instructions help an AI coding agent be productive here by explaining the repo intent, key files, and repository-specific workflows.

**Repo Shape**

- **Root:** contains personal README and examples; not all projects live here.
- **Configs:** see [configs/NextJS](../configs/NextJS/README.md) — this folder holds the canonical, production-ready templates (Prettier, ESLint, Next config, VS Code settings).

**What to assume before making changes**

- The repository holds templates, not a single app. Do not assume a `package.json` at the repo root — check first before running scripts.
- When updating configuration templates, keep them self-contained and avoid references to a root-level build system unless you confirm it exists in the target project.

**Key files to inspect (examples)**

- `configs/NextJS/README.md`: describes the deploy script and the intent of files in the NextJS template.
- `configs/NextJS/next.config.ts`: central Next.js config (e.g. `reactStrictMode: true`).
- `configs/NextJS/prettier.config.mjs` and `eslint.config.mjs`: formatting and linting rules used by downstream projects.
- `.vscode/settings.json` under the NextJS config: recommended editor automation (format on save, cspell, etc.).

**Project-specific conventions**

- Tabs are used consistently in the `configs/NextJS` templates and Prettier is configured to enforce that style — preserve tab indentation when editing those templates.
- Tailwind/Tailwind-class sorting is integrated into Prettier in the NextJS templates — avoid reordering those rules unless necessary.
- `next.config.ts` contains commented workflow hints: prefer `npm run dev`, `npm run build`, `npm run start` in downstream Next.js projects.

**Developer workflows & verification**

- To verify changes to a config template, create or use a small Next.js project and copy the template files into it (the `deploy_nextjs_configs` function is documented in `configs/NextJS/README.md`).
- Always check for the presence of `package.json` inside the target project before running npm/yarn/pnpm scripts.
- If adding or updating CI or GitHub files, ensure they are minimal and reference the correct package manager by detecting `package-lock.json`, `yarn.lock`, or `pnpm-lock.yaml` in the target repository.

**Merging policy for existing agent docs**

- If a `.github/copilot-instructions.md` already exists, preserve any project-specific operational steps and examples. Merge new template-focused guidance below the existing content, and add a short changelog header noting the merge.

**When to ask the user**

- If a change to a template could break downstream projects (e.g., changing TypeScript target or removing an ESLint rule), ask whether to bump a major version and whether to run a smoke-test in a sample project.

**Common tasks an agent may perform here**

- Add or update a configuration file inside `configs/NextJS` and include a brief rationale in the PR description.
- Add examples or small test harnesses demonstrating the template applied to an actual project (recommended before changing compiler options).
- When in doubt about running project scripts, ask the user to confirm the target project and package manager.

**Where to look for context**

- Start at [configs/NextJS/README.md](../configs/NextJS/README.md) for maintainer intentions and `deploy_nextjs_configs` usage.
- Inspect `configs/NextJS/next.config.ts` for Next.js-specific runtime hints.
- Use the root `README.md` for author notes and contact links.

Please review this draft and tell me if you'd like more examples (e.g., a sample smoke-test script or explicit `package.json` script checks) or any additional repository-specific rules to include.
