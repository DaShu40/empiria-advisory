# EMPIRIA Advisory — Website

Static marketing site for EMPIRIA Advisory, built with **Astro** and deployed to **Cloudflare Pages**.

## Stack

| Layer | Choice |
|---|---|
| Framework | [Astro](https://astro.build) — static output, zero JS by default |
| Styling | Tailwind CSS v4 + scoped component styles |
| Fonts | Playfair Display (serif display), Inter (body), JetBrains Mono (labels/code) |
| Deployment | Cloudflare Pages |
| CI/CD | GitHub Actions → Cloudflare Wrangler |

## Local Development

```bash
npm install
npm run dev
```

Open http://localhost:4321

## Build

```bash
npm run build
# Output: /dist — ready to deploy
```

## Deploy to Cloudflare Pages

### Option A — GitHub Actions (recommended)

1. Push this repo to GitHub
2. In Cloudflare Dashboard → Pages → Create a project → Connect to Git
3. Set build settings:
   - **Build command**: `npm run build`
   - **Build output directory**: `dist`
4. Add GitHub Actions secrets:
   - `CLOUDFLARE_API_TOKEN` — from Cloudflare → My Profile → API Tokens → "Edit Cloudflare Workers" template
   - `CLOUDFLARE_ACCOUNT_ID` — from Cloudflare Dashboard URL or Overview page
5. Push to `main` — auto-deploys on every commit

### Option B — Direct Wrangler CLI

```bash
npm install -g wrangler
wrangler login
npm run build
wrangler pages deploy dist --project-name=empiria-advisory
```

### Option C — Cloudflare Dashboard drag-and-drop

```bash
npm run build
# Drag the /dist folder into Cloudflare Pages → Direct Upload
```

## Custom Domain

In Cloudflare Pages → your project → Custom domains → Add domain  
Point your DNS CNAME to `empiria-advisory.pages.dev`

## Environment

No environment variables required — this is a fully static site.

## Project Structure

```
src/
  layouts/
    Layout.astro       # HTML shell, fonts, meta
  pages/
    index.astro        # Homepage (all sections)
    privacy.astro      # Privacy Policy
    terms.astro        # Terms of Use
  styles/
    global.css         # Tailwind + CSS custom properties
public/
  favicon.svg
  _headers             # Cloudflare security headers
  _redirects           # Cloudflare URL redirects
.github/
  workflows/
    deploy.yml         # GitHub Actions CI/CD
```

## Design System

| Token | Value | Usage |
|---|---|---|
| `--slate-900` | `#0B0F19` | Page background |
| `--slate-800` | `#111827` | Section alternates |
| `--accent` | `#4A7FCC` | Interactive, labels |
| `--accent-warm` | `#C8A96E` | Reserved for future use |
| `--off-white` | `#F0EDE6` | Primary text |
| `--muted` | `#7A8EA8` | Body copy |

Display: **Playfair Display** — policy brief + law review authority  
Body: **Inter** — precision clarity  
Labels: **JetBrains Mono** — technical regulatory register

## Content Updates

All copy lives in `src/pages/index.astro`. Each section is clearly marked with comments (`═══ SECTION NAME ═══`). No CMS required for initial launch.

## Contact

advisor@empiriadvisory.com
