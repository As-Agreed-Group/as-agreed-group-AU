# Jekyll + GitHub Pages setup

## What's been added

- `_config.yml`, `Gemfile` — Jekyll config, using the `github-pages` gem so the build matches what GitHub actually runs
- `_layouts/default.html` — shared header/nav/footer, pulled out of the old single index.html
- `_layouts/post.html` — template for individual blog posts
- `assets/css/style.css` — all the site's styling, extracted from the old inline `<style>` block, plus new blog styles in the same ledger/stamp look
- `index.html` — now just front matter + the homepage content, using the default layout
- `blog/index.html` — the blog listing page, at `/blog/`
- `_posts/2026-08-07-why-you-need-an-operations-partner-not-just-a-bookkeeper.md` — your first post
- `CNAME` — set to `asagreed.au` for the custom domain
- `.gitignore` — excludes the Jekyll build output and local cache files

New posts go in `_posts/` as `YYYY-MM-DD-title.md` with this front matter:

```
---
layout: post
title: "Post title"
date: 2026-08-07
description: "One or two sentences for the blog list and SEO."
---
```

## Test it locally (optional, needs Ruby + Bundler on your machine)

```
bundle install
bundle exec jekyll serve
```

Then open `http://localhost:4000`.

## Push to GitHub Pages

1. Create a new GitHub repo (public, or private on a paid plan)
2. From this folder:
   ```
   git init
   git add .
   git commit -m "Add Jekyll and blog"
   git branch -M main
   git remote add origin https://github.com/<your-username>/<repo-name>.git
   git push -u origin main
   ```
3. In the repo, go to Settings > Pages
4. Under "Build and deployment", set Source to "Deploy from a branch", branch `main`, folder `/ (root)`
5. Under "Custom domain", enter `asagreed.au` and save (this re-checks the `CNAME` file already in the repo)

## DNS (at your domain registrar)

Point the apex domain to GitHub Pages with four A records:

| Type | Host | Value |
|---|---|---|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |

And point `www` at your GitHub Pages default domain:

| Type | Host | Value |
|---|---|---|
| CNAME | www | `<your-username>.github.io` |

DNS changes can take a few hours to propagate. Once GitHub sees the DNS resolve correctly, tick "Enforce HTTPS" in the Pages settings for a certificate.

Source: [GitHub Docs — managing a custom domain](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)
