# Update the Website CV

## Goal

Replace the website's CV with the supplied August 2026 PDF while preserving the current filename, routes, and About page.

## Source and Destination

- Source: `/Users/taeksangjang/Library/CloudStorage/Box-Box/CV/Jang_Taeksang_CV_Aug_2026.pdf`
- Source SHA-256: `204ca28637a950df0bbf0efc4f5bde797446b7c26ef1ac452401eb907ac94bcf`
- Destination: `assets/pdf/Jang_Taeksang_CV.pdf`

The source is an unencrypted, two-page Letter PDF with author `Taeksang Jang`. It was generated on August 27, 2026, at 10:50:58 AM CDT.

## Approach

Copy the supplied PDF byte-for-byte to the existing destination. Keep `_pages/cv.md`, `_layouts/cv.liquid`, and the website-facing filename unchanged.

Do not modify `_pages/about.md`. The About-page GitHub logo, GitHub link, email, LinkedIn link, research statement, and committee remain unchanged.

## Verification

- Confirm that the destination SHA-256 equals the source SHA-256.
- Confirm that the destination remains an unencrypted, two-page Letter PDF with author `Taeksang Jang`.
- Render and inspect both PDF pages for clipping, blank regions, unreadable text, or corruption.
- Confirm that the existing `/cv/` page and download link still target `Jang_Taeksang_CV.pdf`.
- Run the existing GitHub Actions deployment and require a successful conclusion.
- Confirm that the live CV has SHA-256 `204ca28637a950df0bbf0efc4f5bde797446b7c26ef1ac452401eb907ac94bcf`.
- Confirm that the live About page still shows the GitHub logo and link.
