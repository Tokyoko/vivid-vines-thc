# Vivid Vines THC — VVVTHC

Marketing and storefront site for Vivid Vines THC. Static HTML/CSS/JS — no build step,
no dependencies. Open a file in a browser and it works.

## Structure

```
.
├── index.html        Single-page main site: age gate, hero, story, shop, lab reports, footer
├── lab-reports.html  Standalone COA page — links the actual PDF lab reports
├── coa/              Certificates of Analysis (PDFs, ~3.7 MB each)
└── README.md
```

Both HTML files are fully self-contained: CSS lives in one `<style>` block and JS in one
`<script>` block at the bottom of each file. Fonts (Playfair Display, Cinzel, Lora) load
from Google Fonts. There are no local images — visuals are CSS gradients and effects.

## Running locally

Because the pages reference PDFs by relative path, use a local server rather than
opening `index.html` off the filesystem:

```bash
python3 -m http.server 8000
```

Then visit http://localhost:8000

## Key behaviors in `index.html`

- **Age gate** (`#agegate`) — blocks the page until the visitor confirms 21+
- **Product tabs** — `#tab-thca` / `#tab-thcp` swap the shop grid
- **Cart drawer** (`#cartdrawer`) — client-side only; state is not persisted or submitted
- **`coaClick(e)`** — COA buttons with `href="#"` show a "coming soon" toast instead of
  opening a PDF. Give a button a real href and it opens normally.

## Compliance notes

Copy on the site asserts: 2018 Hemp Farm Bill compliant, ASTM D3475-20 compliant,
third-party tested, <0.3% Delta-9 THC, Permit #2026-N-2229181. Any change to product or
lab-report content should keep these claims accurate and in sync with the COA PDFs.

## Deploying

Any static host works. The site is plain files with relative links:

- **GitHub Pages** — push to a repo, enable Pages on the `main` branch, root folder
- **Netlify / Vercel** — drag the folder in, or connect the repo; no build command needed
