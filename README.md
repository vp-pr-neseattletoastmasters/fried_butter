# Northeast Seattle Toastmasters — Club 1161 Website

A single-page static site. No build step, no framework, no dependencies beyond
two Google Fonts loaded via `<link>` tags in `index.html`. Open `index.html`
in a browser and it works as-is.

This export reflects everything through **Batch 35**, including the venue
move to Seattle Foursquare Church, the updated meeting calendar, two new
officer photos, and the earlier security hardening pass
(Content-Security-Policy, hardened external links, hardened YouTube embed).
It updates the site already live at **www.neseattletoastmasters.org**.

## What's in this export

- `index.html` — the entire site (one scrolling page with anchor-linked
  sections: Home, Innovation, Member Projects, About & Officers, Awards,
  Spotlights, Club News, Events, Getting Started). The header nav and footer
  link to sections on this same page (`#about`, `#spotlights`, etc.), not to
  separate pages.
- `assets/img/` — every photo and the club logo, as real image files
  (embedded inline in the working draft; extracted here so the browser can
  cache them separately and the HTML stays small). Same file names/paths as
  the previous export, plus three new files added for this batch:
  `assets/img/officers/president.jpg` (Catherine E.),
  `assets/img/officers/treasurer.jpg` (Dallas H.), and
  `assets/img/club-news/fairview-building.jpg` (the new "Thank You Fairview
  Church" news tile).

This replaces the earlier multi-page draft (`index.html` / `about.html` /
`spotlights.html` / `events.html` / `getting-started.html` + `css/style.css`)
from the very first pass at this project — that structure was abandoned early
on in favor of the single scrolling page you have here, which is what's been
refined ever since.

## What's new in this export (Batch 35)

- **Venue change:** the club now meets 100% in-person at **Seattle Foursquare
  Church, 400 N 105th St, Seattle, WA 98133** (previously hybrid at The
  Fairview Church). This is reflected in the meeting-info card, the Getting
  Started section, the Weekly Club Meeting event row, and the closing CTA
  band. The Google Meet virtual link is still shown but now labeled "Ends
  September 22nd."
- **Two new officer photos:** Catherine E. (President) and Dallas H.
  (Treasurer) now have real headshots instead of placeholder avatars.
- **Events calendar overhaul:** the calendar now shows specific cancelled
  dates (Sept 7, Nov 30, Dec 21, Dec 28, 2026), specific "Members Only" dates
  (Sept 14 and 21, 2026), and every Monday from Sept 28, 2026 onward labeled
  "In-person."
- **New Club News tile:** "Thank You Fairview Church," thanking the club's
  former venue and welcoming the new one.
- **VP Membership** now shows "Nomination Pending" instead of a named
  placeholder.
- A "See our dues table" link and a "follow these directions" (parking)
  link were added to the Getting Started section, both pointing to Google
  Drive documents.

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
   git commit -m "Venue change to Seattle Foursquare Church, new officer photos, calendar update"
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
  show initials-only avatars, and VP Membership ("Nomination Pending") has no
  photo by design. Search `index.html` for `officer-avatar` to find them.
- **Event dates** — the Speech Contest Season spotlight tile has a real
  photo, but it (and the matching entry in the Events calendar) still need a
  real, confirmed contest date.
- **Media Kit** — the Media Kit card currently states a release timeline
  (early Fall 2026); the PDF itself doesn't exist yet and isn't linked.
- **"Follow these directions" parking link** — this now links to a Google
  Drive doc; confirm it's the right one and that sharing permissions are set
  so visitors can view it without requesting access.

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
