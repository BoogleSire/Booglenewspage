# Boogle TV News — Base44 Dev Environment

## What this repo is
This is a **Blogger.com theme** project, not a standalone web application. The core files are Blogger XML templates (`booglenew-display-bugs-fixed.xml`, `booglenew-bbc-responsive.xml`, etc.) plus a standalone CSS file (`bbc-responsive-additions.css`). Blogger templates use proprietary tags (`<b:skin>`, `<b:widget>`, `<data:...>`, `<b:loop>`) that only render inside Blogger's engine — they cannot be served directly as a web page.

## How the preview works
Since the theme can't run on its own, a static HTML preview was built at `preview/index.html`. It:
- Extracts the theme's CSS from the `<b:skin>` CDATA block into `preview/assets/theme.css` (appended with `bbc-responsive-additions.css`).
- Reproduces the theme's HTML structure (breaking news bar, header/nav, featured banner, post grid, sidebar, footer) with sample content replacing Blogger data tags.
- Includes the theme's JavaScript (mobile menu toggle, sports submenu, scroll progress bar, back-to-top button).

## Running it
```bash
docker compose -f docker-compose.base44.yml up -d
```
Serves the static preview on **port 3000** via nginx. No build step, no dependencies, no secrets required.

## Editing the theme
- To change the **preview appearance**, edit `preview/index.html` or `preview/assets/theme.css`.
- To change the **actual Blogger theme**, edit the XML files (e.g. `booglenew-display-bugs-fixed.xml`). After editing the XML, re-extract the CSS into `preview/assets/theme.css` to keep the preview in sync.

## Verifying
- `curl -sf -H "Host: external-preview.example.com" http://localhost:3000/` should return the HTML.
- The preview should show the Boogle TV News homepage layout with header, featured banner, post grid, sidebar, and footer.
