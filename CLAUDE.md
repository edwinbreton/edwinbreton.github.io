# CLAUDE.md: edwinbreton.github.io

Personal site for Edwin Bretón: a short bio, an art gallery, and a blog.
A resume page may be added later. Hosted free on GitHub Pages as a user site
(repo `edwinbreton/edwinbreton.github.io`), to be served at **edwinbreton.com**.

## The concept
The whole site is a **typewritten police case file**. Everything should look
struck on a typewriter onto white, lightly textured paper. Photos and art are
**Polaroids taped onto the page**. Section breaks are **typed underscore rules**.
Keep the theme in the visual language; keep the words plain (nav says
"About / Art / Blog", not "Evidence Locker"; headings say "About", "Recent
art", "Latest posts", not "Statement" or "Recent evidence").

On a phone, the sheet fills the screen edge to edge. Past phone width it
reads as a literal page of paper resting on a desk (`--desk`), and widens to
fill most of the viewport rather than staying capped at a fixed column width;
see the `min-width` query at the end of `style.css`.

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
index.html                 About (home): intake header, bio, recent art
                           (no latest-posts section until there's a real post)
art.html                   Gallery of taped Polaroids
blog/index.html            List of posts, newest first
blog/YYYY-MM-DD-slug.html  One file per post
css/style.css              All styles; design tokens at the top
images/                    Art and photos (art-02.svg is still a placeholder,
                           used by the sample blog post)
```

## Design tokens (defined in `:root` in css/style.css)
| Token | Value | Use |
|---|---|---|
| `--paper` | #ffffff | `.sheet` background: literally white (plus SVG noise texture) |
| `--ink` | #24221f | body text, faded ribbon black |
| `--ink-soft` | #67625b | dates, rules, dot leaders |
| `--ribbon-red` | #a3241b | current nav item, focus ring |
| `--pen-blue` | #27386a | handwritten Polaroid captions only |
| `--manila` | #ead9a6 | text selection |
| `--desk` | #dcd7c9 | page background past phone width, behind `.sheet` |

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
  `style="--tilt: 2deg"`; keep tilts between -3deg and 3deg. Square crop.
- **Photo**: `<figure class="polaroid photo">`, same markup as a Polaroid
  but keeps the image's own proportions instead of a square crop. Use it
  for art a square crop would cut into (a two-page spread, two subjects
  side by side); otherwise use a plain Polaroid.
- **Evidence board**: `<ul class="evidence-board">` of `<li>` Polaroids.
  Angles vary automatically by position. (Name is a CSS class only now;
  no "Exhibit" labels or file numbers show on the page anymore.)
- **Case log**: `<ol class="log">` entries with `<time>`, `<h3>` link, summary.

## Common tasks
**Add an art piece:** put the image in `images/`, copy an `<li>` in
`art.html`, set `src`, `alt`, and caption. Newest goes first. If it should
appear on the home page, update the three items in `.evidence-board--recent`
in `index.html`.

**Add a blog post:** copy `blog/2026-10-19-opening-the-file.html` to a new
dated filename, update `<title>`, meta description, `<time>`, `<h1>`, and
body. Then add an entry to the top of `blog/index.html`, and add back a
"Latest posts" section on `index.html` (removed for now; copy its old shape
from `blog/index.html`'s intro + `.log` pattern).

`blog/2026-10-19-opening-the-file.html` itself is sample content, not a real
post: kept only as the copy-template above and as a demo of a Polaroid taped
into an article, but deliberately unlinked from `blog/index.html` and
`index.html` so it doesn't show as a real entry. Once there's a first real
post, this file and `images/art-02.svg` (the placeholder art it uses) can go.

## Roadmap (not started)
- `resume.html` in the same typed style (no phone or address).
- Custom domain: edwinbreton.com, registered at Porkbun (Oct 2026). Connected
  and live: domain verified on GitHub, CNAME file committed, Porkbun DNS
  points at GitHub's A/AAAA records plus a `www` CNAME to
  `edwinbreton.github.io`, and Enforce HTTPS is on.
- Possibly a simple script to generate the blog list once posts pile up.

## Before pushing (QA checklist)
- No horizontal scrolling at 360px wide on every page.
- Tab through each page; the dashed red focus ring is visible on every link.
- All links work from both `index.html` and pages inside `blog/`.
- Every new image has alt text and is reasonably sized (under ~500 KB).
