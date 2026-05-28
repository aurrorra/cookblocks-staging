# cookblocks-pin-staging

Temporary staging area for CookBlocks Pinterest pin images.

## How it works

1. Pin images are committed here to `staging/` so they have a public URL.
2. The `cookblocks-pinterest` skill's `upload-media` ability fetches the image from the raw.githubusercontent.com URL and uploads it to WordPress.
3. WordPress at `wp-content/uploads/pinterest/YYYY/MM/` is the permanent home for the image.
4. A scheduled GitHub Action (`.github/workflows/cleanup.yml`) purges anything older than 7 days from `staging/` automatically.

This repo is a conveyor belt, not an archive. Don't add anything you care about long-term.
