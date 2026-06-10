# abavus-website

This is the official marketing website for [Abavus](https://github.com/toschdev/abavus) — Cryptographic identity and provenance for AI agents.

## Contents

- `index.html` — The main landing page
- `style.css` — Styles (dark, modern, self-contained)
- `.nojekyll` — Prevents GitHub Pages from running Jekyll

## Local Development

Simply open the site in your browser:

```bash
open index.html
# or
python3 -m http.server 8000   # then visit http://localhost:8000
```

## Deployment

This site is designed to be deployed with **GitHub Pages**.

### Recommended setup (GitHub Pages)

1. Create a new repository (e.g. `abavus-website`).
2. Push this folder as the root of the new repo.
3. Go to **Settings → Pages**.
4. Set **Source** to **GitHub Actions** (or "Deploy from a branch" → main, root).
5. The site will be available at:
   - `https://<your-username>.github.io/abavus-website/`
   - Or connect a custom domain (e.g. `abavus.ai`).

A simple GitHub Actions workflow for automatic deployment is recommended:

```yaml
# .github/workflows/deploy.yml
name: Deploy to GitHub Pages

on:
  push:
    branches: [ main ]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/configure-pages@v4
      - uses: actions/upload-pages-artifact@v3
        with:
          path: '.'
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - uses: actions/deploy-pages@v4
```

## License

The Abavus project is licensed under AGPL-3.0.  
This website (marketing material) may be used under the same terms or more permissively for promotional purposes.

## Related

- Main project: https://github.com/toschdev/abavus
- Live Abavus site (once deployed): https://abavus.ai (planned)
