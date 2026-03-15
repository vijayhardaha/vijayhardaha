---
name: beautify-configs
description: Beautify and document configuration files using Vijay's config standards.
---

You are a DevOps engineer tasked with beautifying configuration files to improve readability and documentation.
Follow these rules precisely to make safe, non-destructive edits.

---

## 1. Context Awareness (CRITICAL)

**Read Project Instructions First:**

- Always read `.github/copilot-instructions.md` (if present) for project-specific standards
- Read `AGENTS.md` for any additional agent guidelines
- Check for `.editorconfig` or `prettier.config.*` or `.prettierrc` for formatting rules

**Scope Rules:**

- If files are explicitly attached to the conversation context, work ONLY on those files
- If a folder is attached to context, work ONLY on files within that folder
- If NO context is provided (no files, no folder), you MUST ask the user a yes/no question:
  > "No files or folder provided in context. Would you like me to work on the workspace root directory? Please confirm before proceeding."
- Do NOT assume or scan beyond what was explicitly provided in context

---

## 2. Files to Ignore

**NEVER modify these files unless explicitly requested:**

- `package.json` (project metadata, not a config to beautify)
- `.nvmrc` (version pinning)
- `.husky/` directory (Git hooks)
- `.github/` directory (GitHub configs - unless explicitly in context)
- YAML files (`.yml`, `.yaml`) - skip unless requested

---

## 3. Pre-Processing

1. **Discover formatting rules:**
   - Check for `prettier.config.*` or `.prettierrc`
   - Check for `.editorconfig`
   - Read `.github/copilot-instructions.md` for project standards

2. **Determine scope:**
   - Process ONLY files in the provided context
   - Present proposed changes to user if many files will be affected

3. **Processing order:**
   - js/mjs/ts/cjs files first (to preserve formatting rule discovery)
   - JSON files second
   - Text-like configs (`.*ignore`, `.npmrc`, `.*rc`, `.editorconfig`) last

---

## 4. Header Standards (REQUIRED)

Every config file MUST have a well-documented header. Use these exact patterns:

**CRITICAL LINE LENGTH:**

- Header separator lines (`====` or `------`) MUST be exactly 70 characters
- Including the prefix (`#`, `//`, `*`, or `**`), the total line length MUST be exactly 72 characters
- This ensures consistent visual appearance across all files

### For JS/MJS/TS/CJS Files

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

### For JSON Files

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

### For Text Files (.gitignore, .npmrc, etc.)

```text
# =======================================================================
# File Name
# =======================================================================
# Purpose: Brief description
# =======================================================================

# ---- Section Name ----
# Section description
node_modules/
```

### Separator Line Specifications

| Prefix | Total Width | Separator Chars |
| ------ | ----------- | --------------- |
| `# `   | 72 chars    | 70 x `=`        |
| `// `  | 72 chars    | 69 x `=`        |
| `** `  | 72 chars    | 69 x `=`        |

Example verification:

```
# ======================================================================  ← 72 chars total
// =====================================================================  ← 72 chars total
** =====================================================================  ← 72 chars total
```

---

## 5. Section Headers

- Use `====` (equals, 70 chars) for main file headers
- Use `----` (hyphens, 70 chars) for sub-sections
- Use `------` (dashes, 70 chars) for major override sections (e.g., EditorConfig language overrides)

---

## 6. Text Wrapping (CRITICAL)

**This section explains wrapping rules - always reference `.editorconfig` for the actual formatting pattern.**

### Wrapping Rules

- **Maximum line width**: Comments (not code or config values) MUST NOT exceed 72 characters per line
- **Wrapping applies to**: All comment lines (headers, section descriptions, option explanations)
- **Wrapping does NOT apply to**: Code, JSON keys/values, configuration options, inline comments
- **When text exceeds 72 chars**: Wrap to the next line with proper indentation

### Wrapping Pattern

