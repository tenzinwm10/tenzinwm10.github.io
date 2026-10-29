# Personal site

Static HTML and one stylesheet. No build step, no dependencies, no JavaScript.
Open `index.html` in a browser and it works.

## Files

Two pages, plus a template.

| File                 | Nav label | What it is                                     |
| -------------------- | --------- | ---------------------------------------------- |
| `index.html`         | Things    | Intro plus the timeline feed                    |
| `about.html`         | Me        | Prose page                                      |
| `template-post.html` | —         | Copy this per write-up; rename and link to it   |
| `style.css`          | —         | Every style on the site                         |
| `images/`            | —         | Figures referenced by post pages                |

The wordmark links back to `index.html`, so there is no separate "Home" item.

The only text still marked `PLACEHOLDER` is the opening paragraph of
`about.html` and the two `<meta name="description">` tags.

## Images

| File                     | Used by                            |
| ------------------------ | ---------------------------------- |
| `images/robottorso.png`  | humanoid entry, lead image          |
| `images/actuator.webp`   | humanoid entry                      |
| `images/motordriver.webp`| humanoid entry                      |
| `images/fcisar.webp`      | FC Isar Robotics entry              |
| `images/floorplan.webp`  | venture lab entry                   |
| `images/redback.webp`    | redback racing entry                |
| `images/unsw.png`        | education row (has its own alpha)   |
| `images/tum.png`         | education row (opaque white)        |
| `images/placeholder.svg` | the figure in `template-post.html`  |

Both logos were cropped to their ink bounds so they sit at comparable size in
the 80px box; the untouched originals are in `Downloads`. `tum.png` carries an
opaque white background, so its `<img>` has `class="plate"` — that adds white
padding and rounds the corners. `unsw.png` is transparent and needs no plate.
Drop the class if you ever replace `tum.png` with a transparent version.

Every `alt` string is written for a screen reader. Reword it if you swap the
picture.

## Editing

**Add a timeline entry.** Paste this at the top of the `.timeline` block —
newest first:

```html
<div class="entry" tabindex="0">
  <div class="entry-head">
    <div class="entry-title">title</div>
    <div class="entry-date">august 2026</div>
  </div>
  <p class="entry-body">one sentence.</p>
  <div class="entry-media">
    <img src="images/thing.jpg" alt="what the picture shows">
  </div>
</div>
```

Entries are plain `div`s, not links, because there are no write-up pages yet.
To make one clickable later, wrap the `.entry-title` text in an `<a>`.

**Images.** The optional `.entry-media` block holds one or more `<img>`. On a
screen wider than 1120px they sit in the empty space to the right of the column
and fade in on hover or keyboard focus; the first image runs full width and any
others sit half width beneath it. Below 1120px there is no room beside the
column, so they drop inline under the entry and are simply always visible. This
is pure CSS — there is no JavaScript on the site.

Three entry variants, in descending loudness:

- `class="entry is-featured"` — white card, black border, hard offset shadow.
  One or two per page at most, or nothing reads as emphasised.
- `class="entry is-quiet"` — translucent card, soft border.
- `class="entry"` — no card, hover tint only. Most entries should be this.

Titles truncate to a single line by design. Keep them short.

**Change the palette.** All colours are variables at the top of `style.css`.

```
--bg          #f5f4ef   page background
--fg          #000000   text, borders, shadows
--muted       #686868   dates and descriptions
--link        #595959   inline links
--rule        #d1d5db   timeline spine
--card-border #d4d3cb   quiet card outline
```

**Fonts.** The body uses the system monospace stack and the wordmark uses the
system serif stack, so there are no network requests and no flash of unstyled
text. To swap in a real serif, drop the file in `fonts/`, add an `@font-face`
rule, and change `--font-serif`.

## Preview locally

```bash
python -m http.server 4321 --directory .
```

Then open <http://localhost:4321>. You can also just double-click
`index.html` — the only reason to run a server is to match how the host will
serve it.

## Deploy

The folder is the site. Any static host works:

- **GitHub Pages** — push to a repo, enable Pages on the branch root.
- **Netlify / Vercel** — drag the folder in, or point it at the repo with no
  build command and the root as the publish directory.
- **Any web server** — copy the folder into the document root.
