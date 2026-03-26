# CLAUDE.md — Website Maintenance Notes

## Project Overview
- Personal academic website for Taeksang Jang (PhD student, UIUC Gies College of Business)
- Jekyll site using the **al-folio** theme, deployed via **GitHub Pages**
- Repository: `taeksangjang/taeksangjang.github.io` on `main` branch

## Key File Locations

### CV
- **CV PDF**: `assets/pdf/mycv.pdf` — linked from the CV page and social/footer icon
  - Source of truth: `/Users/taeksangjang/Library/CloudStorage/Box-Box/CV/Jang_Taeksang_CV.pdf`
- **CV page data**: `assets/json/resume.json` — drives the rendered CV page content
- **CV page config**: `_pages/cv.md` — sets `cv_pdf: mycv.pdf`
- **CV layout**: `_layouts/cv.liquid` — contains custom heading mappings (work → "Professional Experience", volunteer → "Academic Service", awards → "Fellowships, Grants, and Awards", skills → "Technical Skills", interests → "Research Interests")
- **Section order**: controlled by `jsonresume` list in `_config.yml` (currently: basics, education, interests, awards, volunteer, certificates, skills, work)
- **Date templates**: `_includes/resume/*.liquid` — modified to show year only (no month), and single year when start == end

### Teaching
- **Teaching page**: `_pages/teaching.md` — includes philosophy, experience, evaluation tables, and student comments
  - Source: `/Users/taeksangjang/Library/CloudStorage/Box-Box/Teaching/teaching statement/Teaching_Statement.pdf`

### Social links
- `_data/socials.yml` — includes `cv_pdf: /assets/pdf/mycv.pdf` for the footer/social CV link

### Favicon
- `_config.yml` line 18: `icon: favicon.jpeg` (Gies College of Business logo)
- Image at: `assets/img/favicon.jpeg`

## Code Formatting
- **Prettier** is configured with `@shopify/prettier-plugin-liquid`
- Config: `.prettierrc` (printWidth: 150, trailingComma: es5)
- **Always run `npx prettier --write <files>` on changed files before committing**
- Check with: `npx prettier --check <files>`

## Workflow Reminders
- After updating CV content, both `mycv.pdf` and `resume.json` may need updating
- The `_data/cv.yml` file still has placeholder (Albert Einstein) data — it is not used because `resume.json` exists (the cv.liquid layout checks for `site.data.resume` first)
- GitHub Pages rebuild takes a minute or two after push; browser cache (Cmd+Shift+R) may need clearing
