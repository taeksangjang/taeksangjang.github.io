# Hide GitHub from the About Page

## Goal

Remove the GitHub logo and profile link from the About page while keeping the email and LinkedIn rows unchanged.

## Approach

Delete the GitHub `<p>` row from `profile.more_info` in `_pages/about.md`. The row contains both the Font Awesome GitHub icon and the link to `https://github.com/taeksangjang`, so deleting it removes both visible and clickable elements.

Do not change shared layouts, CSS, `_config.yml`, or social metadata. GitHub links used elsewhere on the site remain unchanged.

## Acceptance Criteria

- The About page shows the existing email and LinkedIn rows.
- The About page does not render a GitHub logo, the label `GitHub`, or a link to `https://github.com/taeksangjang` in the profile details.
- The homepage research statement, committee, profile image, navigation, and other pages remain unchanged.
- The existing GitHub Actions deployment completes successfully.
- The live About page matches these requirements after deployment.
