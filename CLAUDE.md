# CLAUDE.md: edwinbreton.github.io

Personal site for Edwin Bretón: a short bio, an art gallery, and a blog.
A resume page may be added later. Hosted free on GitHub Pages as a user site
(repo `edwinbreton/edwinbreton.github.io`), to be served at **edwinbreton.com**.

## The concept
The whole site is a **typewritten police case file**. Everything should look
struck on a typewriter onto white, lightly textured paper. Photos and art are
**Polaroids taped onto the page**. Section breaks are **typed underscore rules**.
Keep the theme in the visual language; keep the words plain (nav says
"About / Art / Blog", not "Evidence Locker").

## Stack and rules
- Plain HTML + one CSS file. **No build step, no framework, no JS** unless a
  feature truly needs it. GitHub Pages serves the files as-is.
- `.nojekyll` tells GitHub Pages not to run Jekyll. Keep it.
- **Relative links only** (`../css/style.css`, `art.html`) so pages also work
  when opened straight from disk.
- Every `<img>` needs meaningful `alt` text.
- The repo is public. Never commit a phone number, street address, or other
  private info, because git history keeps it even after deletion.

## Files
```
index.html                 About (home): intake header, bio, recent art, latest posts
art.html                   Gallery of taped Polaroids ("exhibits")
blog/index.html            List of posts, newest first
blog/YYYY-MM-DD-slug.html  One file per post
css/style.css              All styles; design tokens at the top
images/                    Art and photos (current SVGs are placeholders)
```

## Design tokens (defined in `:root` in css/style.css)
| Token | Value | Use |
|---|---|---|
| `--paper` | #fdfcf9 | page background (plus SVG noise texture) |
| `--ink` | #24221f | body text, faded ribbon black |
| `--ink-soft` | #67625b | dates, rules, dot leaders |
| `--ribbon-red` | #a3241b | file numbers, exhibit tags, current nav item, focus ring |
| `--pen-blue` | #27386a | handwritten Polaroid captions only |
| `--manila` | #ead9a6 | text selection |

Fonts (Google Fonts): **Courier Prime** for body, **Special Elite** for
headings, **Reenie Beanie** for handwritten captions only. Don't add more.

## Components
- **Typed rule**: any `<hr>`. Rendered as underscores via `hr::before`.
- **File index (nav)**: `<nav class="file-index">`. Brackets come from CSS.
  Mark the current page with `aria-current="page"`.
- **Intake header**: `.intake` with a `<dl class="intake__fields">` of
  LABEL . . . . value rows (home page only).
- **Polaroid**: `<figure class="polaroid">` with an `<img>` and a
  `<figcaption>`. Tape is automatic. Change the angle with
  `style="--tilt: 2deg"`; keep tilts between -3deg and 3deg.
- **Exhibit tag**: `<span class="exhibit">Exhibit G</span>` inside a caption.
- **Evidence board**: `<ul class="evidence-board">` of `<li>` Polaroids.
  Angles vary automatically by position.
- **Case log**: `<ol class="log">` entries with `<time>`, `<h3>` link, summary.

## Common tasks
**Add an art piece:** put the image in `images/`, copy an `<li>` in
`art.html`, set `src`, `alt`, next exhibit letter, and caption. Newest goes
first. If it should appear on the home page, update the three items in
`.evidence-board--recent` in `index.html`.

**Add a blog post:** copy `blog/2026-10-19-opening-the-file.html` to a new
dated filename, update `<title>`, meta description, `<time>`, `<h1>`, and
body. Then add an entry to the top of `blog/index.html` and update
"Latest entries" on `index.html`.

## Roadmap (not started)
- `resume.html` in the same typed style (no phone or address).
- Custom domain: edwinbreton.com, registered at Porkbun (Oct 2026), not
  connected yet. Order per GitHub docs: (1) verify the domain in GitHub
  profile Settings > Pages (TXT record at Porkbun, keep it forever),
  (2) add the domain in repo Settings > Pages (GitHub commits the CNAME file),
  (3) at Porkbun, delete default parking records and any wildcard `*` record,
  add the four GitHub A records, four AAAA records, and `www` CNAME to
  `edwinbreton.github.io`, (4) once the cert is issued, tick Enforce HTTPS.
  Claiming on GitHub before pointing DNS prevents domain takeover.
- Possibly a simple script to generate the blog list once posts pile up.

## Before pushing (QA checklist)
- No horizontal scrolling at 360px wide on every page.
- Tab through each page; the dashed red focus ring is visible on every link.
- All links work from both `index.html` and pages inside `blog/`.
- Every new image has alt text and is reasonably sized (under ~500 KB).
