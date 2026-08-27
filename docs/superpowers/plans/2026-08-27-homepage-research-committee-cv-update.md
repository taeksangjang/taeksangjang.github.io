# Homepage Research, Committee, and CV Update Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Publish the approved homepage research introduction and dissertation committee, remove the education paragraph, and replace the website CV with the August 2026 PDF.

**Architecture:** Keep the existing Jekyll/al-folio structure and routes unchanged. Make one focused Markdown content edit in `_pages/about.md`, replace the published PDF byte-for-byte at its existing path, and verify the generated site plus both PDF pages.

**Tech Stack:** Jekyll, al-folio, Markdown/Liquid, Prettier 3.1.1, Docker Compose, Poppler PDF tools

## Global Constraints

- Preserve the homepage PhD-student introduction.
- Display this research paragraph exactly: `My research lies at the intersection of international business and strategy, where I study how geopolitical dynamics shape firms’ global innovation strategies. My dissertation focuses on two strategic responses under geopolitical disruption: knowledge flows within multinational corporations and global scaling.`
- Display this committee paragraph directly after the research paragraph: `Committee: Deepak Somaya (co-chair), Joseph Clougherty (co-chair), Fiona Kun Yao, Ishva Minefee.`
- Remove the education paragraph beginning `I earned my B.A.`
- Copy `/Users/taeksangjang/Library/CloudStorage/Box-Box/CV/Jang_Taeksang_CV_Aug_2026.pdf` to `assets/pdf/Jang_Taeksang_CV.pdf` without changing the website-facing filename.
- Require the published CV SHA-256 hash to equal `df58326d877619503e8e6de5c5e32cb88eb3440da7a03b373816f4bb6d4c6397`.
- Preserve `_pages/cv.md`, `_layouts/cv.liquid`, all routes, layout, styling, navigation, and links.
- Require a successful Jekyll production build.

---

## File Structure

- Modify `_pages/about.md`: homepage biography content only.
- Replace `assets/pdf/Jang_Taeksang_CV.pdf`: website-facing CV binary only.
- Preserve `_pages/cv.md`: existing `/cv/` route and PDF filename configuration.
- Preserve `_layouts/cv.liquid`: existing download link and embedded viewer.

### Task 1: Update the Homepage Research and Committee Copy

**Files:**

- Modify: `_pages/about.md:35-39`
- Test: `_pages/about.md` exact-text and deletion checks

**Interfaces:**

- Consumes: the approved research and committee paragraphs from `docs/superpowers/specs/2026-08-26-homepage-research-statement-design.md`
- Produces: homepage Markdown with the welcome paragraph unchanged, the approved research paragraph, and the approved committee paragraph

- [ ] **Step 1: Verify the approved copy is absent before the edit**

Run:

```bash
rg -nF "My research lies at the intersection of international business and strategy, where I study how geopolitical dynamics shape firms’ global innovation strategies. My dissertation focuses on two strategic responses under geopolitical disruption: knowledge flows within multinational corporations and global scaling." _pages/about.md
```

Expected: exit status 1 with no matches.

- [ ] **Step 2: Replace the research and education paragraphs**

Change the Markdown body after the front matter to exactly:

```markdown
Welcome! I am a PhD student in International Business and Strategy at Gies College of Business, the University of Illinois at Urbana-Champaign.

My research lies at the intersection of international business and strategy, where I study how geopolitical dynamics shape firms’ global innovation strategies. My dissertation focuses on two strategic responses under geopolitical disruption: knowledge flows within multinational corporations and global scaling.

Committee: Deepak Somaya (co-chair), Joseph Clougherty (co-chair), Fiona Kun Yao, Ishva Minefee.
```

- [ ] **Step 3: Format the homepage file**

Run:

```bash
npx prettier --write _pages/about.md
```

Expected: Prettier reports `_pages/about.md` as formatted.

- [ ] **Step 4: Verify the exact research paragraph and committee paragraph**

Run:

```bash
rg -nF "My research lies at the intersection of international business and strategy, where I study how geopolitical dynamics shape firms’ global innovation strategies. My dissertation focuses on two strategic responses under geopolitical disruption: knowledge flows within multinational corporations and global scaling." _pages/about.md
rg -nF "Committee: Deepak Somaya (co-chair), Joseph Clougherty (co-chair), Fiona Kun Yao, Ishva Minefee." _pages/about.md
```

Expected: one match for each paragraph.

- [ ] **Step 5: Verify the welcome paragraph remains and the education paragraph is gone**

Run:

```bash
rg -nF "Welcome! I am a PhD student in International Business and Strategy at Gies College of Business, the University of Illinois at Urbana-Champaign." _pages/about.md
rg -nF "I earned my B.A." _pages/about.md
```

