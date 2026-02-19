# Massachusetts Forward Party Website

## Project Overview

Static website for the Massachusetts Forward Party, built with **Hugo** and
hosted on **GitHub Pages**. The site provides MA-specific messaging and content
while linking out to the national Forward Party's existing NationBuilder
infrastructure for all CRM-dependent actions (donations, signups, events,
volunteer management).

**Key constraint**: MA Forward Party has no budget. State law prevents the
national party from giving money to state parties. All CRM functionality is
handled by the national party's NationBuilder pages for free.

**iframe limitation**: NationBuilder pages set `X-Frame-Options: SAMEORIGIN`
and `Content-Security-Policy: frame-ancestors`, so forms cannot be embedded.
All CRM actions are link-outs that open in a new tab.

## Tech Stack

- **Hugo** — static site generator (no theme dependency; layouts are custom)
- **Bootstrap 4.6.2** — CSS framework via CDN
- **Google Fonts** — Inter (body) + League Gothic (headings)
- **Font Awesome 4.6.2** — icons via CDN
- **GitHub Actions** — deployment to GitHub Pages (`.github/workflows/hugo.yml`)

## NationBuilder Link-Out URLs

All configured centrally in `config.toml` under `[params]`:

## Design System — Forward Party Brand Colors

Colors extracted from `forwardparty.com` and `home.forwardparty.com/massachusetts`:

```
--purple:    #470D67    (primary brand color)
--navy:      #182742    (secondary dark)
--cyan:      #59D7EE    (bright accent, used for some buttons)
--red:       #CC3829    (warm CTA accent — donate button in nav, secondary buttons)
--orange:    #FF8200    (warm end of the signature gradient)
--bg-light:  #F3FAFA    (light section backgrounds)
```

### Signature Gradient

The Forward Party's signature visual is a dark left-to-right sweep:
**navy → purple → red → orange**. This matches the banner gradient on
`home.forwardparty.com/massachusetts`.

```css
--gradient-brand: linear-gradient(to right, #182742 0%, #470D67 35%, #CC3829 75%, #FF8200 100%);
```

Used as:
- 4px gradient bar below the nav and above the footer
- Bottom-edge accent on the hero section and page headers
- Top-edge accent on content cards

A darker variant (`--gradient-dark`) without the orange end is used for large
section backgrounds (hero, "Join" CTA, page headers):
```css
--gradient-dark: linear-gradient(to right, #182742 0%, #470D67 40%, #9B2335 75%, #CC3829 100%);
```

### Navigation

The navbar uses a **white background** with dark text, purple brand name, and
a red Donate button. This avoids clashing with the gradient bar beneath it.
Bootstrap class is `navbar-light` (not `navbar-dark`).

## Site Structure

```
config.toml                   — Hugo config, menu items, NationBuilder URLs
content/
  _index.md                   — Homepage front matter (hero text)
  about.md                    — About page (lorem ipsum placeholders)
  platform.md                 — Platform / policy positions (placeholders)
  get-involved.md             — Get involved page with NB link-out buttons
  news/_index.md              — News listing page (no posts yet)
layouts/
  _default/baseof.html        — Base template: nav, gradient bar, main, gradient bar, footer
  _default/single.html        — Single page: header + content + join CTA
  _default/list.html          — List page: header + content + child pages
  index.html                  — Homepage: hero, about, platform cards, join CTA, news, donate CTA
  partials/
    head.html                 — <head>: fonts, Bootstrap, Font Awesome, site CSS
    nav.html                  — White navbar with purple brand, red donate button
    footer.html               — Dark navy footer with 3 columns
    hero.html                 — Hero banner with gradient-dark background
    cta-join.html             — "Join the Movement" section (section-purple)
    cta-donate.html           — "Support Our Work" section (section-red)
    card.html                 — Reusable card (icon, title, text, optional link)
static/css/style.css          — All custom styles
.github/workflows/hugo.yml    — GitHub Pages deployment
```

## Content Status

All `.md` content files have real section headings reflecting actual Forward
Party themes, but body text is **lorem ipsum placeholders** clearly marked for
replacement with `<!-- TODO -->` comments.

## Local Development

```sh
hugo server    # preview at localhost:1313
hugo --minify  # production build to ./public/
```

## Design Decisions

- **Link-outs over iframes**: NationBuilder's CSP headers block iframe embedding.
  Simple link-outs to national NB pages are the $0 approach and a normal UX
  pattern (similar to ActBlue/WinRed for donations).
- **No Hugo theme**: All layouts are custom in `layouts/`. No external theme
  dependency to manage.
- **CDN-only dependencies**: Bootstrap, fonts, and icons are all loaded from
  CDNs. No npm/node build step required.
- **`relLangURL` for internal links**: The navbar brand link uses
  `{{ "" | relLangURL }}` so it works on both localhost and GitHub Pages
  subdirectory deployments.
- **`baseURL` is placeholder**: Set to `https://example.github.io/ma-forward-party/`.
  Must be updated when the actual GitHub repo / custom domain is configured.
