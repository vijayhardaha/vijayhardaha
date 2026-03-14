# AGENTS.md - Agentic Coding Guidelines

This repository is a **backup vault** for configuration files used across Vijay's development environment. It stores configs for various tools (IDEs, shells, desktop environments) and project templates (NextJS, Parcel, etc.) for quick deployment to new projects.

---

## 🏗️ Architecture

### Directory Structure

```
/configs/           # Main config backup directory
  /NextJS/          # Next.js project template configs
  /Parcel/          # Parcel bundler configs (future)
  /<tool-name>/     # Other tool configs (future)
/.github/           # GitHub-specific configs (copilot instructions)
/.gitignore         # Root ignore rules
/AGENTS.md          # This file - agent instructions
/PROJECT-README.md  # Project documentation
```

### Purpose

- **Backup & Restore**: Copy/download configs to new projects for consistency
- **Not Runnable**: These are backup files, not a runnable application
- **Documentation-Rich**: Every config option is documented with comments

---

## 📋 Commands

### Root Level Only

```bash
pnpm format              # Format all files with Prettier
pnpm format:check        # Check formatting without fixing
```

---

## 🎨 Config File Writing Standards

When adding new config files to `configs/`, follow these patterns:

### Header Pattern (REQUIRED)

**For JSON files:**

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

**For JS/MJS files:**

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

### Rules

- Use `====` for main headers (10+ chars)
- Use `----` for sub-sections (10+ chars)
- Use `//` for JSON comments, `/**/` for JS comments
- Every config option MUST have a comment explaining its purpose
- Include `Purpose:` and `Docs:` in the header

---

## 📝 Copilot Instructions

This repo holds **backup configs**, not a single app:

1. Check for `package.json` before running scripts
2. Keep templates self-contained
3. Preserve tab indentation in config templates
4. Always add header comments to new config files
5. Document every option in config files
