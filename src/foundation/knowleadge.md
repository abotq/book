# Knowleadge base

# Rust mdbook

[link](https://rust-lang.github.io/mdBook/index.html)

# Github Actions

[docs](https://docs.github.com/en/actions/writing-workflows/quickstart)

## work with mdbook

[docs](https://github.com/MichaelCurrin/mdbook-quickstart.git)

### mdbook.yml

```
# Sample workflow for building and deploying a mdBook site to GitHub Pages
#
# To get started with mdBook see: https://rust-lang.github.io/mdBook/index.html
#
name: Deploy mdBook site to Pages

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
  # Build job
  build:
    runs-on: ubuntu-latest
    env:
      MDBOOK_VERSION: 0.4.36
    steps:
      - uses: actions/checkout@v4
      - name: Install mdBook
        run: |
          curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf -y | sh
          rustup update
          cargo install --version ${MDBOOK_VERSION} mdbook
      - name: Setup Pages
        id: pages
        uses: actions/configure-pages@v5
      - name: Build with mdBook
        run: mdbook build
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./book

  # Deployment job
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

## Configuring a subdomain

To set up a www or custom subdomain, such as www.example.com or blog.example.com, you must add your domain in the repository settings. After that, configure a CNAME record with your DNS provider.

On GitHub, navigate to your site's repository.

Under your repository name, click Settings. If you cannot see the "Settings" tab, select the dropdown menu, then click Settings.

Screenshot of a repository header showing the tabs. The "Settings" tab is highlighted by a dark orange outline.
In the "Code and automation" section of the sidebar, click Pages.

Under "Custom domain", type your custom domain, then click Save. If you are publishing your site from a branch, this will create a commit that adds a CNAME file directly to the root of your source branch. If you are publishing from a custom GitHub Actions workflow, no CNAME file is created, and any existing CNAME file is ignored and is not required. For more information about your publishing source, see Configuring a publishing source for your GitHub Pages site.

> Note
> If your custom domain is an internationalized domain name, you must enter the Punycode encoded version.
> For more information on Punycodes, see Internationalized domain name.

Navigate to your DNS provider and create a CNAME record that points your subdomain to the default domain for your site. For example, if you want to use the subdomain www.example.com for your user site, create a CNAME record that points www.example.com to <user>.github.io. If you want to use the subdomain another.example.com for your organization site, create a CNAME record that points another.example.com to <organization>.github.io. The CNAME record should always point to <user>.github.io or <organization>.github.io, excluding the repository name. For more information about how to create the correct record, see your DNS provider's documentation. For more information about the default domain for your site, see About GitHub Pages.

> Warning
> We strongly recommend that you do not use wildcard DNS records, such as \*.example.com. These records put you at an immediate risk of domain takeovers, even if you verify the domain. For example, if you verify example.com this prevents someone from using a.example.com but they could still take over b.a.example.com (which is covered by the wildcard DNS record). For more information, see Verifying your custom domain for GitHub Pages.

## HTTPS, Let’s Encrypt

Github pages already support Custom domain enforce HTTPS.
