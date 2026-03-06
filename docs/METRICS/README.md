# Agent Metrics & Self-Learning System

**Last Updated**: 06/03/2026
**Version**: 1.0.0
**Maintained By**: Syntek Studio Development Team
**Language**: British English (en_GB)
**Timezone**: Europe/London

---

## Overview

This folder contains data for the Syntek Dev Suite self-learning system. Agent runs, feedback, and optimisations are recorded here so that the team's AI agents improve over time based on real usage patterns.

**All data in this folder is committed to Git.** The whole team benefits from every piece of feedback — improvements are shared across all developers working on this project.

---

## Folder Structure

```
docs/METRICS/
├── README.md              # This file
├── config.json            # System configuration
├── runs/                  # Individual agent run records
├── feedback/              # User feedback after agent runs
├── aggregates/            # Summarised data
│   ├── daily/             # Daily summaries
│   └── weekly/            # Weekly summaries
├── variants/              # A/B test prompt variants
├── optimisations/         # LLM-generated prompt improvements
│   ├── pending/           # Awaiting review or auto-apply
│   ├── applied/           # Applied to production prompts
│   └── rejected/          # Reviewed and rejected
└── templates/             # Analysis prompt templates
```

---

## Usage

### Recording Feedback

After an agent run, provide feedback using the learning commands:

```bash
/syntek-dev-suite:learning-feedback good
/syntek-dev-suite:learning-feedback bad The output didn't follow our docs style guide
```

### Reviewing Optimisations

```bash
/syntek-dev-suite:learning-optimise status
/syntek-dev-suite:learning-optimise analyse docs
/syntek-dev-suite:learning-optimise apply <id>
```

### A/B Tests

```bash
/syntek-dev-suite:learning-ab-test list
/syntek-dev-suite:learning-ab-test status docs
```

---

## Configuration

See `config.json` for the current system configuration, including whether auto-optimisation is enabled.
