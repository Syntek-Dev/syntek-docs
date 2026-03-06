---
description: Build documentation for staging deployment
usage: /staging
---

Build the documentation site for staging review.

**Run:**
```bash
npm run build
npm run serve    # Preview the built site locally before deploy
```

This will:
1. Run a full Docusaurus build
2. Output the static site to `build/`
3. Serve the built site at http://localhost:3000 for review

**Deployment:**
Merging to the `staging` branch triggers an automatic deployment to the staging environment via CI/CD. You do not need to deploy manually.

$ARGUMENTS
