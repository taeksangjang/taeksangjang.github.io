# Homepage Research Introduction and CV Update

## Objective

Replace the homepage's one-sentence research statement with the approved two-sentence research introduction, replace the education paragraph with the dissertation committee, and publish the August 2026 CV.

## Approved copy

> My research lies at the intersection of international business and strategy, where I study how geopolitical dynamics shape firms’ global innovation strategies. My dissertation focuses on two strategic responses under geopolitical disruption: knowledge flows within multinational corporations and global scaling.

## Approved committee copy

> Committee: Deepak Somaya (co-chair), Joseph Clougherty (co-chair), Fiona Kun Yao, Ishva Minefee.

## Scope

- Replace the current one-sentence research paragraph in `_pages/about.md` with the approved two-sentence paragraph.
- Replace the current education paragraph in `_pages/about.md` with the approved committee paragraph.
- Replace `assets/pdf/Jang_Taeksang_CV.pdf` with `/Users/taeksangjang/Library/CloudStorage/Box-Box/CV/Jang_Taeksang_CV_Aug_2026.pdf` while preserving the website-facing filename.
- Preserve the preceding PhD-student introduction.
- Preserve the existing CV page configuration, download link, and embedded viewer.
- Preserve all other homepage content, layout, styling, navigation, and links.

## Acceptance criteria

- The homepage displays the approved paragraph exactly, including punctuation and curly apostrophes.
- The homepage displays the approved committee paragraph directly after the research introduction and no longer displays the education paragraph.
- The published CV is an unencrypted, two-page letter-size PDF whose SHA-256 hash is `df58326d877619503e8e6de5c5e32cb88eb3440da7a03b373816f4bb6d4c6397`.
- The CV remains available at `/assets/pdf/Jang_Taeksang_CV.pdf` and through the existing `/cv/` page.
- No other visible content or behavior changes.
- The site builds successfully with the existing Jekyll configuration.
