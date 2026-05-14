# andistonemedia-assets

Public CDN for images used on [andilippi.co.uk](https://andilippi.co.uk).

This repo is intentionally public so [jsDelivr](https://www.jsdelivr.com/) can serve every file directly. The main website source stays private; only the rendered assets sit here.

## How to add an image

1. Drop the file into the folder that matches where it'll be used on the site (see structure below).
2. `git add`, commit with a short message, `git push`.
3. The CDN URL is live within a few seconds. Pattern:

```
https://cdn.jsdelivr.net/gh/Andi-Stone-Media/andistonemedia-assets@main/{path}
```

Example — a panel screenshot for the Source Explorer tile on the home page:

```
home/featured-releases/source-explorer-panel-a.png
```

becomes

```
https://cdn.jsdelivr.net/gh/Andi-Stone-Media/andistonemedia-assets@main/home/featured-releases/source-explorer-panel-a.png
```

## Folder structure

Path mirrors where the asset is used on the site:

```
home/                       images used on /
  about-intro/              the "About Andi" block
  featured-releases/        the Source Explorer + BB Code tiles
  workbench/                workbench block illustrations (if any)
  music/                    custom album art overrides (if any)

about/                      images used on /pages/about
commissions/                images used on /pages/commissions
  past-work/                the recent-builds gallery
donate/                     images used on /pages/donate
memberships/                images used on /pages/memberships
shop/                       images used on /collections/all (the FW shop)

products/                   per-product hero art and screenshots
  source-explorer/
  bb-code/
  ...

brand/                      logos, marks, favicons, social cards
```

When in doubt, mirror the path of the source HTML file. If `pages/home/04-featured-releases.html` uses an image, put it in `home/featured-releases/`.

## Naming convention

- **All lowercase, kebab-case.** No spaces, no underscores, no caps.
- **Product before component.** `source-explorer-panel-a.png` reads better than `panel-a-source-explorer.png`.
- **Format extension is honest.** PNG for transparent art, JPG for photos, WebP if you've optimised, SVG for vectors. Don't lie about the format.
- **No version numbers in normal filenames.** Replace the file in place when you iterate. Only add a `-v2`, `-v3` suffix if you're bypassing jsDelivr's cache (see below) or keeping the previous version around for rollback.

Good examples:
- `home/featured-releases/source-explorer-panel-a.png`
- `home/featured-releases/bb-code.png`
- `about/origin-story-photo.jpg`
- `products/source-explorer/hero.png`

## Cache busting

jsDelivr aggressively caches `@main` URLs and can take up to 12 hours to pick up a replacement at the same path. Two ways around it:

1. **Pin to a commit hash** for guaranteed freshness on demo links:
   ```
   https://cdn.jsdelivr.net/gh/Andi-Stone-Media/andistonemedia-assets@<commit-sha>/home/featured-releases/source-explorer-panel-a.png
   ```
2. **Bump the filename** when you replace an image you can't wait for: `source-explorer-panel-a.png` → `source-explorer-panel-a-v2.png`, then update the reference on the website.

For new assets the cache is irrelevant — they're live instantly.

## What does NOT belong here

- Anything secret (auth tokens, private API keys, customer data).
- Source files for vector art (Figma, AI, Sketch, .psd) — keep those in `andistonemedia-brand` or wherever you're authoring.
- Raw camera files or unprocessed exports — optimise before committing.
- Marketing video — too large; use a video host (YouTube, Vimeo) or Cloudflare Stream.
