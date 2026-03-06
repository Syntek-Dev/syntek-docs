---
description: Build documentation for production deployment
usage: /production
---

Build the documentation site for production.

**Pre-flight checklist:**
- [ ] All links verified (`npm run check-links`)
- [ ] Markdown linting passed (`npm run lint:md`)
- [ ] Build succeeds locally (`npm run build`)
- [ ] Staging reviewed and approved

**Build:**
```bash
npm run build
```

**Deployment:**
Merging to `main` triggers an automatic production deployment via CI/CD to `syntek-infrastructure` (Hetzner). The site is served via Cloudflare Tunnels — no manual server access required or permitted.

**Infrastructure changes** (if needed) are managed in `syntek-infrastructure`, not here.

$ARGUMENTS
