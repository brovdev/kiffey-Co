# AGENTS.md

## Project overview
This repository is an **HTTrack mirror** of a static website ("Booking Core" / "KIFFEY CO"), originally scraped from `sandbox.bookingcore.co`. It contains only static HTML, CSS, JS, and image assets — there is no backend, no database, and no build step.

## Structure
- `index.html` — HTTrack landing page that auto-redirects to `sandbox.bookingcore.co/login38a2.html`
- `sandbox.bookingcore.co/` — the mirrored site content (~2000 files: login, hotel/tour/car/boat/event listings, assets in `libs/`, `dist/`, `uploads/`, etc.)
- Other top-level dirs (`connect.facebook.net`, `unpkg.com`, `www.googletagmanager.com`) are mirrored third-party assets.
- `hts-cache/` — HTTrack's own cache/metadata (not served).

## Running in Base44
Served by **nginx:alpine** via `docker-compose.base44.yml` on host port 3000.
- A custom `nginx.base44.conf` runs the nginx worker as `root` because the sandbox repo directory has `0700` permissions (the default non-root worker gets 403).
- The repo root is bind-mounted read-only at `/usr/share/nginx/html`.

## Verification
- `curl -s -o /dev/null -w "%{http_code}" http://localhost:3000/` → 200
- `curl -s -o /dev/null -w "%{http_code}" http://localhost:3000/sandbox.bookingcore.co/login38a2.html` → 200
- Preview should show the Booking Core login page.

## Secrets
None required — fully static site.
