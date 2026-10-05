# Northeast Seattle Toastmasters (Club 1161) — Website Export

This is a hosting-ready export of the Club 1161 website: a single `index.html` with real image files under `assets/img/`, built from the live working draft (`live-preview.html`) that London and Claude iterate on in chat.

## What's new in this export since the last one (Batch 56, 2026-10-05)

This export reflects every batch through **Batch 56** — the last export (delivered 2026-10-02) reflected through Batch 55. New since then (text/link changes only; no new images):

- **Media Kit is now linked (Batch 56).** The finished Club 1161 Media Kit PDF lives on Google Drive (`https://drive.google.com/file/d/17WqIu-T-X9hP5W6fJYnB5mm1vVzEBcut/view?usp=sharing`). It's linked in two places, both opening in a new tab with `rel="noopener noreferrer"`:
  - The Events-section Media Kit card now reads **"Download the Club 1161 Media Kit now."** (a link), replacing the old "will release sometime early Fall 2026" placeholder.
  - The footer's Connect column has a new **"Media Kit (PDF)"** link, placed just above "Email the Club."

### Earlier changes (previous export, Batches 54-55)
- **Ignite Seattle 52 outing (Batch 54).** A new Member Spotlights tile, "Ignite Seattle 52", and a new Club News card, "Our Night at Ignite", with London's writeup of the October 1 outing.
- **Stage photo leveled and centered (Batch 55)** and **Spotlights reorder (Batch 55)** so "Ignite Seattle 52" leads the grid.

### Earlier changes (Batch 53 export)
- Getting Started step 1 gained a "Watch the video for how to find us (YouTube)" link, and the existing directions link was relabeled "follow these directions (PDF)" so visitors know it opens a PDF.

### Earlier changes still (Batch 52 export and before)
Getting Started was restructured into an 8-step process with a dedicated RSVP step; new Club News card "The Next Era Has Begun" (first meeting at the new venue); new Spotlights tile for Dallas H. ("License Plate Improv"); Speech Contest Season tile reordered to the end and centered in its row; the Spotlights grid's empty final-row space now matches the page background instead of showing as a grey block; closing CTA band reworded to "See you Monday at 7:30 pm!". See the project status doc for the full batch-by-batch history.

## Image assets

No new images in this export. All 23 images under `assets/img/` are unchanged from the Batch 55 export (re-extracted from the current `live-preview.html` under the same naming convention).

## Updating the live GitHub Pages site

The site is already live at **www.neseattletoastmasters.org**, deployed from the GitHub repo `vp-pr-neseattletoastmasters.github.io` with a Squarespace-managed custom domain. To push this update:

1. Clone (or open your local copy of) `vp-pr-neseattletoastmasters.github.io`.
2. Replace the repo's `index.html` and `assets/` folder with the ones in this export.
3. Commit and push to the branch GitHub Pages serves from (usually `main`):
   ```
   git add index.html assets
   git commit -m "Link Media Kit in Events card and footer (Batch 56)"
   git push
   ```
4. GitHub Pages will rebuild automatically — changes are usually live within a minute or two. No DNS or Squarespace changes are needed; the custom domain is already wired up.

## Before this goes live — things worth double-checking
- **Speech Contest Season** tile still needs a real, confirmed contest date (on both the Spotlights tile and the Events list) — it's been using a placeholder-free real photo since Batch 32, but no date yet.
- **Google Meet virtual-meeting link** (`https://meet.google.com/tef-kmyi-xxb`) no longer appears anywhere on the page since Batch 36 repointed its button to the Events calendar — confirm with London whether the virtual option should get a new home on the page, or whether it's genuinely gone.
- **Residual security gap:** click-jacking protection (`X-Frame-Options` / CSP `frame-ancestors`) can't be added on GitHub Pages as configured today — that needs a real HTTP response header, which this static host can't send. Putting a service like Cloudflare in front of the domain would close this gap, but that's a hosting/DNS change that shouldn't happen without asking first.
- **Media Kit link** points to a Google Drive share link. If the PDF is ever replaced with a new file (new Drive ID), both links on the page need updating; replacing the contents of the same Drive file keeps the link working.

## Security notes (carried forward from Batch 31)
- A `Content-Security-Policy` meta tag and a `referrer` meta tag are in the `<head>` — this is the strongest lever available on a static host like GitHub Pages, since it can't send custom HTTP response headers. If a future edit adds a new external resource (a new font host, embed, or image origin), the matching CSP directive will need updating or the browser will silently block it.
- All external links use `rel="noopener noreferrer"`.
- The YouTube embed goes through `youtube-nocookie.com` with a trimmed permissions list.
- The "Copy Emails Instead" buttons use a three-step fallback (Clipboard API → `execCommand` → `window.prompt`) since `window.isSecureContext` reliance alone wasn't working for everyone — GitHub Pages's HTTPS satisfies the modern path, so this is mostly a safety net.

## Verification performed on this export
Checked with a headless browser against the exported files directly (not the chat preview):
- Zero JS errors; zero unexpected console messages beyond the sandbox's own network-blocked YouTube/font requests (both resolve fine on the real, deployed domain).
- Zero leftover `data:` image URIs — all 23 images are real files under `assets/img/`.
- Zero 4xx/5xx responses for any local resource, including the favicon (this only resolves in a real export, not the bare chat-preview fragment).
- All 9 `<img>` tags load with a valid `naturalWidth` (the one exception, the click-to-play YouTube thumbnail, is blocked by this sandbox's network only — confirmed working on the live domain previously).
- Media Kit: footer "Media Kit (PDF)" link and Events card "Download the Club 1161 Media Kit now." link both point to the Drive URL, open in a new tab, and carry `rel="noopener noreferrer"`; the old "early Fall 2026" text is gone.
- Spotlights grid: 8 tiles in the correct order, led by "Ignite Seattle 52."
- Club News carousel: 7 cards in the correct order, led by "Our Night at Ignite" with the corrected, leveled photo.
- All 7 officer cards render with the correct name/role and a real photo.
- Getting Started step 1 has both links with correct labels, hrefs, and hardening attributes.
- Closing CTA band reads "See you Monday at 7:30 pm!"
