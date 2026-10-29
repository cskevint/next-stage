# Next-Stage

A modern, type-safe Next.js starter template designed for AI-driven development.

## Features

- **Package Manager**: Bun 1.3.14
- **Framework**: Next.js 16.3.6 with App Router
- **Runtime**: React 19.2.8, React DOM 19.2.8
- **Language**: TypeScript 7.0.2 (type-checking; TypeScript 6.0.3 kept as `typescript` for tooling that needs the JS API)
- **API Framework**: Hono 4.13.0
- **API Validation**: @hono/zod-validator 0.7.6
- **UI Components**: shadcn/ui
- **Styling**: Tailwind CSS 4.3.3
- **Form Management**: React Hook Form 7.84.0
- **Form Validation**: Zod 4.4.3
- **Icons**: lucide-react 1.28.0
- **Linting & Formatting**: Biome 2.3.8, Markuplint 4.18.3
- **Testing**: Playwright 1.61.1, Bun test runner
- **Supply Chain Security**: Minimum Release Age

## Getting Started
Before you start, make sure you have the following installed:

```bash
bun install
```

Bun is an all-in-one JavaScript runtime & toolkit designed for speed, complete with a bundler, test runner, and Node.js-compatible package manager.

This project uses [Bun](https://bun.sh/) to manage dependencies and run scripts.

### Environment Setup（Optional）
If you want to use environment variables, follow these steps:

1. Copy the `.env.example` file to `.env.local`:

```bash
cp .env.example .env.local
```

2. Update the environment variables in `.env.local` as needed.

### Agent Skills Setup（Recommended）
If you use an AI coding agent (Claude Code, Cursor, Codex, Windsurf, Gemini CLI, etc.), install the project's default skills:

```bash
bun run skills
```

This installs the skills listed in [Agent Skills](#agent-skills) into `.agents/skills/` and links them for the agents it detects on your machine (e.g. `.claude/skills/`). Installed skills are gitignored, so each developer runs this once after cloning, and again whenever the list changes. Restart your agent afterward so it picks them up.

The same command also updates skills: each run reinstalls every listed skill at its latest version, so run `bun run skills` again whenever you want to pick up updates.

### Development

Run the development server:

```bash
# Using bun
bun dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `src/app/page.tsx`. The page auto-updates as you edit the file.

## Project Structure

```
├── public/             # Static assets
├── src/
│   ├── app/            # App router routes
│   │   ├── _components/  # App-specific components
│   │   └── _styles/      # App-specific styles
│   ├── components/     # UI components
│   │   ├── layout/     # Layout components
│   │   └── ui/         # UI components from shadcn/ui
│   ├── config/         # Configuration files
│   ├── lib/            # Utility functions
│   └── types/          # Type definitions
├── e2e/                # E2E tests
├── _llm-rules/         # Base rules for AI-assisted development
├── _llm-docs/          # Base docs for AI-assisted development
├── _tasks/             # Task files
├── .env.example        # Example environment variables
└── ...                 # Config files
```

## Supply Chain Security

This project implements supply chain attack protection using Bun's built-in security features.

### Minimum Release Age

To protect against newly published malicious packages, this project enforces a minimum release age requirement:

```toml
[install]
# Only install package versions published at least 1 day ago (1440 minutes)
minimumReleaseAge = 1440
```

This helps mitigate supply chain attacks by ensuring packages have been publicly available long enough for the community to detect potential issues.

### Trusted Packages (Exclusions)

Well-established packages from trusted organizations bypass the minimum age requirement:

```toml
minimumReleaseAgeExcludes = [
  "@types/bun",
  "typescript",
  "@playwright/test",
  "react",
  "react-dom",
  "next",
  "@types/node",
  "@types/react",
  "@types/react-dom",
  "tailwindcss",
  "@tailwindcss/postcss",
  "@biomejs/biome",
  "hono",
  "@hono/zod-validator",
  "zod",
  "react-hook-form",
]
```

For more details, see [Bun's bunfig.toml documentation](https://bun.sh/docs/runtime/bunfig).

## Code Quality with Biome and Markuplint

This project uses [Biome](https://biomejs.dev/) for linting and formatting JavaScript/TypeScript code. Biome is a fast, modern JavaScript/TypeScript toolchain that replaces ESLint and Prettier.

Additionally, [Markuplint](https://markuplint.dev/) is used for linting JSX/TSX markup to ensure high-quality, accessible, and consistent UI components.

### Available Commands

```bash
# Run development server
bun run dev

# Run production build
bun run build

# Run all linters (Markuplint and Biome)
bun run lint

# Run both linting and formatting with auto-fixes
bun run check

# Run unit tests
bun run test:unit

# Run e2e tests
bun run test:e2e

# Run UI mode tests
bun run test:e2e:ui

# Run e2e codegen
bun run test:codegen

# Install the default agent skills
bun run skills
```

## AI-Driven Development Rules
This project supports AI-assisted development with predefined rules for writing clean, maintainable, and scalable code.

### Universal AI Agent Support
The project includes `AGENTS.md` following the [agents.md standard](https://agents.md/) - a universal format that works across all AI coding agents and tools.

### Supported AI Tools:

#### AI Editors:
- [Cursor](https://www.cursor.com/) - Generated rules in `.cursor/rules/`
- [Windsurf](https://codeium.com/windsurf) - Generated rules in `.windsurf/rules/`
- [GitHub Copilot](https://github.com/features/copilot) - Generated instructions in `.github/`
- [Kiro](https://kiro.dev/) - Generated rules in `.kiro/steering/`

#### AI CLI Tools:
- [Claude Code](https://claude.ai/code) - Uses `CLAUDE.md`
- [Google Gemini CLI](https://gemini.google.com/) - Uses `GEMINI.md`

### Rule File Hierarchy
The project maintains a hierarchical rule system:

1. **Base Rules** (`_llm-rules/` directory):
   - `core-rule.md`: Core task execution methodology
   - `nextjs-rule.md`: Next.js specific development patterns
   - `test-rule.md`: Testing guidelines and best practices

2. **Universal Format**:
   - `AGENTS.md`: Universal format following agents.md standard

3. **Tool-Specific Files**:
   - `CLAUDE.md`: Claude CLI specific instructions
   - `GEMINI.md`: Google Gemini CLI specific instructions
   - Generated editor files: `.cursor/`, `.windsurf/`, `.github/`, `.kiro/`

### Generating Editor-Specific Rules

You can generate editor-specific rule files from the base rules using the following commands:

```bash
# Generate rules for Cursor editor
bun run rules:cursor

# Generate rules for Windsurf editor
bun run rules:windsurf

# Generate rules for GitHub Copilot (instructions)
bun run rules:copilot

# Generate rules for Kiro editor
bun run rules:kiro

# Generate rules for all supported editors
bun run rules
```

### Rule File Cross-Monitoring
**Important**: When updating any rule file, all related files must be updated to maintain consistency. The project includes a cross-monitoring protocol that ensures:

- Technology stack versions remain synchronized across all rule files
- Core development patterns are consistently applied
- Changes are properly documented and validated

See `AGENTS.md` for detailed cross-monitoring requirements and procedures.

### Next.js DevTools MCP Integration

This project includes **[Next.js DevTools MCP](https://www.npmjs.com/package/next-devtools-mcp)** integration for AI coding assistants that support the [Model Context Protocol (MCP)](https://modelcontextprotocol.io).

#### What is Next.js DevTools MCP?

Next.js DevTools MCP provides a standardized interface for AI agents and coding assistants to interact with Next.js applications. It offers comprehensive tools to support Next.js development workflows.

**Key Features:**

- **MCP Tools**: Callable tools for automating Next.js upgrades and Cache Components setup
- **Development Prompts**: Pre-configured prompts for common Next.js development tasks
- **Next.js Documentation**: Access Next.js documentation and best practices
- **Browser Testing**: Integrate with Playwright for browser automation and testing
- **Next.js Agent**: Access internal state, diagnostics, and errors from running Next.js dev servers via MCP

#### Setup

The MCP server is already configured in `.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "next-devtools": {
      "command": "bunx",
      "args": ["-y", "next-devtools-mcp@latest"]
    }
  }
}
```

For complete documentation and advanced usage, visit:
- [Next.js DevTools MCP on npm](https://www.npmjs.com/package/next-devtools-mcp)
- [Next.js MCP Documentation](https://nextjs.org/docs/app/guides/mcp)

### Agent Skills

`bun run skills` installs a fixed set of [Agent Skills](https://skills.sh/) chosen for this stack, so every developer's agent works from the same guidance:

| Skill | Source | Purpose |
|---|---|---|
| `vercel-react-best-practices` | `vercel-labs/agent-skills` | React/Next.js performance rules from Vercel |
| `web-design-guidelines` | `vercel-labs/agent-skills` | Accessibility and UX review checklist |
| `shadcn` | `shadcn-ui/ui` | Official shadcn/ui usage and CLI |
| `frontend-design` | `anthropics/skills` | Distinctive UI instead of generic AI-looking design |
| `playwright-cli` | `microsoft/playwright-cli` | Drive a browser to check changes |
| `hono` | `honojs/skills` | Official Hono APIs, routing and middleware |
| `verification-before-completion` | `obra/superpowers` | Run checks before claiming work is done |
| `systematic-debugging` | `obra/superpowers` | Find root causes instead of guessing fixes |

To add or remove a skill, edit the `skills` script in `package.json`. Next.js guidance isn't on the list because Next.js 16.3+ ships it through its bundled docs and the agent rules `next dev` generates. Skills run with your agent's permissions, so review a skill's source before adding it.

## Turbopack

Next.js 16 uses [Turbopack](https://turbo.build/pack) as the default bundler for both development (`next dev`) and production builds (`next build`). This provides faster refresh rates and improved developer experience out of the box.

## Learn More

For more information about the tech stack powering this template, refer to these resources:

- [Bun](https://bun.sh/) - an all-in-one JavaScript runtime & toolkit designed for speed, complete with a bundler, test runner, and Node.js-compatible package manager.
- [Next.js](https://nextjs.org/docs) - a React framework for building full-stack applications.
- [Hono](https://hono.dev/docs/) - a small, simple, and ultrafast web framework built on Web Standards.
- [shadcn/ui](https://ui.shadcn.com/) - re-usable components built with Radix UI and Tailwind CSS.
- [Radix UI](https://www.radix-ui.com/) - a collection of composable React components for building high-quality, accessible design systems and web apps.
- [Tailwind CSS](https://tailwindcss.com/) - a utility-first CSS framework for rapidly building custom designs.
- [React Hook Form](https://react-hook-form.com/) - performant, flexible, and extensible forms with easy-to-use validation.
- [Zod](https://zod.dev/) - TypeScript-first schema declaration and validation library.
- [Biome](https://biomejs.dev/) - a fast, modern JavaScript/TypeScript toolchain that replaces ESLint and Prettier.
- [Markuplint](https://markuplint.dev/) - a linter for HTML, JSX, and other markup languages to ensure high-quality, accessible UI components.
- [Playwright](https://playwright.dev/) - a browser automation tool for testing and debugging.

## Deploy on Vercel

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/new) from the creators of Next.js.

Check out the [Next.js deployment documentation](https://nextjs.org/docs/app/building-your-application/deploying) for more details.

## References
- [Awesome CursorRules](https://github.com/PatrickJS/awesome-cursorrules)
- [cursor.directory](https://cursor.directory/)
- [kinopeee/cursorrules](https://github.com/kinopeee/cursorrules)
