# Northeast Seattle Toastmasters (Club 1161) — Website Export

This is a hosting-ready export of the Club 1161 website: a single `index.html` with real image files under `assets/img/`, built from the live working draft (`live-preview.html`) that London and Claude iterate on in chat.

## What's new in this export since the last one (Batch 55, 2026-10-02)

This export reflects every batch through **Batch 55** — the last export (delivered 2026-10-01) only reflected through Batch 53. New since then:

- **Ignite Seattle 52 outing (Batch 54).** Two new pieces of content from the club's October 1 trip to Ignite Seattle 52 at Seattle Town Hall:
  - A new Member Spotlights tile, **"Ignite Seattle 52"** (eyebrow "Extracurricular Opportunities"), using a group photo from the event.
  - A new Club News card, **"Our Night at Ignite"** (eyebrow "Extracurricular Activities"), using a photo of club members on stage, with London's full writeup about the evening.
- **Stage photo leveled and centered (Batch 55).** The "Our Night at Ignite" photo had a ~1.3° tilt in the projector screen behind the speakers — straightened and re-cropped so the screen reads level and centered.
- **Spotlights reorder (Batch 55).** The "Ignite Seattle 52" tile now leads the Spotlights grid instead of trailing it (pure reorder, no other tiles changed).

### Earlier changes (previous export, Batch 53)
- Getting Started step 1 gained a "Watch the video for how to find us (YouTube)" link, and the existing directions link was relabeled "follow these directions (PDF)" so visitors know it opens a PDF.

### Earlier changes still (Batch 52 export and before)
Getting Started was restructured into an 8-step process with a dedicated RSVP step; new Club News card "The Next Era Has Begun" (first meeting at the new venue); new Spotlights tile for Dallas H. ("License Plate Improv"); Speech Contest Season tile reordered to the end and centered in its row; the Spotlights grid's empty final-row space now matches the page background instead of showing as a grey block; closing CTA band reworded to "See you Monday at 7:30 pm!". See the project status doc for the full batch-by-batch history.

## New image assets in this export

Two new images were added (both from the Ignite Seattle 52 outing):
- `assets/img/spotlights/ignite-seattle-52.jpg`
- `assets/img/club-news/our-night-at-ignite.jpg` (this is the leveled/recentered version, not the original tilted photo)

Every other image in this export is unchanged from the Batch 53 export, just re-extracted and re-saved under the same naming convention (no previous export's asset files were available locally to hash-match byte-for-byte against this time, so all 23 images were re-extracted fresh from the current `live-preview.html` — this does not change any image's content, only regenerates the files).

## Updating the live GitHub Pages site

The site is already live at **www.neseattletoastmasters.org**, deployed from the GitHub repo `vp-pr-neseattletoastmasters.github.io` with a Squarespace-managed custom domain. To push this update:

1. Clone (or open your local copy of) `vp-pr-neseattletoastmasters.github.io`.
2. Replace the repo's `index.html` and `assets/` folder with the ones in this export.
3. Commit and push to the branch GitHub Pages serves from (usually `main`):
   ```
   git add index.html assets
   git commit -m "Add Ignite Seattle 52 content (Batches 54-55)"
   git push
   ```
4. GitHub Pages will rebuild automatically — changes are usually live within a minute or two. No DNS or Squarespace changes are needed; the custom domain is already wired up.

## Before this goes live — things worth double-checking
- **Speech Contest Season** tile still needs a real, confirmed contest date (on both the Spotlights tile and the Events list) — it's been using a placeholder-free real photo since Batch 32, but no date yet.
- **Google Meet virtual-meeting link** (`https://meet.google.com/tef-kmyi-xxb`) no longer appears anywhere on the page since Batch 36 repointed its button to the Events calendar — confirm with London whether the virtual option should get a new home on the page, or whether it's genuinely gone.
- **Residual security gap:** click-jacking protection (`X-Frame-Options` / CSP `frame-ancestors`) can't be added on GitHub Pages as configured today — that needs a real HTTP response header, which this static host can't send. Putting a service like Cloudflare in front of the domain would close this gap, but that's a hosting/DNS change that shouldn't happen without asking first.
- Media Kit PDF doesn't exist yet as a linked file on the site (draft tracked separately).

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
- Spotlights grid: 8 tiles in the correct order, led by "Ignite Seattle 52."
- Club News carousel: 7 cards in the correct order, led by "Our Night at Ignite" with the corrected, leveled photo.
- All 7 officer cards render with the correct name/role and a real photo.
- Getting Started step 1 has both links with correct labels, hrefs, and hardening attributes.
- Closing CTA band reads "See you Monday at 7:30 pm!"
