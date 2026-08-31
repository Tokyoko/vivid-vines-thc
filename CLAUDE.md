# Vivid Vines THC — working notes for Claude

Static site, no build step, no package manager. Edit HTML directly.

## Conventions

- **Self-contained pages.** Each HTML file carries its own `<style>` and `<script>`.
  Keep it that way unless we deliberately split assets out — don't introduce a bundler,
  framework, or external CSS file for a one-off change.
- **Design tokens** live in the `:root` block at the top of each file's `<style>`
  (`--gold`, `--deep`, etc.). Change colors there, not at call sites.
- **`.reveal` class** — elements with it fade in via IntersectionObserver on scroll.
  New sections should use it to match the rest of the page.
- Two files duplicate their COA markup and styling (`index.html` §`#lab-reports` and
  `lab-reports.html`). A change to lab-report content usually needs to happen in both.

## Verifying changes

Serve locally and check in a browser — relative PDF links break under `file://`:

```bash
python3 -m http.server 8000
```

Check the age gate, the THCA/THCP tab swap, the cart drawer, and that COA links open
their PDFs.

## Known issues / open work

- `index.html` has no link to `lab-reports.html`. The nav's "Lab Reports" points at the
  in-page `#lab-reports` anchor, so `lab-reports.html` is unreachable from the homepage.
- All 6 COA buttons inside `index.html` use `href="#"` and fire the "coming soon" toast,
  even though 3 real THCP COA PDFs exist in `coa/`. The THCA COAs genuinely don't exist yet.
- COA PDFs are ~3.7 MB each and committed to the repo. Fine for now; if they multiply,
  move them to object storage or Git LFS.

## Content that must stay accurate

Compliance claims (Hemp Farm Bill, ASTM D3475-20, <0.3% Delta-9, permit number) and
potency figures appear in body copy. Don't edit these to fit a layout — they're legal
claims that must match the COAs.