Expected: the welcome paragraph has one match; the education search exits with status 1 and no matches.

- [ ] **Step 6: Review the focused source diff**

Run:

```bash
git diff --check
git diff -- _pages/about.md
```

Expected: no whitespace errors and no changes outside the three homepage body paragraphs.

- [ ] **Step 7: Commit the homepage update**

Run:

```bash
git add _pages/about.md
git commit -m "content: update homepage research and committee"
```

Expected: one commit containing only `_pages/about.md`.

### Task 2: Replace and Visually Verify the August 2026 CV

**Files:**

- Replace: `assets/pdf/Jang_Taeksang_CV.pdf`
- Preserve: `_pages/cv.md`
- Preserve: `_layouts/cv.liquid`
- Test: PDF hash, metadata, page renders, and route configuration

**Interfaces:**

- Consumes: `/Users/taeksangjang/Library/CloudStorage/Box-Box/CV/Jang_Taeksang_CV_Aug_2026.pdf`, SHA-256 `df58326d877619503e8e6de5c5e32cb88eb3440da7a03b373816f4bb6d4c6397`
- Produces: `assets/pdf/Jang_Taeksang_CV.pdf`, an identical unencrypted two-page letter-size PDF

- [ ] **Step 1: Verify the source CV before copying**

Run:

```bash
shasum -a 256 "/Users/taeksangjang/Library/CloudStorage/Box-Box/CV/Jang_Taeksang_CV_Aug_2026.pdf"
pdfinfo "/Users/taeksangjang/Library/CloudStorage/Box-Box/CV/Jang_Taeksang_CV_Aug_2026.pdf"
```

Expected: SHA-256 `df58326d877619503e8e6de5c5e32cb88eb3440da7a03b373816f4bb6d4c6397`; 2 pages; letter size; not encrypted; author `Taeksang Jang`.

- [ ] **Step 2: Confirm the current published PDF is different**

Run:

```bash
shasum -a 256 assets/pdf/Jang_Taeksang_CV.pdf
```

Expected: SHA-256 `d282f5f0d08170885dd007a0312aa47ad27a15d098db8061683f0413015992b6` before replacement.

- [ ] **Step 3: Replace the published CV**

Run:

```bash
cp "/Users/taeksangjang/Library/CloudStorage/Box-Box/CV/Jang_Taeksang_CV_Aug_2026.pdf" assets/pdf/Jang_Taeksang_CV.pdf
```

Expected: the destination file is replaced without changing its path.

- [ ] **Step 4: Verify byte identity and PDF metadata**

Run:

```bash
shasum -a 256 assets/pdf/Jang_Taeksang_CV.pdf
pdfinfo assets/pdf/Jang_Taeksang_CV.pdf
```

Expected: SHA-256 `df58326d877619503e8e6de5c5e32cb88eb3440da7a03b373816f4bb6d4c6397`; 2 pages; letter size; not encrypted; author `Taeksang Jang`.

- [ ] **Step 5: Render both CV pages for visual inspection**

Run:

```bash
mkdir -p /Users/taeksangjang/Documents/Codex/2026-08-26/i-w/work/cv-preview
pdftoppm -png -r 150 assets/pdf/Jang_Taeksang_CV.pdf /Users/taeksangjang/Documents/Codex/2026-08-26/i-w/work/cv-preview/page
```

Expected: `page-1.png` and `page-2.png` are created in the preview directory.

- [ ] **Step 6: Inspect both rendered pages**

Open `/Users/taeksangjang/Documents/Codex/2026-08-26/i-w/work/cv-preview/page-1.png` and `/Users/taeksangjang/Documents/Codex/2026-08-26/i-w/work/cv-preview/page-2.png` with the image-viewing tool.

Expected: both pages render completely with legible text, no clipping, no blank regions caused by rendering failure, and no visible corruption.

- [ ] **Step 7: Verify the existing CV route still targets the preserved filename**

Run:

```bash
rg -nF "cv_pdf: Jang_Taeksang_CV.pdf" _pages/cv.md
rg -nF "page.cv_pdf | prepend: 'assets/pdf/'" _layouts/cv.liquid
```

Expected: both configuration checks match once.

- [ ] **Step 8: Commit the CV update**

Run:

```bash
git add assets/pdf/Jang_Taeksang_CV.pdf
git commit -m "content: update CV for August 2026"
```

Expected: one commit containing only the website-facing CV PDF.

### Task 3: Build and Verify the Complete Site Update

**Files:**

- Verify: `_pages/about.md`
- Verify: `assets/pdf/Jang_Taeksang_CV.pdf`
- Verify generated output: `_site/index.html`
- Verify generated output: `_site/assets/pdf/Jang_Taeksang_CV.pdf`

**Interfaces:**

