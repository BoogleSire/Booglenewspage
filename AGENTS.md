# Boogle TV News — Blogger Theme

This repo contains Blogger XML theme files for **Boogle TV News** (boogletvnews.blogspot.com).

## What's here
- `boogletvnews-theme-upgraded.xml` — the upgraded, professional news theme (the deliverable). Install via Blogger → Theme → Edit HTML → paste.
- `booglenew-display-bugs-fixed.xml` — the original theme (kept as backup; do not delete).
- `preview/` — a static HTML rendering of the theme (homepage + article) with mock content, served on port 3000 so the design is visible without Blogger.

## Running the preview
```
docker compose -f docker-compose.base44.yml up -d
```
Serves `preview/` via nginx on **port 3000**. Open the homepage at `/` and the article view at `/post.html`.

This is a static preview only — Blogger data tags (`data:post.*`, `b:loop`, etc.) only resolve inside Blogger. The preview uses mock content to show the design.

## The actual theme is NOT a runnable web app
The deliverable is the XML file uploaded to Blogger. There is no backend, database, or build step. Do not try to "run" the XML with docker — only the `preview/` folder is served.

## Key facts for editing the theme
- Based on Blogger's **Indie** 2nd-gen template (`b:templateUrl='indie.xml'`, layoutsVersion 3).
- Blog1 widget uses `super.main` and overrides only `post`, `postBody`, `postCommentsAndAd`, `headerByline`, `postFooter`, `postLabels`, etc. Standard Blogger includables are inherited from defaults.
- Breaking-news ticker and related-posts are populated client-side via the Blogger JSON feed (`feeds/posts/default?alt=json`) — no hard-coded content.
- Navigation links and Sports dropdown URLs are hard-coded to the exact page URLs the user provided; do not change them.
- Footer social links are intentionally left as "needs configuration" placeholders — do NOT invent social URLs.
