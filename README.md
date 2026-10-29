# JAHID / DEV — React + Vite Portfolio

A responsive, dark developer portfolio with lime-green accents, subtle motion, project cards, skills, education, social links, and a contact section.

## Requirements
- Node.js 18+ (Node.js 20+ recommended)
- npm

## Run locally
```bash
npm install
npm run dev
```
Open the local URL Vite prints in your terminal (usually `http://localhost:5173`).

## Customize before publishing
Open `src/main.jsx` and update:
- `email = 'hello@example.com'` with your real email address.
- Project descriptions, technology tags, and repository links in the `projects` array.
- Skill names and descriptions in the `skills` array.
- LinkedIn / GitHub URLs if needed.
- The current avatar is an initials-based placeholder (`J.`). Replace the avatar markup with an image when you have a profile photo.

The page intentionally describes project concepts without claiming unverified employment or experience.

## Build and preview
```bash
npm run build
npm run preview
```

## Deploy to GitHub Pages

### Option A — recommended: GitHub Actions
1. Create a GitHub repository named `jahid-portfolio` (or any name you prefer).
2. Push this project to the repository.
3. On GitHub, open **Settings → Pages**.
4. Under **Build and deployment**, choose **GitHub Actions**.
5. Add the workflow below at `.github/workflows/deploy.yml`, commit and push it.
6. Wait for the workflow to finish. Your site URL will be shown in **Settings → Pages**.

Create `.github/workflows/deploy.yml` with:

```yaml
name: Deploy portfolio to GitHub Pages

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
  cancel-in-progress: true

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      - name: Setup Node
        uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: npm
      - run: npm install
      - run: npm run build
      - name: Upload Pages artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: dist
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

This project uses `base: './'` in `vite.config.js`, so Vite emits relative asset paths suitable for a GitHub Pages project site and the repository name does not need to be hard-coded.

### Option B — deploy from your computer
1. Run `npm install`.
2. Add and commit your code to a GitHub repository.
3. Run `npm run deploy`.
4. In GitHub **Settings → Pages**, choose the `gh-pages` branch and `/ (root)` folder if it is not automatically selected.

## Notes
- Google Fonts require an internet connection; fallback fonts are configured.
- The email button copies the configured email to the clipboard. If clipboard access is blocked, it opens a mail draft.
- This is a static frontend portfolio; no backend is required.
