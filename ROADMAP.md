# elliotreich.com — Personal Infrastructure Roadmap

Covers the personal website, VPS, home server (Raspberry Pi), and self-hosted services.

---

## Architecture Overview

```
Internet → Cloudflare (DNS/CDN) → VPS (Caddy reverse proxy + WireGuard server)
                                         ↓ WireGuard tunnel
                                    Raspberry Pi (local services)
```

- **VPS**: public-facing hub, routes traffic to Pi services via encrypted tunnel
- **Pi**: runs services locally (Pi-hole, CUPS, etc.), connects outbound to VPS
- **Caddy**: handles SSL and subdomain routing on the VPS
- **Cloudflare**: DNS + CDN proxy in front of VPS

Services that only need to work on the local network (Pi-hole) don't need the VPS.
Services you want accessible from anywhere (print server, etc.) go through the VPS tunnel.

---

## Stage 1: Raspberry Pi — Local Setup
*Do this first. No VPS spending required.*

### Done
- [x] Pi is on, reachable at `pi.local` (192.168.86.26), MAC `2c:cf:67:d9:e1:d9`
- [x] SSH key on Mac, VS Code Remote-SSH configured
- [x] Password SSH login disabled (key-only auth)
- [x] System packages fully updated (2026-02-18)
- [x] dpkg repaired (initramfs-tools config conflict resolved)

### Next Up — Start Here
- [ ] **Install Docker** — previous attempt failed (Pi rebooted mid-download, SSH dropped)
  - SSH in, confirm with `docker --version` (almost certainly not installed)
  - Re-run: `curl -fsSL https://get.docker.com | sudo sh && sudo usermod -aG docker admin`
  - Pi Zero 2 W is slow over WiFi — give it 10–15 min, don't run as background task

### To Do (in order)
- [ ] Confirm Docker is installed and `docker compose version` works
- [ ] Set DHCP reservation in router: MAC `2c:cf:67:d9:e1:d9` → always assign 192.168.86.26 *(Pi currently gets this via regular DHCP, not a guaranteed reservation)*
- [ ] Install ufw: allow SSH (22), DNS (53 tcp+udp), Pi-hole web UI (80); deny everything else; enable
- [ ] Install fail2ban
- [ ] Set up Pi-hole in Docker (`~/pihole/docker-compose.yml`)
- [ ] Note Pi-hole admin password from container logs on first start
- [ ] Point router DNS to 192.168.86.26 (replaces current 1.1.1.1)
- [ ] Check printer: built-in WiFi printing? If yes, skip CUPS. If no, set up CUPS in Docker.

---

## Stage 2: VPS Setup (Spaceship.com)
*Start this when Pi stage is complete and you're ready to pay.*

- [ ] Activate VPS (Standard 1: 1 AMD core, 2GB RAM, 25GB SSD, $4.90/mo)
- [ ] SSH in for first time (key already on Mac — just needs to be copied to VPS)
- [ ] Disable password SSH login
- [ ] Install Docker + Docker Compose
- [ ] Install and configure Caddy (reverse proxy + auto SSL)
- [ ] Install ufw, configure rules
- [ ] Install fail2ban

---

## Stage 3: WireGuard VPN
*Connects VPS and Pi into a private tunnel.*

- [ ] Install WireGuard on VPS
- [ ] Configure WireGuard server (wg0.conf, generate server keys)
- [ ] Open UDP port 51820 in VPS firewall
- [ ] Install WireGuard on Pi
- [ ] Configure Pi as WireGuard peer (connects outbound to VPS)
- [ ] Test tunnel is up (Pi can reach VPS internal IP and vice versa)
- [ ] Optional: set up Mac and phone as additional WireGuard clients for secure remote access

---

## Stage 4: Domain & Routing
*Point the domain at the VPS and set up subdomain routing.*

- [ ] Point elliotreich.com nameservers to Cloudflare
- [ ] In Cloudflare: create A record → VPS IP, enable orange-cloud proxy
- [ ] Configure Caddy on VPS:
  - [ ] `elliotreich.com` → personal website
  - [ ] `print.elliotreich.com` → CUPS on Pi (via WireGuard tunnel, password protected) — *if CUPS is needed*
  - [ ] `vpn.elliotreich.com` → WireGuard endpoint (DNS only, no proxy)

