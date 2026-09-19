# Stack: vanilla HTML, CSS, and JavaScript

Drew’s constraint: **plain HTML/CSS/JS, no framework** unless this repo already argued for one. It does not. README and `Research/My details/` describe a one-page portfolio with header, pop-ups, and three content panes. That maps cleanly onto HTML landmarks, CSS layout, and a small script. A framework would add a build, a lockfile, and hosting complexity the hosting research is trying to avoid.

## What “vanilla” means here

| Layer | Choice | Out of scope |
| --- | --- | --- |
| Markup | HTML5, one `index.html` (includes allowed later *only* if a tiny static preprocessor is introduced) | React/Vue/Svelte, JSX, Markdown-to-site generators |
| Style | One or few `.css` files. CSS custom properties, flex/grid, media queries | Tailwind-as-build, CSS-in-JS, design-system packages |
| Behavior | One or few `.js` files, no bundler required | npm app, TypeScript *required*, jQuery |
| Content | Copy sourced from `Research/My details/`; HTML updated by hand | Headless CMS, JSON fetched at runtime from a backend |
| Media | `<audio>` / `<video>` or iframe embeds | Self-hosted streaming stack |

A **static site generator** (Jekyll, Eleventy, 11ty, Hugo) is still “HTML out,” but it is a second toolchain and GitHub Pages’ Jekyll defaults. It is not justified until copy volume or repeated card markup becomes painful. **Defer.** If includes become painful, Eleventy is the least-surprising later add — not v1.

## Native platform features that replace libraries

The brief’s “pop-ups” and “tabs” are solved by browser APIs, not UI kits.

### Pop-ups → `<dialog>`

Use the HTML [`<dialog>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/dialog) element and [`showModal()`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLDialogElement/showModal). Baseline: widely available since March 2022; Safari/iOS 15.4+ ([Can I use: dialog](https://caniuse.com/dialog)).

Browser-provided behavior ([WCAG technique H102](https://w3c.github.io/wcag/techniques/html/H102), [ARIA APG Dialog (Modal)](https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/)):

- Focus moves into the dialog
- Background becomes inert
- Escape closes (modal)
- `::backdrop` for the dimmer
- Focus should return to the opener on close (verify; do not assume every browser/version restores perfectly)

Still required in author CSS/JS: visible close control, labelled dialog (`aria-labelledby` to the heading), scroll inside long About / project bodies, and **no nested modals**.

About, Contact, and project cards should share **one dialog pattern**, with content swapped or with one dialog per concern. Do not invent a second “lightbox” library.

### Skill switcher → tabs on desktop, not fake links

Writing / Orchestration / Music Technology is in-page content switching, not three websites. Follow [ARIA APG Tabs](https://www.w3.org/WAI/ARIA/apg/patterns/tabs/): `tablist` / `tab` / `tabpanel`, arrow keys inside the list, Tab leaves the list into the panel. Automatic activation is fine if all three panels are already in the DOM (they should be, for no-JS readability).

If JavaScript fails, all three sections should still be reachable as stacked headings (progressive enhancement). Hide-with-CSS-only after JS runs.

Mobile should **not** squeeze three equal tabs into a narrow header. See `Research/Mobile/`.

### One-page feel vs. real URLs

“Feel all like one page” is a UX instruction, not “never change the URL.” Deep links help booking directors share a show. Recommended later implementation:

- `#about`, `#contact`, `#writing`, `#orchestration`, `#music-technology`
- Optional `#writing/the-likely-heroes` to open a project dialog

`hashchange` is enough; History API is optional. GitHub Pages cannot 301 old paths, so **do not ship multi-file routes in v1** (`/writing.html`) unless Drew later wants crawlable per-show pages.

## CSS approach

- **Mobile-first media queries.** The brief already flags mobile as a different IA, not a shrunk desktop.
- **Custom properties** for type scale, spacing, and a small color set — decided at visual-design time, not now.
- **No CSS framework.** A reset/normalize of a few dozen lines is enough.
- Prefer `grid` for the card gallery; `flex` for the header.
- Respect `prefers-reduced-motion` when opening dialogs.

Visual identity (typefaces, color, “theatre poster vs. résumé”) is **not** a stack decision. It is a later design pass. Do not install webfont kits until that pass; system or one licensed/display face is enough.

## JavaScript scope (keep it small)

v1 script should only:

1. Open/close dialogs and manage focus
2. Switch skill panels and update `aria-selected` / `hidden`
3. Sync hash ↔ UI
4. Maybe pause media when a dialog closes

It should **not**:

- Render the About essay from a JS string (copy lives in HTML so it is readable and crawlable)
- Lazy-load a component framework
- Depend on a build

Optional later: a tiny content file (`projects.json`) **only if** card fields stabilize and HTML duplication hurts. That is data, not a framework. Until credits and descriptions exist, duplicated HTML is cheaper than a schema.

## Accessibility bar for this stack

Target **WCAG 2.2 Level AA** as a working bar (common, testable, not AAA-complete). Relevant bits:

- Text alternatives and media ([WCAG 2.2 Guideline 1.2](https://www.w3.org/TR/WCAG22/)): captions on videos; transcripts for audio-only demos ([WebAIM checklist](https://webaim.org/standards/wcag/checklist))
- Keyboard: tabs and dialogs as above
- Target size: 24×24 CSS px minimum ([SC 2.5.8](https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html)); prefer ~44×44 for header/tab controls ([SC 2.5.5](https://www.w3.org/WAI/WCAG22/Understanding/target-size-enhanced.html), Apple HIG 44×44 pt on iOS)

Theatre portfolio visitors include casting, MD, and design people on phones in rehearsal. Keyboard and captions are not optional polish.

## Hosting interaction

Vanilla files deploy to GitHub Pages, Cloudflare Pages, or Netlify unchanged. **Do not** introduce `package.json` “just in case.” If someone later wants TypeScript or Sass, that is a new decision with a build and a Pages Action.

## Recommendation

| Decision | Choice |
| --- | --- |
| Stack | Hand-authored HTML + CSS + JS |
| Pop-ups | `<dialog showModal()>` |
| Skill UI (desktop) | ARIA tabs, three panels in one document |
| Routing | Hash fragments on one `index.html` |
| Build | None for v1; `.nojekyll` if publishing raw files |
| Dependencies | Zero runtime libraries unless a measured gap appears (none identified) |

**Do not decide now:** typefaces, color, whether cards become JSON, whether Eleventy is introduced after the tenth show page.
