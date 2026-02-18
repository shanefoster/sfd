# Portfolio Site

A modern, static portfolio site built with Jekyll and Tailwind CSS.

## Prerequisites

- Ruby (2.7 or higher)
- RubyGems
- Bundler
- Node.js and npm

## Setup

1. **Install Ruby dependencies:**
   ```bash
   bundle install
   ```

2. **Install Node dependencies:**
   ```bash
   npm install
   ```

3. **Build Tailwind CSS:**
   ```bash
   npm run build:css
   ```

   For development with auto-rebuild:
   ```bash
   npm run watch:css
   ```

4. **Run Jekyll server:**
   ```bash
   bundle exec jekyll serve
   ```

   Your site will be available at `http://localhost:4000`

## Development Workflow

1. Start Tailwind CSS watcher in one terminal:
   ```bash
   npm run watch:css
   ```

2. Start Jekyll server in another terminal:
   ```bash
   bundle exec jekyll serve
   ```

3. Make changes to your files and see them update automatically!

## Project Structure

```
.
├── _config.yml          # Jekyll configuration
├── _layouts/            # Page layouts
│   ├── default.html
│   ├── page.html
│   └── work.html
├── _includes/           # Reusable components
│   ├── header.html
│   └── footer.html
├── _work/               # Work markdown files
├── assets/
│   └── css/
│       ├── main.css     # Tailwind source file
│       └── style.css    # Generated CSS (gitignored)
├── index.html           # Home page
├── about.md             # About page
├── work.html            # Work listing page
└── Gemfile              # Ruby dependencies
```

## Adding Work

Create a new markdown file in the `_work/` folder with front matter:

```markdown
---
title: My Work
date: 2024-01-15
technologies:
  - React
  - Node.js
excerpt: A brief description of the work.
---

Your work content here...
```

## Customization

- **Site title and description:** Edit `_config.yml`
- **Styling:** Modify Tailwind classes in HTML files or extend the theme in `tailwind.config.js`
- **Layouts:** Customize templates in `_layouts/`
- **Navigation:** Update `_includes/header.html`

## Building for Production

1. Build Tailwind CSS:
   ```bash
   npm run build:css
   ```

2. Build Jekyll site:
   ```bash
   bundle exec jekyll build
   ```

   The generated site will be in the `_site/` directory.

## License

This is a starter template - customize it to your needs!
