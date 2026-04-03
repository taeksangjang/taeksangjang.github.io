# CLAUDE.md — Website Maintenance Notes

## Project Overview

- Personal academic website for Taeksang Jang (PhD student, UIUC Gies College of Business)
- Jekyll site using the **al-folio** theme, deployed via **GitHub Pages**
- Repository: `taeksangjang/taeksangjang.github.io` on `main` branch

## Key File Locations

### CV

- **CV PDF**: `assets/pdf/Jang_Taeksang_CV.pdf` — linked from the CV page
  - Source of truth: `/Users/taeksangjang/Library/CloudStorage/Box-Box/CV/Jang_Taeksang_CV.pdf`
- **CV page config**: `_pages/cv.md` — sets `cv_pdf: Jang_Taeksang_CV.pdf`
- **CV layout**: `_layouts/cv.liquid` — simplified to PDF download link + embedded PDF preview
- **Full CV layout backup**: `_layouts/cv_full.liquid.bak` — previous layout with structured HTML sections from `resume.json` (custom heading mappings, section ordering, etc.). Rename back to `cv.liquid` to restore.
- **CV page data**: `assets/json/resume.json` — still present but not currently used by the simplified layout
- **Section order** (for full layout): controlled by `jsonresume` list in `_config.yml`
- **Date templates** (for full layout): `_includes/resume/*.liquid` — modified to show year only

### Teaching

- **Teaching page**: `_pages/teaching.md` — includes philosophy, experience, evaluation tables, and student comments
  - Source: `/Users/taeksangjang/Library/CloudStorage/Box-Box/Teaching/teaching statement/Teaching_Statement.pdf`

### Social links

- `_data/socials.yml` — social icons are disabled on the about page (`social: false`); CV icon (`cv_pdf`) is commented out

### Favicon

- `_config.yml` line 18: `icon: favicon.jpeg` (Gies College of Business logo)
- Image at: `assets/img/favicon.jpeg`

## Code Formatting

- **Prettier** is configured with `@shopify/prettier-plugin-liquid`
- Config: `.prettierrc` (printWidth: 150, trailingComma: es5)
- **Always run `npx prettier --write <files>` on changed files before committing**
- Check with: `npx prettier --check <files>`

## Workflow Reminders

- After updating CV content, update `Jang_Taeksang_CV.pdf` (and `resume.json` if restoring the full layout)
- The `_data/cv.yml` file still has placeholder (Albert Einstein) data — it is not used because `resume.json` exists (the cv.liquid layout checks for `site.data.resume` first)
- GitHub Pages rebuild takes a minute or two after push; browser cache (Cmd+Shift+R) may need clearing
