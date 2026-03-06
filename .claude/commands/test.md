---
description: Run documentation checks (links, markdown lint)
usage: /test
---

Run all documentation quality checks.

**Commands:**
```bash
npm run check-links    # Check for broken internal and external links
npm run lint:md        # Lint markdown files for formatting issues
npm run build          # Full build test (catches rendering errors)
```

**Run all checks:**
```bash
npm run check-links && npm run lint:md && npm run build
```

$ARGUMENTS
