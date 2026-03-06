# Project: syntek-docs

**Last Updated**: 06/03/2026
**Version**: 1.0.0
**Maintained By**: Syntek Studio Development Team
**Language**: British English (en_GB)
**Timezone**: Europe/London

---

## Table of Contents

- [Stack Overview](#stack-overview)
- [Coding Principles](#coding-principles)
- [Skill Targets](#skill-targets)
- [Repository Purpose](#repository-purpose)
- [Key Locations](#key-locations)
- [Documentation Standards](#documentation-standards)
- [Development Commands](#development-commands)
- [Deployment](#deployment)
- [Content Conventions](#content-conventions)
- [Related Repositories](#related-repositories)

---

## Stack Overview

| Component       | Technology                                        |
| --------------- | ------------------------------------------------- |
| **Type**        | Documentation Site                                |
| **Purpose**     | Canonical documentation for the Syntek ecosystem  |
| **Format**      | Markdown source → Docusaurus static site          |
| **Renderer**    | Docusaurus (React-based static site generator)    |
| **Language**    | Markdown (MDX where needed), British English      |
| **Hosting**     | `syntek-infrastructure` (Hetzner, via Cloudflare) |
| **Environment** | Node.js (NO Docker — static site only)            |

---

## Coding Principles

All content and any configuration code in this project follows Rob Pike's 5 Rules of Programming and Linus Torvalds' Coding Rules.

**Core rules:**

- Measure before optimising — no speed hacks without profiling
- Simple structures over fancy ones — clear headings over clever nesting
- Data structures dominate: get the information architecture right and the content becomes obvious
- Short, focused sections that cover one topic
- Eliminate special cases rather than patching them
- Make it work first, then make it better
- Favour stability and readability over cleverness

See `.claude/CODING-PRINCIPLES.md` for the full rules.

---

## Skill Targets

- **Stack Skill:** `stack-react` (nearest match — Docusaurus is React-based)
- **Global Skill:** `global-workflow`

---

## Repository Purpose

`syntek-docs` is the **canonical documentation source** for the entire Syntek ecosystem. It is the single source of truth for:

- Getting started guides for self-hosted `syntek-platform` developers
- API reference for `syntek-modules` (npm + PyPI packages)
- Extension development guide (building, testing, submitting to `syntek-store`)
- Template development guide (building, submitting to `syntek-store`)
- `syntek-ai` task and prompt reference (public-facing portion only)
- Infrastructure runbooks (internal, restricted section)
- Licensing, billing, and renewal documentation
- Changelogs per product

**Contribution model:**

- Platform core changes must include a docs update in the same PR
- Extension or template authors must submit docs before their product is listed in `syntek-store`
- All public API changes are documented before release

---

## Key Locations

| Path                                | Purpose                                              |
| ----------------------------------- | ---------------------------------------------------- |
| `docs/PLANS/`                       | Architecture plans and decision documents            |
| `docs/PLANS/SYNTEK-ARCHITECTURE.md` | Full ecosystem architecture overview (canonical)     |
| `docs/METRICS/`                     | Self-learning system data (agent metrics + feedback) |
| `.claude/CLAUDE.md`                 | This file — project context for Claude agents        |
| `.claude/CODING-PRINCIPLES.md`      | Rob Pike + Linus Torvalds coding rules               |
| `.claude/SYNTEK-GUIDE.md`           | Full Syntek Dev Suite plugin usage guide             |
| `.claude/plugins/`                  | Python plugin tools for agent automation             |
| `.claude/commands/`                 | Project-specific slash commands                      |

---

## Documentation Standards

### File Naming

- All documentation files: `UPPER-KEBAB-CASE.md` (e.g., `SYNTEK-ARCHITECTURE.md`)
- All plan files: `PLAN-FEATURE-NAME.md` (e.g., `PLAN-SYNTEK-AI-AND-MULTI-TENANCY.md`)

### Markdown Metadata Header

Every `.md` file must include a metadata header:

```markdown
# Document Title
```

### Language and Style

- **British English** throughout (colour not color, licence not license for noun, etc.)
- Date format: `DD/MM/YYYY`
- Time format: 24-hour clock (`14:30`)
- Currency: GBP (£)
- Use active voice; avoid passive where possible
- One idea per paragraph
- Tables for comparisons and reference data
- Code blocks for all commands, file paths, and code samples

### Document Structure

Every document should have:

1. Metadata header
2. Table of contents (for documents longer than ~200 lines)
3. Clear `##` section headings
4. No orphaned content — every section belongs under a heading

### Content Rules

- No feature ships without a corresponding entry here
- PRs that add or change public APIs must include a docs update
- Docs updates are reviewed in the same PR as the code change
- All code examples must be tested and correct
- All links must be verified before merge

---

## Development Commands

```bash
# Install dependencies
npm install

# Start local dev server (hot reload)
npm start                     # http://localhost:3000

# Build static site
npm run build

# Serve built static site locally
npm run serve

# Check for broken links
npm run check-links

# Lint markdown files
npm run lint:md
```

---

## Deployment

The built static site is deployed to `syntek-infrastructure` (Hetzner) via Cloudflare Tunnels.

- **Staging:** Automatic deploy on merge to `staging` branch
- **Production:** Automatic deploy on merge to `main` branch
- **URL:** `docs.syntekstudio.com` (or configured subdomain)

Deployment is managed by the CI/CD pipeline and NixOS service definitions in `syntek-infrastructure`. No manual server access is required or permitted.

---

## Content Conventions

### Adding New Documentation

1. Create the file in the correct section folder
2. Add the metadata header
3. Add to the sidebar configuration (`sidebars.js`)
4. Link from relevant parent documents
5. Update the section `README.md` if one exists

### Updating Existing Documentation

1. Update the `**Last Updated**` date in the metadata header
2. Keep the `**Version**` in sync with the relevant product version
3. Do not delete content without redirecting old URLs

### Plan Documents (`docs/PLANS/`)

Plan documents describe architectural decisions, technical choices, and feature designs. They are not user-facing documentation but are committed here so the whole team can reference the decision history.

Format: `PLAN-FEATURE-NAME.md`

---

## Related Repositories

| Repository              | Relationship                                                  |
| ----------------------- | ------------------------------------------------------------- |
| `syntek-platform`       | Core platform — PRs must include docs updates                 |
| `syntek-modules`        | npm + PyPI packages — API reference lives here                |
| `syntek-extensions`     | Paid extensions — developer guide lives here                  |
| `syntek-templates`      | Free templates — developer guide lives here                   |
| `syntek-premium`        | Paid templates — developer guide lives here                   |
| `syntek-store`          | Marketplace — listing requirements and submission guide here  |
| `syntek-ai`             | AI configs — public-facing portion documented here            |
| `syntek-infrastructure` | Hosts this docs site — NixOS deployment config lives there    |
| `syntek-licensing`      | License portal — billing and renewal docs live here           |
| `syntek-marketplace`    | Dev tooling — Syntek team Claude Code plugins (internal only) |
