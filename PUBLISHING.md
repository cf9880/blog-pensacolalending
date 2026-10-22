# Publishing a post (Pensacola Lending blog)

Live: https://blog.pensacolalending.com/ (old https://cf9880.github.io/blog-pensacolalending/ redirects here)

1. Create `content/posts/<slug>.md` (lowercase, hyphens, e.g. `content/posts/fha-loan-limits-2027.md`). The slug becomes the URL: `/posts/<slug>/`.
2. Start the file with front matter:

```yaml
---
title: "FHA Loan Limits for 2027"
date: 2026-10-20            # ISO date (or 2026-10-20T09:00:00-05:00); future dates are NOT published until then
description: "One or two sentences, <=160 chars, used for meta/OG description."
tags: ["fha", "pensacola"]
author: "Coastal Funding Corporation — Pensacola"
image: "images/fha-2027.jpg"     # REQUIRED; see "Images" below
image_alt: "Describe the photo"  # optional; defaults to the title
draft: false                # true = not published
---
```
3. Write the body in Markdown below the front matter.
4. Commit to `main` (e.g. `gh api` contents PUT, or git push). GitHub Actions builds with Hugo and deploys in ~1 minute. Sitemap (`/sitemap.xml`), RSS (`/index.xml`) and schema update automatically.
5. Delete `content/posts/welcome-placeholder.md` once the first real post is live.

Compliance: keep NMLS 103035 references accurate; no rate guarantees.

## Images (required on every post)
Every post must have an `image`. It is shown automatically as the featured image at the top of the post, as the thumbnail on the home and list pages, as the social share image (og:image) and in the BlogPosting schema. **Do not** also put the same image inline in the body, or it will be shown only once, inline.

Use one of these:
- **Shared folder (recommended):** commit the file to `static/images/<name>.jpg` and set `image: "images/<name>.jpg"` (no leading slash needed; a leading `/` also works).
- **Page bundle:** make the post a folder, `content/posts/<slug>/index.md` with the image next to it (`content/posts/<slug>/cover.jpg`), and set `image: "cover.jpg"`.
- **External URL:** `image: "https://..."` (must be a stable public URL).

Recommended: JPG or WebP, landscape 1200x630 or larger, under 500 KB, lowercase hyphenated file name. Commit the image in the same commit as the post.

## Custom domain (done Oct 22, 2026)
1. GoDaddy DNS for pensacolalending.com: add `CNAME` record, Name `blog`, Value `cf9880.github.io`, TTL 1 hour.
2. In `hugo.toml` set `baseURL = "https://blog.pensacolalending.com/"` and create `static/CNAME` containing `blog.pensacolalending.com`.
3. Repo Settings → Pages → Custom domain `blog.pensacolalending.com`, then enable Enforce HTTPS.

## FAQ block (optional, recommended for answer engines)
Add a `faq` list to the front matter. Each item has `q` (question) and `a` (short, plain answer, 1-3 sentences). The site shows it as a "Frequently Asked Questions" section at the end of the post and adds FAQPage schema automatically. If the post body already has its own `## Frequently Asked Questions` heading, only the schema is added (no duplicate section). Leave `faq` out and nothing is shown.

```yaml
faq:
  - q: "What credit score do I need for an FHA loan?"
    a: "Many FHA lenders look for a 580 or higher score for 3.5% down. Requirements vary by lender."
  - q: "How long does preapproval take?"
    a: "Often 1-3 business days once your documents are in."
```

## Author
Set `author:` to the exact `name` of a page in `content/authors/` so the byline links to that author page and the schema is correct. Current author names: `Coastal Funding Corporation — Pensacola`. If `author` is missing, the byline falls back to the business name. To add a new author, copy a file in `content/authors/`, set `title` and `name`, and use only verified facts in the bio.

```yaml
author: "Coastal Funding Corporation — Pensacola"
```

`static/llms.txt` summarizes this site for AI assistants. Update it if the business details change.
