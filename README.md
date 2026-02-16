# Massachusetts Forward Party Website

Static website for the Massachusetts Forward Party, built with [Hugo](https://gohugo.io/) and hosted on GitHub Pages.

## Architecture

This is a free static site that links out to the national Forward Party's NationBuilder infrastructure for all CRM-dependent actions (donations, signups, events, volunteer management). Design is inspired by the "Tolerance" theme used by most state Forward Party NationBuilder sites.

### What this site handles

- MA-specific messaging, branding, and identity
- Platform / policy positions
- News and announcements
- General "About" and "Get Involved" content

### What links out to NationBuilder (free, already exists)

| Action | URL |
|---|---|
| Join / Sign Up | home.forwardparty.com/massachusetts |
| Donate | home.forwardparty.com/donate_massachusetts |
| Events | home.forwardparty.com/ma_event_calendar |
| Volunteer | home.forwardparty.com/massachusetts_hub |
| Run for Office | home.forwardparty.com/ma_candidate_application |

## Local Development

### Prerequisites

- [Hugo](https://gohugo.io/installation/) (extended edition not required)

### Run locally

```sh
hugo server
```

Open http://localhost:1313 in your browser.

### Build for production

```sh
hugo --minify
```

Output goes to `./public/`.

## Deployment

The site deploys automatically to GitHub Pages via GitHub Actions when changes are pushed to the `main` branch. See `.github/workflows/hugo.yml`.

### Setup

1. Push this repo to GitHub
2. Go to **Settings > Pages** and set Source to **GitHub Actions**
3. Update `baseURL` in `config.toml` to match your GitHub Pages URL
4. Push to `main` — the site will build and deploy automatically

## Customization

### Content

Edit the Markdown files in `content/`:

- `content/_index.md` — Homepage front matter
- `content/about.md` — About page
- `content/platform.md` — Platform / policy positions
- `content/get-involved.md` — How to get involved
- `content/news/` — Add news posts as individual `.md` files

### Adding a news post

Create a new file in `content/news/`, e.g. `content/news/2026-03-01-launch.md`:

```markdown
---
title: "Massachusetts Forward Party Website Launches"
date: 2026-03-01
description: "We're excited to announce the launch of our new website."
---

Post content goes here.
```

### NationBuilder URLs

All NationBuilder link-out URLs are configured in `config.toml` under `[params]`. Update them there to change where buttons link to.

### Styling

Custom CSS is in `static/css/style.css`. The site uses Bootstrap 4 via CDN.

### Logo / Images

Place images in `static/images/`. Reference them in templates or content as `/images/filename.png`.
