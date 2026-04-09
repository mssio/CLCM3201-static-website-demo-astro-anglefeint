<h1 align="center">Anglefeint</h1>
<p align="center">A cinematic, multi-atmosphere Astro theme for personal publishing.</p>

<p align="center">
  <a href="https://demo.anglefeint.com/">Live Demo</a>
  ·
  <a href="https://github.com/anglefeint/astro-theme-anglefeint">Repository</a>
  ·
  <a href="ASTRO_THEME_LISTING.md">Theme Listing</a>
</p>

<p align="center">
  <img alt="Astro" src="https://img.shields.io/badge/Astro-6.1.3-BC52EE?logo=astro&logoColor=white" />
  <img alt="Node" src="https://img.shields.io/badge/Node.js-22.12%2B-339933?logo=node.js&logoColor=white" />
  <img alt="Locales" src="https://img.shields.io/badge/i18n-en%20%7C%20ja%20%7C%20ko%20%7C%20es%20%7C%20zh-0A7EA4" />
  <img alt="Deployment" src="https://img.shields.io/badge/Deploy-Cloudflare%20Workers-F38020?logo=cloudflare&logoColor=white" />
  <img alt="License" src="https://img.shields.io/badge/License-MIT-2EA043" />
</p>

## Template Install

```bash
pnpm create astro@latest -- --template anglefeint/astro-theme-anglefeint#starter
```

Or with `pnpm`:

```bash
pnpm create astro@latest --template anglefeint/astro-theme-anglefeint#starter
```

## Requirements

- Node.js `22.12.0+` (LTS recommended)
- Package manager: `pnpm`, `pnpm`, `yarn`, or `bun`

## Quick Start

```bash
pnpm install
pnpm dev
```

Build and preview:

```bash
pnpm build
pnpm preview
```

Quality commands:

```bash
pnpm lint
pnpm format:check
pnpm e2e:install
pnpm e2e
```

With `pnpm`:

```bash
pnpm install
pnpm dev
pnpm build
pnpm preview
```

## Upgrade Theme

For package updates in projects created from `#starter`, start with:

```bash
pnpm update @anglefeint/astro-theme
pnpm install
pnpm doctor
# if doctor reports adapter drift:
# pnpm sync-adapters
pnpm check
pnpm build
```

If release notes mention starter-side contract changes, pull those changes into your project as well. `pnpm update` alone only updates the published package.

If your custom code still imports `src/consts` or `@anglefeint/astro-theme/consts`, migrate to `src/config/site.ts`.

For Astro major-version migrations, follow the official Astro guide first:

- https://docs.astro.build/en/guides/upgrade-to/
- then re-run this project's `pnpm check` and `pnpm build`.

## Create New Post

Create the same slug in all configured locales:

```bash
pnpm new-post -- my-first-post
```

Slug rule: use lowercase letters, numbers, and hyphens only (example: `my-first-post`).
If default covers exist in `src/assets/blog/default-covers/`, a stable cover is auto-assigned by slug hash (you can replace `heroImage` later).
Optional locale override:

```bash
pnpm new-post -- my-first-post --locales en,fr
# or
ANGLEFEINT_LOCALES=en,fr pnpm new-post -- my-first-post
```

How URL works:

- File: `src/content/blog/<locale>/my-first-post.md`
- URL: `/<locale>/blog/my-first-post/`
- Blog list: `/<locale>/blog/`
- You do not need to add routes manually. Astro generates them from content files at build time.

## Create New Page

`new-post` creates blog content only. For custom pages, use:

```bash
pnpm new-page -- projects --theme base
```

Available themes: `base`, `ai`, `cyber`, `hacker`, `matrix`.
The command creates `src/pages/[lang]/projects.astro` with locale routes via `getStaticPaths()`.
Slug rule: lowercase letters, numbers, and hyphens only; nested paths are allowed (example: `projects/labs`). `_` and uppercase are invalid.

Examples:

```bash
pnpm new-page -- projects --theme base
pnpm new-page -- projects --theme ai
pnpm new-page -- projects --theme cyber
pnpm new-page -- projects --theme hacker
pnpm new-page -- projects --theme matrix
```

## Languages

English (this file) · [简体中文](README.zh-CN.md) · [日本語](README.ja.md) · [Español](README.es.md) · [한국어](README.ko.md)

## Preview

| Home                                                           | Blog List                                                                |
| -------------------------------------------------------------- | ------------------------------------------------------------------------ |
| ![Home preview](public/images/theme-previews/preview-home.png) | ![Blog list preview](public/images/theme-previews/preview-blog-list.png) |

| Blog Post                                                                     |
| ----------------------------------------------------------------------------- |
| ![Blog post preview](public/images/theme-previews/preview-blog-post-open.png) |

| About                                                            |
| ---------------------------------------------------------------- |
| ![About preview](public/images/theme-previews/preview-about.png) |

## Route Atmospheres

- `/<default-locale>/` (with `/` redirecting there by default): Matrix-inspired terminal landing
- `/:lang/blog`: cyberpunk archive mood
- `/:lang/blog/[slug]`: AI-interface reading layout
- `/:lang/about`: optional hacker-style profile page