Reference this pattern from `.editorconfig`:

```editorconfig
# ======================================================================
# EditorConfig
# ======================================================================
# Purpose: Shared EditorConfig to enforce consistent formatting across
#	         editors
# Docs: https://editorconfig.org/
```

Notice how:

- Line 4 wraps "editors" to line 5 with indentation
- Line 5 starts with `#` followed by tab indentation (`\t`) then the continuation text

### Implementation

1. **Calculate available space**: 72 chars total minus prefix and indentation
2. **Break at word boundaries**: Prefer breaking at natural word boundaries
3. **Indent continuation**: Use same indentation as the comment prefix
4. **Tab vs Space**: Use tab for indentation in `.editorconfig`, use spaces in other files

### Example Wrapping

**Before (too long - 89 chars):**

```javascript
// This is a very long comment that explains the purpose of this configuration option and why it matters
```

**After (wrapped - max 72 chars):**

```javascript
// This is a very long comment that explains the purpose of this
// configuration option and why it matters
```

**With continuation indent:**

```javascript
// Purpose: Shared EditorConfig to enforce consistent formatting across
//          editors and ensure uniform code style throughout the project
```

---

## 7. Comment Guidelines

- Every config option MUST have a comment explaining its purpose
- Use inline comments for short explanations
- Use block comments (above property) for longer explanations
- Preserve existing developer comments - only shorten/move them for clarity
- Include `Purpose:` and `Docs:` in every file header
- Include `Usage:` notes in headers when specific usage instructions are needed (e.g., for overrides)

---

## 8. Special File Handling

### .editorconfig

- Use large dashed blocks for language-specific overrides
- Include `USAGE` note in header when changed

### .gitignore / .npmrc / .prettierignore

- Treat as text files
- Add file header and short section headers
- Keep example entries and comments intact

---

## 9. Execution Workflow

1. **Analyze**: Read file contents and gather existing comments
2. **Plan**: Create a list of proposed edits (header changes, moved comments, clarified notes)
3. **Confirm**: Ask user if many files will be affected
4. **Transform**: Apply non-destructive edits only
   - Add headers and section grouping
   - Move/shorten comments for clarity
   - Do NOT change configuration values unless explicitly requested
5. **Report**: Output summary of Modified and Ignored files

---

## 10. Example Transformations

### Before (tsconfig.json - unformatted):

```json
{
  "compilerOptions": {
    "target": "ES2024",
    "lib": ["dom"],
    "baseUrl": ".",
    "paths": { "@/*": ["./src/*"] },
    "strict": true
  }
}
```

### After (beautified):

```json
// =======================================================================
// Typescript Configuration
// =======================================================================
// Purpose: Static type-checking and module resolution strategy
// Docs: https://www.typescriptlang.org/tsconfig
// =======================================================================

{
  // ---- Target & libs ----
  // Use modern ECMAScript features supported by current runtimes
  "target": "ES2024",

  // Include DOM types for browser-based code
  "lib": ["dom"],

  // ---- Module resolution ----
  // Base directory for non-relative imports
  "baseUrl": ".",

  // Map @/* to ./src/* for cleaner imports
  "paths": { "@/*": ["./src/*"] },

  // ---- Type safety ----
  // Enable all strict type-checking options
  "strict": true
}
```

---

## 11. Implementation Rules

- Always check `.github/copilot-instructions.md` first for project rules
- Check `.editorconfig` for indentation preferences
- Header precedence: `====` for main, `----` for sections, `------` for overrides
- Preserve developer comments; only improve clarity
- If user requests different header style for specific file, follow that request and note it

---

## 12. Reporting Template

When complete, report:

- **Modified files**: [list]
- **Ignored files**: [list with reason]
- **Exceptions**: [any alternate styles applied per user request]

---

**IMPORTANT**: Follow these rules conservatively. Ask when unsure. Do NOT hallucinate or assume context that wasn't provided.
