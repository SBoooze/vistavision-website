# VISTA VISION

A single-page retro CRT-TV website for the indie rock band **VISTA VISION**.
Inspired by the lo-fi, 2000s-era aesthetic of bands like The Strokes, with a
cursive neon-tube logo nodding to *Blue Velvet* and *Brazil*.

The site is mostly a single `index.html` — vanilla HTML, CSS and JavaScript.
News posts are separate markdown files in `posts/` that get fetched and
rendered at runtime.

## Channels

- **CH 1 — HOME**: Cursive neon logo. After 10s the band photo and social
  icons fade in.
- **CH 2 — LIVE**: Tour dates with a glowing marquee.
- **CH 3 — MERCH**: ASCII-art T-shirt and Vinyl record with mailto: buy
  links.
- **CH 4 — NEWS**: Newsletter signup + the latest markdown posts from
  `posts/`.
- **CH 5 — CONTACT**: One big button that opens the user's email client.

Keyboard shortcuts: press `1`–`5` to switch channels.

## Editing content

### Adding a news post

1. Drop a new markdown file into `posts/`. Name it `YYYY-MM-DD-slug.md`.
2. Frontmatter format:

   ```md
   ---
   title: Your Title
   date: 2026-06-01
   ---

   Body text. **Bold** and *italic* and [links](https://example.com) work.

   - Lists work too
   - Like this
   ```

3. Add the path to the `POSTS` array near the bottom of `index.html`:

   ```js
   const POSTS = [
     'posts/2026-06-01-your-slug.md',
     ...
   ];
   ```

### Newsletter

The signup form posts to [FormSubmit](https://formsubmit.co/) — no signup
required, but you need to confirm the address once. In `index.html`, replace:

```html
<form ... action="https://formsubmit.co/hello@vistavision.fm" ...>
```

with your own email.

### Contact button

Update the `mailto:` URL on the `#contactBtn` link in `index.html`.

### Social links

Already wired to:
- SoundCloud: `https://on.soundcloud.com/Ii0FRxS4XfAWE6CjOm`
- Instagram: `https://www.instagram.com/vistavisionband/`
- TikTok: `https://www.tiktok.com/@vistavisionband`
- Facebook: `https://www.facebook.com/profile.php?id=61584714924639`

### Band photo

`assets/band_pic.jpg` — swap it out, keep the filename, or update the
`<img src>` in `index.html`.

## Local preview

The markdown posts are fetched via `fetch()`, which does **not** work from
the `file://` protocol. Run a static server:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

(You'll see an "OFFLINE PREVIEW" fallback in the NEWS channel if you open
`index.html` directly.)

## Deploy to GitHub Pages

### Option A — Branch deploy

1. Push this repo to GitHub.
2. **Settings → Pages → Build and deployment → Source**: choose **Deploy
   from a branch**, pick `main` / `/ (root)`.
3. Live at `https://<your-user>.github.io/<repo-name>/` within a minute.

### Option B — GitHub Actions (already wired up)

`.github/workflows/pages.yml` deploys automatically on every push to `main`.

1. Push to GitHub.
2. **Settings → Pages → Source**: choose **GitHub Actions**.

### First push

```bash
git init
git add .
git commit -m "Initial commit — VISTA VISION CRT site"
git branch -M main
git remote add origin git@github.com:<your-user>/<repo-name>.git
git push -u origin main
```

## Files

```
.
├── .github/workflows/pages.yml   # Auto-deploy workflow
├── .nojekyll                     # Skip Jekyll (lets /posts/*.md serve as text)
├── .gitignore
├── README.md
├── assets/
│   └── band_pic.jpg              # Used on the home screen
├── posts/                        # Markdown posts, fetched by CH 4
│   ├── 2026-05-12-back-in-the-studio.md
│   ├── 2026-04-22-spring-tour-announced.md
│   └── 2026-03-08-room-12-pressing.md
└── index.html
```
