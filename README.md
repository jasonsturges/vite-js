# Vite JavaScript Template

![capture](https://github.com/user-attachments/assets/8fbbb328-e0a4-419b-8ec0-da644a0f7948)

Vite project setup that more closely resembles the TypeScript template, using a `src/` directory with minimal boilerplate.

This is a mutatiion of the `npm create vite` Vanilla JavaScript template, adding a vite config to define the root source path.

## Getting Started

Clone and initialize a fresh repo:

```sh
git clone https://github.com/jasonsturges/vite-js-template.git
cd vite-js-template
rm -rf .git
git init
git add -A
git commit -m "Initial commit"
```

### GitHub Actions

Example workflow action to deploy to GitHub pages.

Go to repo Settings, Pages, and set Build and Deployment source to "GitHub Actions".

Add the following action (file: .github/workflows/static.yml)

```yaml
# Workflow for deploying static content to GitHub Pages
name: Deploy static content to Pages

on:
  # Runs on pushes targeting the default branch
  push:
    branches: ["main"]

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# Sets permissions of the GITHUB_TOKEN to allow deployment to GitHub Pages
permissions:
  contents: read
  pages: write
  id-token: write

# Allow only one concurrent deployment, skipping runs queued between the run in-progress and latest queued.
# However, do NOT cancel in-progress runs as we want to allow these production deployments to complete.
concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup Node
        uses: actions/setup-node@v3
        with:
          node-version: 20
          cache: "npm"

      - name: Install dependencies
        run: npm ci

      - name: Build
        run: npm run build

      - name: Setup Pages
        uses: actions/configure-pages@v5

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          # Upload `dist` folder
          path: "./dist"

      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4

```
