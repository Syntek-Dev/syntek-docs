# Syntek Docs

---

The canonical documentation source for the entire Syntek ecosystem. Every public-facing guide, API reference, developer tutorial, and changelog for all Syntek products lives here. If information about a Syntek product does not appear in this repository, it does not ship.

---

## Table of Contents

1. [What This Repository Is](#what-this-repository-is)
2. [What It Contains](#what-it-contains)
3. [The Syntek Ecosystem](#the-syntek-ecosystem)
4. [Getting Started](#getting-started)
5. [Development Commands](#development-commands)
6. [Deployment](#deployment)
7. [Contributing Documentation](#contributing-documentation)
8. [Documentation Standards](#documentation-standards)
9. [Key Locations](#key-locations)
10. [Related Repositories](#related-repositories)

---

## What This Repository Is

`syntek-docs` is a [Docusaurus](https://docusaurus.io/) static site — Markdown source files rendered into a documentation website deployed at `syntekstudio.com/docs`.

It is **not** a code repository. There is no application logic, no API, and no database. The entire site is built from Markdown (and MDX where interactive components are needed) and served as static HTML via `syntek-infrastructure`.

This repository is the **single source of truth** for:

- How to self-host `syntek-platform`
- How to build extensions, templates, and modules
- What every public API does and how to call it
- How licensing, billing, and renewals work
- How to use every licenseable part of the ecosystem — `syntek-modules`, `syntek-extensions`, `syntek-templates`, and `syntek-premium`
- How to build custom AI agents using `syntek-ai` — from starter chatbots for client sites to fully configured customer-facing assistants
- How to publish and sell your own agents, extensions, templates, and modules in `syntek-store` (or list them for free)
- How to submit products to the Syntek Store
- Changelogs for every Syntek product

---

## What It Contains

| Section                            | Audience                          | Description                                                           |
| ---------------------------------- | --------------------------------- | --------------------------------------------------------------------- |
| Getting Started                    | Platform developers               | Self-hosting `syntek-platform` from scratch                           |
| Module API Reference               | Extension and template developers | Full API docs for all `syntek-modules` npm and PyPI packages          |
| Extension Development Guide        | Third-party developers            | Building, testing, and submitting extensions to `syntek-store`        |
| Template Development Guide         | Third-party developers            | Building free and premium templates; manifest format; token overrides |
| AI Reference                       | Platform developers               | Public-facing portion of `syntek-ai` task and prompt reference        |
| Licensing and Billing              | All developers and Syntek clients | License model, renewals, developer portal, non-profit pricing         |
| Changelogs                         | All users                         | Per-product version history                                           |
| Architecture Plans (`docs/PLANS/`) | Syntek development team           | Technical decision records and feature design documents               |

---

## The Syntek Ecosystem

`syntek-docs` sits at the centre of the Syntek ecosystem. Every other repository links to this one; this one depends on nothing.

```
Syntek Organisation
│
├── syntek-infrastructure     # NixOS / Hetzner — hosts Syntek-managed client services only
│
├── syntek-modules            # Foundation: reusable npm + Python packages (Apache 2.0)
│   ├── syntek-platform       # Free, self-hostable CMS core (AGPL v3)
│   │   ├── syntek-extensions # Paid add-ons for the platform (commercial licence)
│   │   ├── syntek-templates  # Free starter templates
│   │   └── syntek-premium    # Paid premium starter templates
│   └── syntek-saas           # Internal: Syntek-owned SaaS UI products
│
├── syntek-ai                 # Internal: Prompt Management, Tasks & Rules (YAML/MD)
├── syntek-licensing          # Licence management UI + PostgreSQL (Rust key server in infra)
├── syntek-store              # Third-party developer marketplace
│
├── syntek-docs               # ← This repository — all documentation
│
└── syntek-marketplace        # Internal: Claude Code plugins for Syntek development workflow
```

For the full architecture description — how each repository works, how they relate, and the guiding principles — see [`docs/PLANS/SYNTEK-ARCHITECTURE.md`](docs/PLANS/SYNTEK-ARCHITECTURE.md).

---

## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) 20 or later
- npm (bundled with Node.js)

### Install and run locally

```bash
# Clone the repository
git clone <repository-url>
cd syntek-docs

# Install dependencies
npm install

# Start the local dev server with hot reload
npm start
```

The site will be available at `http://localhost:3000`.

---

## Development Commands

```bash
# Install dependencies
npm install

# Start local dev server (hot reload)
npm start                     # http://localhost:3000

# Build static site
npm run build

# Serve the built static site locally
npm run serve

# Check for broken links
npm run check-links

# Lint Markdown files
npm run lint:md
```

---

## Deployment

The built static site is deployed to `syntek-infrastructure` (Hetzner) via Cloudflare Tunnels.

| Environment | Trigger                   | URL                     |
| ----------- | ------------------------- | ----------------------- |
| Staging     | Merge to `staging` branch | Staging subdomain       |
| Production  | Merge to `main` branch    | `syntekstudio.com/docs` |

Deployment is fully automated via the CI/CD pipeline and NixOS service definitions in `syntek-infrastructure`. No manual server access is required or permitted.

---

## Contributing Documentation

### Who contributes here

- **Syntek development team** — platform core, modules, extensions, infrastructure runbooks
- **Third-party extension and template authors** — required to submit documentation before a product is listed in `syntek-store`
- **Syntek clients** — may raise issues or suggest corrections via pull request

### Rules for contributions

- **No feature ships without docs.** Every public-facing feature must have a corresponding entry here before it is released.
- **API changes require a docs update in the same PR.** A pull request that adds or modifies a public API must include the documentation change in the same diff — not as a follow-up.
- **Products must be documented before listing.** Extension and template authors must submit documentation to this repository (or host it within their `syntek-store` listing) before their product is approved for listing.
- **All code examples must work.** Every command and code snippet must be tested and correct at the time of submission.
- **All links must resolve.** Verify all links before opening a pull request.

### Adding a new document

1. Create the file in the correct section folder using `UPPER-KEBAB-CASE.md` naming
2. Add the metadata header (see [Documentation Standards](#documentation-standards))
3. Add it to `sidebars.js`
4. Link to it from the relevant parent document or section index
5. Update the section `README.md` if one exists

### Updating an existing document

1. Update the `**Last Updated**` date in the metadata header
2. Keep `**Version**` in sync with the relevant product version
3. Do not delete content without setting up a redirect for the old URL

---

## Documentation Standards

### File naming

| Type               | Convention             | Example                               |
| ------------------ | ---------------------- | ------------------------------------- |
| All doc files      | `UPPER-KEBAB-CASE.md`  | `GETTING-STARTED.md`                  |
| Plan/decision docs | `PLAN-FEATURE-NAME.md` | `PLAN-SYNTEK-AI-AND-MULTI-TENANCY.md` |

### Metadata header

Every `.md` file must open with:

```markdown
# Document Title

**Last Updated**: DD/MM/YYYY
**Version**: x.y.z
**Maintained By**: Syntek Studio Development Team
**Language**: British English (en_GB)
**Timezone**: Europe/London
```

### Language and style

- **British English** throughout — colour not color, licence (noun) not license, organisation not organization
- Date format: `DD/MM/YYYY`
- Time format: 24-hour clock (`14:30`)
- Currency: GBP (£)
- Active voice; avoid passive where possible
- One idea per paragraph
- Tables for comparisons and reference data
- Code blocks for all commands, file paths, and code samples

### Document structure

Every document must have:

1. Metadata header
2. Table of contents (for documents longer than approximately 200 lines)
3. Clear `##` section headings
4. No orphaned content — every section belongs under a heading

---

## Key Locations

| Path                                | Purpose                                                |
| ----------------------------------- | ------------------------------------------------------ |
| `docs/PLANS/`                       | Architecture plans and technical decision documents    |
| `docs/PLANS/SYNTEK-ARCHITECTURE.md` | Full ecosystem architecture overview (canonical)       |
| `docs/METRICS/`                     | Self-learning system data (agent metrics and feedback) |
| `.claude/CLAUDE.md`                 | Project context for Claude agents                      |
| `.claude/CODING-PRINCIPLES.md`      | Rob Pike and Linus Torvalds coding rules               |
| `.claude/SYNTEK-GUIDE.md`           | Full Syntek Dev Suite plugin usage guide               |
| `.claude/plugins/`                  | Python plugin tools for agent automation               |
| `.claude/commands/`                 | Project-specific slash commands                        |

---

## Related Repositories

| Repository              | Relationship                                                       |
| ----------------------- | ------------------------------------------------------------------ |
| `syntek-platform`       | Core platform — PRs must include a docs update                     |
| `syntek-modules`        | npm and PyPI packages — API reference lives here                   |
| `syntek-extensions`     | Paid extensions — developer guide lives here                       |
| `syntek-templates`      | Free templates — developer guide lives here                        |
| `syntek-premium`        | Paid templates — developer guide lives here                        |
| `syntek-store`          | Marketplace — listing requirements and submission guide lives here |
| `syntek-ai`             | AI configs — public-facing portion documented here                 |
| `syntek-infrastructure` | Hosts this docs site — NixOS deployment config lives there         |
| `syntek-licensing`      | Licence portal — billing and renewal docs live here                |
| `syntek-marketplace`    | Dev tooling — Syntek team Claude Code plugins (internal only)      |
