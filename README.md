# RKR Networks Blog

Source for **https://blog.rkr-networks.com**, built with [Hugo](https://gohugo.io) (extended, v0.168.0) and the
[PaperMod](https://github.com/adityatelange/hugo-PaperMod) theme (vendored in `themes/PaperMod`, MIT license kept).
Every push to `main` builds and deploys to GitHub Pages via `.github/workflows/hugo.yml`.

Main site: https://www.rkr-networks.com · Contact: sales@rkr-networks.com

## This repo is public

Marketing content only. No internal/product-internal details, no pricing, nothing confidential.
Terminology: say "synthetic twin" (never the other common "… twin" phrase).

## Writing a post

Posts are Markdown files in `content/posts/`. Create one with:

```sh
hugo new content posts/my-post-slug.md
```

or add the file by hand with this front matter:

```yaml
---
title: "Post title"
date: 2026-10-26
description: "One or two sentences; used as the page's meta description and social-card text."
tags: ["networking", "operations"]
draft: false   # true = not published
---
```

Optional: `cover.image` (path under `static/`) for a social-card image.

## Local preview

```sh
hugo server -D      # http://localhost:1313, includes drafts
hugo --minify       # production build into public/ (git-ignored)
```

## Custom domain

`static/CNAME` contains `blog.rkr-networks.com`. DNS needs `CNAME blog -> <owner>.github.io`;
after DNS resolves, enable **Settings > Pages > Enforce HTTPS**.
