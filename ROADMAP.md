# elliotreich.com — Personal Infrastructure Roadmap

**See master docs:** `/Users/elliot.reich/Local Codebase/CLAUDE.md` for the unified memory system. All completed stages are summarized there so every agent understands what infrastructure already exists.

---

## Architecture snapshot
```
Internet → Cloudflare (DNS/CDN/Pages) → VPS (Caddy reverse proxy + WireGuard server) →[encrypted tunnel]→ Raspberry Pi (local services)
```
- VPS: Spaceship.com VM (209.74.71.160) handles the WireGuard hub, Caddy routing (print.elliotreich.com), and exposes the public Tunnel endpoint.
- Raspberry Pi Zero 2 W runs Pi-hole (Docker), dnscrypt-proxy, and CUPS, and reaches the VPS over WireGuard (10.0.0.2 → 10.0.0.1).
- Cloudflare hosts `elliotreich.com` via Pages (CNAME to elliotreich-com.pages.dev) and proxies the domain; `print.elliotreich.com` is an A record to the VPS (Caddy reverse-proxied to CUPS).
- SSH keys: `~/.ssh/id_ed25519_new` works on both Pi and VPS; `ssh vps` and `ssh admin@pi.local` aliases exist.

## Completed work (moved to CLAUDE memory)
- Stages 1–4 (Pi setup, VPS setup, WireGuard tunnel, domain routing, SSL, print-server testing) fully operational. All infrastructure updates in `CLAUDE.md`.
- Stage 5 initial portfolio: live on Cloudflare Pages with contact links, auto-deploy, placeholder content (bio, gallery).
- Mac dev environment cleanup complete (Homebrew-only, python@3.14, SSH hygiene finalized).
- **Important note:** elliotreich-work/ draft CSS has drifted from the published site’s style guide (wrong fonts, background color). Content should be drafted using published site’s CSS before being copied over.

## Current actionable items

### Stage 5: Portfolio polish
- [ ] Replace placeholder gallery blocks with curated photos once the `elliotreich-work/` assets are ready; keep layouts responsive per the existing CSS grid.
- [ ] Write and publish the real bio content (About section) that conveys the media/technology/policy background you want the site to display.
- [ ] Add the print shop link (when Stage 6 decisions settle) so visitors can flow from the portfolio to the upcoming City Capture offerings.

### Stage 6: NYC photography print shop (City Capture)
- [ ] Finalize the brand name (City Capture is the working name) and tier (Printful vs. Prodigi vs. Fine Art America/Pixels) before opening the shop.
- [ ] If you choose Printful: create the Printful account, upload source images, choose product formats, connect to Etsy (or another storefront), and build 50–100+ listings with NYC-focused SEO language.
- [ ] If you take the Shopify route: wire Printful into the Shopify store once it exists, or use the Printful standalone storefront; keep the same catalog and launch sequence as the Etsy integration.
- [ ] Plan initial marketing (Etsy ads, reviews, image selection) and add the store link to the portfolio when the shop launches.

*Book project tasks are tracked separately in `../book-project/CLAUDE.md`.*

## Status & next action
**Updated:** 2026-02-27 (architecture audit; Stage 7 moved to book-project silo)

- **Status:** Infrastructure fully operational (Stages 1–4 complete, now tracked in `../infrastructure/`). Portfolio live on Cloudflare Pages with placeholder content. elliotreich-work CSS drifted from style guide.
- **Next action:** (1) Write real bio for elliotreich.com About section, (2) Curate & add gallery photos using published site's CSS, (3) Decide City Capture print shop details (brand name, vendor). When a task finishes, update this status paragraph with the date and new next action so memory always mirrors reality.
