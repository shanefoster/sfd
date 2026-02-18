# Deploy to GitHub Pages (Path B: Fresh Repo)

Use this guide to deploy your Jekyll 4 portfolio to a new GitHub repo and point shanefoster.design at it.

---

## Step 1: Create a new repo on GitHub

1. Go to [github.com/new](https://github.com/new)
2. Name: `shanefoster.github.io` (for user site) or any name (for project site)
3. Public visibility
4. **Do not** add README, .gitignore, or license
5. Click Create repository

---

## Step 2: Add the GitHub Actions workflow

Create `.github/workflows/pages.yml` in this project with:

```yaml
name: Deploy to GitHub Pages
on:
  push:
    branches: [main]
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
      - uses: ruby/setup-ruby@v1
        with:
          ruby-version: '3.2'
          bundler-cache: true
      - run: bundle exec jekyll build
      - uses: actions/upload-pages-artifact@v3
        with:
          path: ./_site
  deploy:
    needs: build
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - id: deployment
        uses: actions/deploy-pages@v4
```

---

## Step 3: Set production URL in _config.yml

Add before deploying (or use environment variable):

```yaml
url: "https://shanefoster.design"
```

Leave `baseurl: ""` for a user/apex domain setup.

---

## Step 4: Initialize git and push

```bash
cd /Users/shanefoster/Sites/sfd
git init
git add .
git commit -m "Initial commit: new Jekyll 4 portfolio"
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO.git
git branch -M main
git push -u origin main
```

Replace `YOUR_USERNAME` and `YOUR_REPO` with your GitHub username and repo name.

---

## Step 5: Enable GitHub Pages

1. Repo → **Settings** → **Pages**
2. Under **Build and deployment**, set Source to **GitHub Actions**
3. Save (no further config needed—the workflow handles the rest)

---

## Step 6: Point shanefoster.design to the new site

### If the domain is already used by another repo (e.g. your old site)

GitHub only lets a domain be attached to one repo. Remove it from the old one first:

1. Open your **old** repository on GitHub
2. **Settings** → **Pages**
3. Under **Custom domain**, click **Remove**
4. Save

Then add it to your new repo (steps below).

### In GitHub (new repo Settings → Pages)

1. Under **Custom domain**, enter: `shanefoster.design`
2. Save
3. Optionally enable **Enforce HTTPS** (after DNS verifies)

### In your DNS provider (where you manage shanefoster.design)

| Type | Name/Host | Value |
|------|-----------|-------|
| A | `@` (or blank for apex) | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |
| CNAME | `www` | `shanefoster.github.io` |

Replace `shanefoster` with your GitHub username in the CNAME value.

**If you already use shanefoster.design with the old site:** These records may already be correct. You only need to set the custom domain in the new repo's Pages settings.

**Propagation:** DNS changes can take a few minutes to 48 hours. GitHub will show "DNS check is still in progress" until it's ready.

---

## After deployment

- Site URL: `https://shanefoster.design`
- Build logs: Repo → **Actions** tab
- Allow 1–2 minutes after each push for the site to update
