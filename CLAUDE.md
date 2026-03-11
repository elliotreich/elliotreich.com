# elliotreich.com — Personal Portfolio Website

## What This Is

Published personal portfolio website hosted on Cloudflare Pages. Static HTML/CSS site showcasing professional background (media, technology, policy), NYC street photography, and links to other projects.

## Key Assets & Context

- **Domain:** elliotreich.com (public repo)
- **Hosting:** Cloudflare Pages (auto-deploy on push)
- **Infrastructure:** See `../infrastructure/CLAUDE.md` for DNS, CDN, reverse proxy setup
- **Design:** Responsive CSS grid, DM Sans + Inter fonts, Parchment/Bark/Lichen color palette
- **Gallery:** NYC street photography (curated, high-res managed separately)
- **Backup:** Git repo + Cloudflare Pages cache

## Tech Stack

- **HTML5** — semantic structure
- **CSS3** — responsive grid, mobile-first
- **Assets:** Photography (local), icons (svg/css)
- **Deployment:** `git push` → Cloudflare auto-deploys
- **Domain:** Cloudflare DNS + Pages CNAME

## How to Get Things Done

### Updating Content
1. Edit `index.html`, `style.css` or add files locally
2. Test in browser (open `index.html` locally or use a simple server)
3. Commit: `git add . && git commit -m "elliotreich.com - [Change description]"`
4. Push: `git push origin main` (Cloudflare deploys automatically)

### Adding Gallery Photos
1. Store high-res originals in `assets/photos/`
2. Create thumbnails/web-optimized versions
3. Update `index.html` to reference new images in the gallery section
4. Test responsiveness at mobile/tablet/desktop sizes
5. Push to deploy

### Styling Changes
- Edit `style.css` directly
- Test across browsers and screen sizes
- Follow existing conventions: CSS Grid for layouts, relative units (em/rem), mobile-first media queries
- Keep fonts consistent: DM Sans (headers) + Inter (body)

### Publishing Drafts from elliotreich-work
1. Draft/edit in `../elliotreich-work/`
2. When ready, copy finalized files here
3. Follow style guide from `styleguide.md`
4. Commit and push

## Conventions Specific to This Project

- **Branch:** Always `main` (no feature branches for single edits)
- **Commits:** `elliotreich.com - [Change]` (e.g., "elliotreich.com - Update bio section")
- **Asset naming:** `kebab-case.jpg` (e.g., `brooklyn-bridge-sunrise.jpg`)
- **CSS classes:** `.section`, `.gallery`, `.photo`, `.contact` (descriptive, no abbreviations)
- **Font weights:** Regular (400), Semi-bold (600), Bold (700) only

## Current Status & Next Actions

**Updated:** 2026-02-27

- **Status:** Site live on Cloudflare Pages with placeholder content (landing page, gallery stubs, contact links). Infrastructure complete (Pi, VPS, WireGuard, print server all operational).
- **Next Actions:**
  - [ ] Write real bio for About section (currently placeholder)
  - [ ] Curate and add real NYC street photography to gallery
  - [ ] Verify print shop link (when City Capture print shop launches)
  - [ ] Test gallery responsiveness on mobile

---

**Public GitHub:** https://github.com/elliotreich/elliotreich.com
