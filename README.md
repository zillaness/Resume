# Portfolio site

Samuel Cao's portfolio, published to GitHub Pages.

**Live at <https://zillaness.github.io/Resume/portfolio/>**

`https://zillaness.github.io/Resume/` redirects there, so either link works.

```
site/                     <- everything in here is published
  index.html              <- redirect to portfolio/
  .nojekyll               <- stops Pages from running Jekyll over the files
  portfolio/
    index.html            <- the portfolio page
    support.js
    _ds/                  <- design-system tokens and styles
    uploads/              <- images and media (~159 MB)
    assets/
.github/workflows/deploy-pages.yml
```

## How the URL is built

GitHub Pages serves a project site at `https://<user>.github.io/<repo>/`, so `Resume` is the repo name and can only be changed by renaming the repo. Everything after that is a directory inside `site/` — which is why the page lives in `site/portfolio/`.

## Publishing

Push to `main`. The workflow uploads the whole `site/` directory and deploys it; the live URL appears in the run summary and under Settings → Pages. A deploy takes about a minute.

Use relative paths in the HTML (`uploads/photo.jpg`, not `/uploads/photo.jpg`) — the site is served from a subdirectory, so absolute paths break.

## Pages setup

Already configured: **Settings → Pages → Build and deployment → Source: GitHub Actions**. If the deploy step ever fails with "Pages not enabled", that setting was reset.

## Size limits

| Limit | Value |
| --- | --- |
| Single file | 100 MB hard block (warning over 50 MB) |
| Published site | 1 GB |
| Recommended page weight | under 10 MB |

The `uploads/` directory is ~159 MB — well under the site cap, but heavy for a first visit. Compressing the largest images and GIFs is the cheapest speed win available.

## Custom domain

Add a `site/CNAME` file containing the bare domain (e.g. `example.com`), then point DNS at GitHub Pages. That would serve the site at the domain root and make the `/Resume/` path disappear.
