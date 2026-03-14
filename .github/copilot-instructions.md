# Copilot Instructions

**Purpose**

This repository is a backup vault for configuration files used across Vijay's development environment. It stores configs for various tools (IDEs, shells, desktop environments) and project templates (NextJS, Parcel, etc.) for quick deployment to new projects. These instructions help an AI coding agent be productive here.

**Architecture**

- **Root**: Contains README.md (GitHub profile magic file), AGENTS.md, PROJECT-README.md, package.json, and prettier.config.mjs
- **configs/**: Main directory holding all backup config files organized by tool/project type
- **configs/NextJS/**: Next.js project template configs (backup - manually controlled)
- **configs/Parcel/**: Parcel bundler configs (future)
- **configs/<tool-name>/**: Other tool configs (future)

Each config directory is self-contained and can be copied to new projects.

**What to assume before making changes**

- The repository holds backup config files, not a single runnable app.
- Do not assume a `package.json` at the repo root — check first before running scripts.
- Config files in configs/ are manually controlled backups - do not auto-format or auto-fix them unless explicitly asked.
- When updating configuration templates, keep them self-contained.

**Key points**

- Root level only has Prettier for formatting: `pnpm format` / `pnpm format:check`
- Check for `package.json` before running npm/yarn/pnpm scripts
- The configs/ directory contains backup files - they are not part of this project's codebase

**Config File Writing Standards**

When adding new config files to `configs/`, follow these patterns:

For JSON files:

```json
// =======================================================================
// File Name
// =======================================================================
// Purpose: Brief description of what this config does
// Docs: https://link.to/docs
// =======================================================================

{
  // ---- Section Name ----
  // Option description
  "option": "value"
}
```

For JS/MJS files:

```javascript
/**
 * ======================================================================
 * File Name
 * ======================================================================
 * Purpose: Brief description of what this config does
 * Docs: https://link.to/docs
 * ======================================================================
 */

/** @type {import('...').Config} */
const config = {
  // ---- Section Name ----
  // Option description
  option: "value"
};

export default config;
```

Rules:

- Use `====` for main headers (10+ chars)
- Use `----` for sub-sections (10+ chars)
- Every config option MUST have a comment explaining its purpose
- Include `Purpose:` and `Docs:` in the header

**When to ask the user**

- When unsure about running project scripts
- Before making changes to backup config files
