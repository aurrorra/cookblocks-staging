# cookblocks-staging

Temporary staging area for CookBlocks workflow assets that need to reach WordPress programmatically.

## How it works

CookBlocks skills (Pinterest, blog-writing, others) sometimes need to upload images to WordPress as part of an automated workflow. The WordPress server can't reach into Haley's Mac to fetch files, so we use this repo as a bridge: commit the file here, get a public `raw.githubusercontent.com` URL, hand that URL to the WordPress plugin's `upload-media` ability, which fetches and stores it permanently.

## Structure

staging/
├── pinterest/    ← Pinterest skill writes here (pin images)
├── blog/         ← Blog-writing skill writes here (blog photos)
└── (additional skill subfolders added as the system grows)

Each skill uses its own subfolder so files don't collide.

## Lifecycle

1. A skill writes an image to its subfolder (e.g., `staging/pinterest/2026-05-28_souper-cubes_tutorial_1.png`).
2. The file is committed and pushed to GitHub.
3. The skill calls `cookblocks-wp:upload-media` with the resulting raw URL.
4. WordPress fetches the image and stores it in the proper permanent location (e.g., `wp-content/uploads/pinterest/2026/05/`).
5. The image's job in this repo is done. It will be auto-deleted 7 days later by `.github/workflows/cleanup.yml`.

This repo is a conveyor belt, not an archive. Don't add anything you care about long-term — it will be deleted on schedule.

## Permanent home

WordPress is the permanent home for any image that ships through this workflow:

- Pinterest pin images: `wp-content/uploads/pinterest/YYYY/MM/`
- Blog photos: `wp-content/uploads/YYYY/MM/` (standard WP media library)