- Consumes: the committed homepage and CV updates from Tasks 1 and 2
- Produces: a successful Jekyll build whose homepage text and CV asset match the approved source files

- [ ] **Step 1: Run repository formatting checks**

Run:

```bash
npx prettier --check _pages/about.md docs/superpowers/specs/2026-08-26-homepage-research-statement-design.md docs/superpowers/plans/2026-08-27-homepage-research-committee-cv-update.md
git diff --check
```

Expected: Prettier reports all files formatted and Git reports no whitespace errors.

- [ ] **Step 2: Build the site with the repository's Dockerized Jekyll environment**

Run:

```bash
docker compose run --rm jekyll bundle exec jekyll build
```

Expected: exit status 0 and a generated `_site` directory. The Docker path avoids the host's incompatible Ruby 2.6 and missing Bundler 2.7.2.

- [ ] **Step 3: Verify the generated homepage content**

Run:

```bash
rg -nF "My research lies at the intersection of international business and strategy, where I study how geopolitical dynamics shape firms’ global innovation strategies." _site/index.html
rg -nF "Committee: Deepak Somaya (co-chair), Joseph Clougherty (co-chair), Fiona Kun Yao, Ishva Minefee." _site/index.html
rg -nF "I earned my B.A." _site/index.html
```

Expected: the research and committee text each match; the education search exits with status 1 and no matches.

- [ ] **Step 4: Verify the generated CV asset**

Run:

```bash
shasum -a 256 _site/assets/pdf/Jang_Taeksang_CV.pdf
```

Expected: SHA-256 `df58326d877619503e8e6de5c5e32cb88eb3440da7a03b373816f4bb6d4c6397`.

- [ ] **Step 5: Verify the working tree and commit history**

Run:

```bash
git status --short --branch
git log -3 --oneline
```

Expected: no uncommitted source changes; the plan, homepage, and CV commits are present. Generated `_site` output remains ignored by Git.

### Task 4: Publish and Verify GitHub Pages

**Files:**

- Publish committed `main` branch changes to `origin`
- Verify workflow: `.github/workflows/deploy.yml`
- Verify live homepage: `https://taeksangjang.github.io/`
- Verify live CV: `https://taeksangjang.github.io/assets/pdf/Jang_Taeksang_CV.pdf`

**Interfaces:**

- Consumes: the clean, validated `main` branch from Task 3
- Produces: a successful `Deploy site` workflow run and a live site matching the approved homepage and CV

- [ ] **Step 1: Verify the publication target**

Run:

```bash
git branch --show-current
git remote get-url origin
git status --short --branch
```

Expected: branch `main`; remote `https://github.com/taeksangjang/taeksangjang.github.io.git`; no uncommitted changes; local branch ahead of `origin/main`.

- [ ] **Step 2: Push the validated commits**

Run:

```bash
git push origin main
```

Expected: the new local commits are accepted by `origin/main`, triggering `.github/workflows/deploy.yml` because the push changes Markdown and assets.

- [ ] **Step 3: Wait for the deployment workflow**

Run:

```bash
deploy_run_id=$(gh run list --workflow deploy.yml --branch main --limit 1 --json databaseId --jq '.[0].databaseId')
gh run watch "$deploy_run_id" --exit-status
```

Expected: the latest `Deploy site` run completes with conclusion `success`.

- [ ] **Step 4: Verify the live homepage**

Run:

```bash
curl -fsSL https://taeksangjang.github.io/ -o /Users/taeksangjang/Documents/Codex/2026-08-26/i-w/work/published-homepage.html
rg -nF "My research lies at the intersection of international business and strategy, where I study how geopolitical dynamics shape firms’ global innovation strategies." /Users/taeksangjang/Documents/Codex/2026-08-26/i-w/work/published-homepage.html
rg -nF "Committee: Deepak Somaya (co-chair), Joseph Clougherty (co-chair), Fiona Kun Yao, Ishva Minefee." /Users/taeksangjang/Documents/Codex/2026-08-26/i-w/work/published-homepage.html
rg -nF "I earned my B.A." /Users/taeksangjang/Documents/Codex/2026-08-26/i-w/work/published-homepage.html
```

Expected: the research and committee text each match; the education search exits with status 1 and no matches.

- [ ] **Step 5: Verify the live CV bytes**

Run:

```bash
curl -fsSL https://taeksangjang.github.io/assets/pdf/Jang_Taeksang_CV.pdf -o /Users/taeksangjang/Documents/Codex/2026-08-26/i-w/work/published-cv.pdf
shasum -a 256 /Users/taeksangjang/Documents/Codex/2026-08-26/i-w/work/published-cv.pdf
```

Expected: SHA-256 `df58326d877619503e8e6de5c5e32cb88eb3440da7a03b373816f4bb6d4c6397`.
