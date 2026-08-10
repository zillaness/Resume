# Portfolio site

Static portfolio published to GitHub Pages. Everything inside `site/` is the published site; the repo root holds only config.

```
site/
  index.html    <- your portfolio page goes here
  assets/       <- images, CSS, fonts, PDFs
  .nojekyll     <- stops Pages from running Jekyll over the files
.github/workflows/deploy-pages.yml
```

## One-time setup

In the repo: **Settings → Pages → Build and deployment → Source: GitHub Actions**.

Without this the workflow will fail at the deploy step with a "Pages not enabled" error.

## Publishing

Put your HTML at `site/index.html` and push. The workflow uploads the whole `site/` directory and deploys it. The live URL shows up in the workflow run summary and under Settings → Pages.

Via the browser: open `site/`, use **Add file → Upload files**, drag the HTML in named `index.html`, commit.

Via git:

```sh
cp /path/to/your-portfolio.html site/index.html
git add site && git commit -m "Add portfolio page"
git push
```

Relative paths behave the same as they do locally — `<img src="assets/headshot.jpg">` resolves as long as the file sits at `site/assets/headshot.jpg`. Use relative paths, not paths starting with `/`, since the site is served from a subdirectory (`/Resume/`) unless you attach a custom domain.

## Size limits

| Limit | Value |
| --- | --- |
| Single file | 100 MB hard block (warning over 50 MB) |
| Published site | 1 GB |
| Recommended page weight | under 10 MB |

A "large" HTML file is usually base64 data URIs. Extract the media into `site/assets/` and reference it by filename — it stays under the limits and the page loads much faster. Git LFS is checked out by the workflow if you need it, but Pages serves LFS files poorly, so treat it as a last resort.

## Custom domain

Add a `site/CNAME` file containing the bare domain (e.g. `example.com`), then point DNS at GitHub Pages.
