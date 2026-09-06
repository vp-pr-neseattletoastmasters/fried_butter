# Northeast Seattle Toastmasters — Club 1161 Website

A single-page static site. No build step, no framework, no dependencies beyond
two Google Fonts loaded via `<link>` tags in `index.html`. Open `index.html`
in a browser and it works as-is.

## What's in this export

- `index.html` — the entire site (one scrolling page with anchor-linked
  sections: Home, Innovation, Member Projects, About & Officers, Awards,
  Spotlights, Club News, Events, Getting Started). The header nav and footer
  link to sections on this same page (`#about`, `#spotlights`, etc.), not to
  separate pages.
- `assets/img/` — every photo and the club logo, as real image files
  (previously embedded inline in the working draft; extracted here so the
  browser can cache them separately and the HTML stays small).

This replaces the earlier multi-page draft (`index.html` / `about.html` /
`spotlights.html` / `events.html` / `getting-started.html` + `css/style.css`)
from the very first pass at this project — that structure was abandoned early
on in favor of the single scrolling page you have here, which is what's been
refined ever since.

## Deploying to GitHub Pages

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
  format (currently: Mondays, 7:30–9:00 PM, hybrid, The Fairview Church,
  Room 311, 844 NE 78th St, Seattle, WA 98115) — cross-check against the
  official Toastmasters "Find a Club" listing:
  <https://www.toastmasters.org/Find-a-Club/00001161-northeast-toastmasters-club>
- **Officer photos** — 2 of 7 officers (VP Innovation, VP Public Relations)
  have real photos; the other 5 still show initials-only avatars. Search
  `index.html` for `officer-avatar` to find them.
- **Event dates** — the Speech Contest Season spotlight tile and the Events
  calendar still need real, confirmed dates.
- **Media Kit** — the Media Kit card currently states a release timeline
  (early Fall 2026); the PDF itself doesn't exist yet and isn't linked.

## Toastmasters branding note

This site avoids using the official Toastmasters International logo file
in any way not sanctioned by the Brand Portal, and doesn't use a
club-created logo or tagline (not permitted per the Brand Manual). Copy
uses the manual's approved marketing phrases verbatim ("Find Your Voice",
"Find Your Confidence"). The footer includes the mandatory Website
Guidelines disclaimer. Confirm current brand-portal compliance before
publishing if the Brand Manual has been updated since this was built.