## Theme Naming Contract

- Theme variants: `base`, `ai`, `cyber`, `hacker`, `matrix`
- Internal selectors/scripts use aligned prefixes: `ai-*`, `cyber-*`, `hacker-*`
- Core composition follows: `ThemeFrame -> Shell -> Layout -> Page`

## Features

- Astro 6 static output
- Markdown + MDX content collections
- Starter ships sample locales: `en`, `ja`, `ko`, `es`, `zh`
- Per-locale RSS feeds
- Sitemap + robots support
- Config-driven customization
- Sticky footer (viewport-bottom on short pages)

## Theme Setup

1. Copy `.env.example` to `.env` and set site identity variables.
2. Edit `src/site.config.ts`:
   - `site.title`, `site.description`, `site.url`, `site.author`, `site.tagline` for site identity and default metadata
   - `i18n.defaultLocale` to set the canonical root locale
   - `i18n.routing.defaultLocalePrefix` to choose whether the default locale lives at `/<default-locale>/` (default) or `/`
   - `i18n.locales` to add/remove supported locales from a single source
   - `i18n.locales.<code>.messages` for localized UI copy overrides
   - `i18n.locales.<code>.site.hero` for localized home hero copy
   - `i18n.locales.<code>.about` for localized About content/runtime text
   - `social.links` for header/footer links
   - `theme.enableAboutPage` for About route/nav toggle
   - `theme.effects.enableRedQueen` to enable/disable the post-side monitor effect
   - `theme.comments` to enable and configure Giscus (core IDs + behavior options)
3. Replace starter posts in `src/content/blog/<locale>/`.
4. Set your real site URL (`PUBLIC_SITE_URL` or `src/site.config.ts`) before production deploy.

Notes:

- `site.description` is the site-level default description. The home page uses localized `messages.siteDescription` when provided and falls back to `site.description`.
- Locale metadata currently supports `label`, `hreflang`, `ogLocale`, `enabled`, and `fallback`.

### Optional: Giscus Comments

Comments are disabled by default. To enable:

1. In `src/site.config.ts`, set `theme.comments.enabled = true`.
2. Fill:
   - `theme.comments.repo`
   - `theme.comments.repoId`
   - `theme.comments.category`
   - `theme.comments.categoryId`
3. Optionally customize:
   - `theme.comments.mapping`
   - `theme.comments.term` (required when `mapping = "specific"`)
   - `theme.comments.number` (required when `mapping = "number"`)
   - `theme.comments.strict`
   - `theme.comments.reactionsEnabled`
   - `theme.comments.emitMetadata`
   - `theme.comments.inputPosition` (`top` or `bottom`)
   - `theme.comments.theme`
   - `theme.comments.lang`
   - `theme.comments.loading`
   - `theme.comments.crossorigin`

If these required fields are missing, the comments block is not rendered.

## Configuration Surface

- Single entry: `src/site.config.ts`
- Adapters (do not edit directly): `src/config/site.ts`, `src/config/theme.ts`, `src/config/about.ts`, `src/config/social.ts`
- Environment override supported: `PUBLIC_*` vars for site identity

## Docs

- Architecture: `docs/ARCHITECTURE.md`
- Visual systems: `docs/VISUAL_SYSTEMS.md`
- Submission checklist: `docs/THEME_SUBMISSION_CHECKLIST.md`
- Theme listing draft: `ASTRO_THEME_LISTING.md`
- Upgrading guide: `UPGRADING.md`
- Changelog: `CHANGELOG.md`

## Credits

- Parts of the base typography CSS are adapted from Bear Blog defaults (MIT).  
  Source note is preserved in `src/styles/global.css`.

## Deploy to GitHub Pages

### Step 1: Set your site URL

Open `src/site.config.ts` and set `site.url` to your GitHub Pages URL:

```
https://<your-github-username>.github.io/<your-repo-name>
```

If your repo is named `<username>.github.io`, the URL is just `https://<username>.github.io`.

### Step 2: Create the GitHub Actions workflow

Create `.github/workflows/deploy.yml` with the following content:

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [main]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: pages
  cancel-in-progress: false

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 22
          cache: npm
      - run: npm install
      - run: npm run build
        env:
          PUBLIC_SITE_URL: https://<your-github-username>.github.io/<your-repo-name>
      - uses: actions/upload-pages-artifact@v3
        with:
          path: ./dist

  deploy:
    needs: build
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - uses: actions/deploy-pages@v4
        id: deployment
```

Replace `<your-github-username>` and `<your-repo-name>` with your actual values.

### Step 3: Enable GitHub Pages in repository settings

1. Go to your GitHub repository
2. Click **Settings** → **Pages**
3. Under **Build and deployment**, set **Source** to **GitHub Actions**
4. Save

### Step 4: Push and deploy

```bash
git add .github/workflows/deploy.yml
git commit -m "Add GitHub Pages deployment workflow"
git push
```

The workflow triggers automatically on every push to `main`. Monitor progress under the **Actions** tab.

### Step 5: Verify

Once the workflow completes, your site will be live at:

```
https://<your-github-username>.github.io/<your-repo-name>
```

## License

MIT License. See `LICENSE`.
