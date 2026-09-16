# Northeast Seattle Toastmasters — Club 1161 Website

A single-page static site. No build step, no framework, no dependencies beyond
two Google Fonts loaded via `<link>` tags in `index.html`. Open `index.html`
in a browser and it works as-is.

This export reflects everything through **Batch 39**, including the venue
move to Seattle Foursquare Church, the updated meeting calendar, officer
roster changes, the copy-to-clipboard email buttons (now with a hardened
fallback chain so they work in more browsers), and the earlier security
hardening pass (Content-Security-Policy, hardened external links, hardened
YouTube embed). It updates the site already live at
**www.neseattletoastmasters.org**.

## What's in this export

- `index.html` — the entire site (one scrolling page with anchor-linked
  sections: Home, Innovation, Member Projects, About & Officers, Awards,
  Spotlights, Club News, Events, Getting Started). The header nav and footer
  link to sections on this same page (`#about`, `#spotlights`, etc.), not to
  separate pages.
- `assets/img/` — every photo and the club logo, as real image files
  (embedded inline in the working draft; extracted here so the browser can
  cache them separately and the HTML stays small). Same file names/paths as
  the previous export — no new photos were added in this batch.

This replaces the earlier multi-page draft (`index.html` / `about.html` /
`spotlights.html` / `events.html` / `getting-started.html` + `css/style.css`)
from the very first pass at this project — that structure was abandoned early
on in favor of the single scrolling page you have here, which is what's been
refined ever since.

## What's new in this export since the last one

- **VP Membership** is now "Doni K." (was "Nomination Pending").
- **Meeting-card button changed:** the old "Virtual Meeting Link" button is
  now "Calendar of Events" with a calendar icon, and takes visitors straight
  to the Events calendar instead of the Google Meet link. Note: the Google
  Meet link itself no longer appears anywhere on the page as a result — flag
  if you'd like it linked somewhere else.
- **Multi-recipient email links** (the "our officers" link and the "RSVP Now"
  button) now separate addresses with semicolons instead of commas, and each
  has a "Copy Emails Instead" button next to it. That button now uses a
  three-step fallback (modern clipboard API → legacy `execCommand` → a
  manual copy prompt) so it works even in browsers or preview panes that
  block the newer clipboard API.
- The Spotlights tile "An Impromptu Bit at Stage Night" now reads "London's
  Impromptu Bit at Stage Night."

## Updating the live GitHub Pages site

Since the site is already deployed, this export replaces the files in your
existing repo rather than starting a new one:

1. In your local clone of the `vp-pr-neseattletoastmasters.github.io` repo,
   delete the old `index.html` and `assets/` folder and copy in this export's
   `index.html` and `assets/` folder (do not touch your `CNAME` file, if you
   have one, or any GitHub Pages settings — those stay as they are).
2. From the repo folder:
   ```bash
   git add -A
   git commit -m "VP Membership update, calendar CTA, email copy buttons"
   git push
   ```
3. GitHub Pages rebuilds automatically after the push — give it a minute or
   two, then reload **www.neseattletoastmasters.org** (a hard refresh /
   private window helps if you still see the old version, since browsers
   cache static sites aggressively).

## Deploying from scratch (first-time reference)

1. Create a new **public** repo on GitHub (e.g. `ne-seattle-toastmasters`).
2. From this folder:
   ```bash
   git init
   git add .
   git commit -m "Initial site build"
   git branch -M main
   git remote add origin https://github.com/<your-username>/<repo-name>.git
   git push -u origin main
   ```
3. On GitHub: **Settings → Pages → Build and deployment → Source: Deploy from
   a branch → Branch: `main` / root**. Save.
4. Your site will be live at `https://<your-username>.github.io/<repo-name>/`
   within a minute or two.
5. Optional: add a custom domain under **Settings → Pages → Custom domain**
   (requires a `CNAME` file at the repo root, which GitHub will create for you).

## Deploying anywhere else

This is a plain static site, so any static host works the same way — drag
the whole folder into Netlify, Vercel, Cloudflare Pages, or an S3 bucket with
static-website hosting turned on. There's nothing to build or configure
beyond pointing the host at `index.html`.

## Before this goes live

- **Verify meeting details against Club Central** — day/time, location, and
  format (currently: Mondays, 7:30–9:00 PM, 100% in-person, Seattle
  Foursquare Church, 400 N 105th St, Seattle, WA 98133) — cross-check against
  the official Toastmasters "Find a Club" listing:
  <https://www.toastmasters.org/Find-a-Club/00001161-northeast-toastmasters-club>
- **Officer photos** — 4 of 7 officers (President, Treasurer, VP Innovation,
  VP Public Relations) have real photos; VP Education and VP Operations still
  show initials-only avatars, and Doni K. (VP Membership) doesn't have one
  yet either. Search `index.html` for `officer-avatar` to find them.
- **Event dates** — the Speech Contest Season spotlight tile has a real
  photo, but it (and the matching entry in the Events calendar) still need a
  real, confirmed contest date.
- **Media Kit** — the Media Kit card currently states a release timeline
  (early Fall 2026); the PDF itself doesn't exist yet and isn't linked.
- **Virtual meeting option** — since the meeting-card button now points to
  the calendar instead of Google Meet, confirm whether the virtual option
  should be linked somewhere else on the page, or whether it's intentionally
  gone now that meetings are 100% in-person.

## Security notes

- `index.html` includes a Content-Security-Policy meta tag restricting
  scripts, styles, fonts, images, and frames to the specific origins the
  page actually uses, plus a `referrer` meta tag. GitHub Pages serves static
  files only and can't send custom HTTP response headers, so this meta tag
  is the strongest lever available on this host — it cannot cover
  click-jacking protection (`frame-ancestors`), which requires a real HTTP
  header. If that matters, putting a service like Cloudflare in front of the
  domain would allow adding it, but that's a hosting/DNS change worth
  deciding on deliberately rather than doing by default.
- All external links use `rel="noopener noreferrer"`, and the club video
  embed uses YouTube's privacy-enhanced `youtube-nocookie.com` domain.
- The "Copy Emails Instead" buttons use the Clipboard API only when the page
  is in a secure context (`window.isSecureContext`) — GitHub Pages serves
  over HTTPS, so this will be true on the live site.
- If you add a new external resource later (a new font host, embed, or
  image origin), the CSP meta tag's directives will need a matching update
  or the browser will silently block it.

## Toastmasters branding note

This site avoids using the official Toastmasters International logo file
in any way not sanctioned by the Brand Portal, and doesn't use a
club-created logo or tagline (not permitted per the Brand Manual). Copy
uses the manual's approved marketing phrases verbatim ("Find Your Voice",
"Find Your Confidence"). The footer includes the mandatory Website
Guidelines disclaimer. Confirm current brand-portal compliance before
publishing if the Brand Manual has been updated since this was built.
