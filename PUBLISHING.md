# Publishing a post (Pensacola Lending blog)

Live: https://cf9880.github.io/blog-pensacolalending/ (future: https://blog.pensacolalending.com/)

1. Create `content/posts/<slug>.md` (lowercase, hyphens, e.g. `content/posts/fha-loan-limits-2027.md`). The slug becomes the URL: `/posts/<slug>/`.
2. Start the file with front matter:

```yaml
---
title: "FHA Loan Limits for 2027"
date: 2026-10-20            # ISO date (or 2026-10-20T09:00:00-05:00); future dates are NOT published until then
description: "One or two sentences, <=160 chars, used for meta/OG description."
tags: ["fha", "pensacola"]
author: "Coastal Funding Corporation — Pensacola"
image: "/images/fha-2027.jpg"   # optional; put file in static/images/
draft: false                # true = not published
---
```
3. Write the body in Markdown below the front matter.
4. Commit to `main` (e.g. `gh api` contents PUT, or git push). GitHub Actions builds with Hugo and deploys in ~1 minute. Sitemap (`/sitemap.xml`), RSS (`/index.xml`) and schema update automatically.
5. Delete `content/posts/welcome-placeholder.md` once the first real post is live.

Compliance: keep NMLS 103035 references accurate; no rate guarantees.

## Switching to the custom domain
1. GoDaddy DNS for pensacolalending.com: add `CNAME` record, Name `blog`, Value `cf9880.github.io`, TTL 1 hour.
2. In `hugo.toml` set `baseURL = "https://blog.pensacolalending.com/"` and create `static/CNAME` containing `blog.pensacolalending.com`.
3. Repo Settings → Pages → Custom domain `blog.pensacolalending.com`, then enable Enforce HTTPS.
