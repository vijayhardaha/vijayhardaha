# ⚡ NextJS Architect Configs

A master collection of production-ready configurations and ignore files designed for high-performance Next.js development. Curated by **Vijay Hardaha**, these files enforce strict linting, consistent formatting, and optimized TypeScript behavior to ensure a "Designer Developer Experience" (DX) from the very first commit.

## 📦 What's Inside?

| File                      | Purpose                                                    |
| :------------------------ | :--------------------------------------------------------- |
| `.editorconfig`           | Global editor standards (tabs, line endings, encoding).    |
| `.gitignore`              | Prevents local noise and build artifacts from hitting Git. |
| `.prettierignore`         | Defines the "No-Format" zones for the project.             |
| `prettier.config.mjs`     | The aesthetic engine (Tabs, Tailwind plugin, formatting).  |
| `eslint.config.mjs`       | The logic guardian (Strict Next.js + TS rules).            |
| `jsconfig.json`           | IDE Intelligence and path mapping for JS files.            |
| `tsconfig.json`           | The TypeScript engine and compiler strategy.               |
| `next.config.ts`          | Framework runtime and build-time optimizations.            |
| `next-sitemap.config.js`  | Automated SEO: Sitemaps and robots.txt generation.         |
| `postcss.config.mjs`      | Modern CSS processing with Tailwind integration.           |
| `.vscode/settings.json`   | Workspace automation (Fix-on-save, CSpell, Auto-format).   |
| `.vscode/extensions.json` | Recommended toolset for team synchronization.              |
| `LICENSE`                 | Clean MIT licensing.                                       |

---

## 🚀 Instant Deployment

You can pull the entire suite into your current directory using the optimized bash script below. It includes error handling and directory creation to ensure a perfect setup.

### Option 1: The Automation Script (Recommended)

```bash
# -------------------------------------------------------------------
# Function: deploy_nextjs_configs
# -------------------------------------------------------------------
# Downloads and deploys standard configuration files for a Next.js
# project from a predefined GitHub repository.
#
# Creates necessary directories (.vscode) and downloads files listed
# in the manifest. Fails immediately if any download fails.
#
# Usage:
#   deploy_nextjs_configs
#
deploy_nextjs_configs() {
  # Base URL for configuration files
  local BASE="https://raw.githubusercontent.com/vijayhardaha/vijayhardaha/configs/nextjs/refs/heads/master"

  # List of files to download
  local files=(
    ".editorconfig"
    ".gitignore"
    ".prettierignore"
    "prettier.config.mjs"
    "eslint.config.mjs"
    "jsconfig.json"
    "tsconfig.json"
    "next.config.ts"
    "next-sitemap.config.js"
    "postcss.config.mjs"
    ".vscode/settings.json"
    ".vscode/extensions.json"
    "LICENSE"
  )

  echo "🏗️  Starting Architect Config Deployment..."

  # Ensure directories exist
  mkdir -p .vscode

  # Download each file
  for f in "${files[@]}"; do
    echo "📥 Downloading: $f"
    curl -fSL -o "$f" "$BASE/$f"
  done

  echo "✅ All configs successfully deployed. Happy coding!"
}
```

### Option 2: Individual File Fetch

If you only need a specific piece of the puzzle:

```bash
# Example: Fetching the TypeScript Engine
curl -fSL -o tsconfig.json https://raw.githubusercontent.com/vijayhardaha/vijayhardaha/configs/nextjs/refs/heads/master/tsconfig.json

# Example: Fetching VS Code Settings
mkdir -p .vscode && curl -fSL -o .vscode/settings.json https://raw.githubusercontent.com/vijayhardaha/vijayhardaha/configs/nextjs/refs/heads/master/.vscode/settings.json
```

---

## 🛠️ Developer Workflow

Once these files are in your project, your environment is fully automated:

1. **Auto-Format:** On save, Prettier sorts your Tailwind classes and enforces tab consistency.
2. **Auto-Lint:** ESLint catches logical errors and type mismatches instantly.
3. **Strict Types:** TypeScript is configured for ES2024, providing the latest language features.
4. **SEO Automation:** Sitemaps and robots.txt are generated on every build.

---

Maintained by [Vijay Hardaha](https://github.com/vijayhardaha)