---

## Stage 5: Personal Website & Photography Portfolio
- [x] Built (plain HTML/CSS, no build tools)
- [x] Pushed to GitHub (`github.com/elliotreich/elliotreich.com`, main branch)
- [x] **Decision made: portfolio lives on main domain (`elliotreich.com`), not a subdomain** — photos are the primary content; About and Contact are supporting info
- [x] Rebuilt as photography-first portfolio with placeholder gallery (2026-02-19)
- [x] Cloudflare Pages connected and deployed — site live at `elliotreich-com.pages.dev` (2026-02-20)
- [x] Auto-deploy confirmed working — pushes to GitHub trigger automatic redeployment
- [x] Contact links updated: email, LinkedIn, Instagram, Pinterest, Twitter (bird icon), GitHub (2026-02-20)
- [ ] Add real bio content (intro headline + about paragraphs still placeholder)
- [ ] Curate and upload actual photos (replace placeholder grid)
- [ ] Add link to print shop once Stage 6 is underway

---

## Stage 6: NYC Photography Print Shop
*Completely separate from infrastructure above. No Pi, no VPS required — all third-party hosted.*

### Decisions to Make First (in order)
- [ ] **Confirm brand name** — working name: **City Capture** (market-facing, signals NYC photography; confirm or revise)
- [ ] **Choose quality tier:**
  - **Printful** — standard quality, strong integrations, easier setup, lower price point
  - **Prodigi** — fine art / giclée / archival quality, better for premium positioning and buyers who want the real thing; less consumer-friendly but better output
- [ ] **Evaluate Fine Art America / Pixels** as a simpler alternative — they're a marketplace AND fulfillment combined; you upload once, they sell through their own site, you can embed a store widget elsewhere; lowest overhead but lowest margin and brand control

### Printful + Etsy Setup (recommended default path after decisions above)
- [ ] Create Printful account
- [ ] Upload high-resolution source images (can serve both Etsy and own storefront from single upload)
- [ ] Select print products and formats you want to offer (sizes, paper types, framed/unframed)
- [ ] Open Etsy shop under the brand name
- [ ] Connect Printful → Etsy integration
- [ ] Build initial product catalog — **target 50–100+ listings** (Etsy's algorithm rewards volume; this is the main upfront labor)
- [ ] Optimize every listing: title, tags, description with NYC search terms (e.g. "New York City photography print," "Brooklyn wall art," "Manhattan black and white photo")
- [ ] Price listings (account for Etsy fees: ~6.5% transaction + $0.20 listing fee)
- [ ] Photograph/mockup products for listing images (Printful provides mockup generator)

### Own Storefront Setup
- [ ] Choose own storefront platform:
  - **Printful standalone storefront** — simplest, free, Printful-hosted; fine for a basic brand home
  - **Simple Shopify store** — more control, small monthly cost, same Printful integration
- [ ] Connect Printful → own storefront (same product catalog, no duplicate work)
- [ ] Add link from `elliotreich.com` portfolio to the print shop

### Launch & Early Traction
- [ ] Publish first batch of listings (even 20–30 is enough to launch, then keep adding)
- [ ] Consider low-budget Etsy ads ($1–5/day) for initial traction — Etsy's algorithm favors new listings that convert
- [ ] Monitor which subjects/images actually sell; double down on those
- [ ] Collect first reviews (critical for Etsy ranking; first few sales are the hardest)
- [ ] After initial catalog is built and reviews are in, business becomes genuinely low-maintenance

---

## Notes
- Pi model: **Raspberry Pi Zero 2 W** (confirmed)
- Pi is low-power — Pi-hole runs fine on it; avoid running many heavy services simultaneously
- Home Assistant: dropped for now (too heavy for Zero 2 W, not a priority)
- VPS provider: Spaceship.com (not yet activated)
- Domain registrar: Spaceship.com
- Cloudflare: free tier
- Website hosting: Cloudflare Pages (free) — not VPS-hosted
- All services on Pi and VPS run in Docker containers
