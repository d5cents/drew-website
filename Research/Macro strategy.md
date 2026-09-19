# Macro development strategy

This is the plan for **how** to build Drew Nichols’ portfolio site. It is not implementation. No HTML/CSS/JS site work should start until the “decide now” list below is accepted (or explicitly overridden).

Related research (same `Research/` tree):

- Copy and inventory: `My details/My Details.md`
- Hosting: `Hosting/GitHub Pages and static hosts.md`
- Stack: `Stack/Vanilla HTML CSS JS.md`
- IA: `Content and IA/Site structure.md`
- Mobile: `Mobile/Navigation guidelines.md`

## Constraints (non-negotiable unless Drew changes them)

1. **Static hosting**, GitHub Pages first (Cloudflare Pages / Netlify are compatible escape hatches, not parallel builds).
2. **Vanilla HTML/CSS/JS** — no framework, no required bundler, no CMS.
3. **One page** with dialogs for About, Contact, and project detail; three skill modes.
4. **Copy is unfinished.** The site must tolerate missing thumbnails, missing demos, and withheld titles.
5. **Research stays in git** and is not the published website. Implementation (later) lives in a publish folder (`docs/` or `site/`), not mixed into these notes as a second brief.

## How research feeds implementation

| When someone later builds… | They read… | They do not… |
| --- | --- | --- |
| Deploy / DNS / `CNAME` | Hosting | Invent Netlify-only features for v1 |
| `index.html` structure | Content and IA + My Details | Invent extra nav (blog, shop, separate socials page) |
| CSS layout / breakpoints | Mobile + Stack | Shrink desktop tabs and call it responsive |
| Dialog and tab JS | Stack (APG, `<dialog>`) | Add a UI library for modals/tabs |
| Card text | My Details, then IA “public vs hold” | Publish `mixed by ________` or a private pitch |
| Audio/video | Hosting (off-site embeds) + WCAG notes in Stack | Commit LFS media for Pages |

`My Details.md` remains the **content inventory**. Research docs remain **decisions**. Site files (future) remain **presentation**. If those three disagree, update them in that order: inventory → decision → markup.

## Sequencing (implementation comes after this document, in this order)

0. **This research phase (current).** Hosting, stack, IA, mobile, open questions. Stop. No pages.

1. **Content gate (still not code).** Drew (or an editor) marks each Writing/Orchestration title **public / hold**, fills one-line credits, and supplies a shortened About. Mixer blanks stay omitted.

2. **Information skeleton.** One `index.html` with header, three panels, empty-or-thin cards, dialog shells, no visual branding pass. Hash URLs. Verify with JS disabled (all sections still readable).

3. **Behavior.** Tab keyboard pattern; `<dialog>` focus/escape; hash sync; one dialog at a time.

4. **Layout CSS.** Desktop grid + mobile segmented control + Music Technology accordions. Sticky header. Touch targets.

5. **Publish.** GitHub Pages from the site folder only; `.nojekyll`; relative URLs.

6. **Media.** Embed demos as URLs appear; captions/transcripts with the files, not as a retrofit year later.

7. **Visual design.** Type, color, motion. After the skeleton works, so design is not fighting missing IA.

8. **Optional later.** Custom domain; Cloudflare if bandwidth/previews matter; JSON/Eleventy if card HTML becomes unmaintainable; contact form only if `mailto:` is not enough.

Do not start at step 7. Do not introduce a framework at step 2 because the About text is long.

## Decide now vs later

### Decide now (blocks a coherent v1)

- Host: **GitHub Pages**, publish folder separate from `Research/`
- Stack: **HTML/CSS/JS**, `<dialog>` + ARIA tabs, no npm app
- Chrome: **About** and **Contact** (not “Socials”)
- Skills: three modes; Music Technology is a **CV**, not cards
- Mobile: **visible** skill switcher (segmented tabs), not hamburger, not a second site
- Media: **not** in Git LFS; embeds off-site
- Contact: **mailto + Instagram**, no form
- Public writing v1: **The Likely Heroes** and **McCobb Mortality Services**; others only with a public sentence
- Unknown credits: **omit**, don’t placeholder-underline

### Decide later (does not block the skeleton)

- Custom domain name and DNS
- Cloudflare vs staying on Pages
- Visual identity (type, palette, photography)
- Exact mobile breakpoint and whether “Music Technology” shortens
- Which Alyssa Payne / BMI / Muppets / Monte Cristo items ship in v1
- Whether older shows in the bio get cards
- Thumbnails and demo URLs
- Captions workflow per video
- Sass/TypeScript/Eleventy
- Analytics

## Risks if this order is ignored

- Designing a desktop tab bar first makes mobile a retrofit (the brief already flagged this).
- Putting audio in the repo hits Pages size/LFS limits and stalls launch.
- Waiting for complete copy stalls a site that is allowed to be thin.
- A framework or Netlify form in v1 couples the HTML to a vendor the hosting research said to avoid.

## Done when (for this research-only phase)

- Hosting, stack, IA, and mobile notes exist with sources, options, and a recommendation.
- This strategy names sequence, constraints, and now/later splits.
- No site files have been added.

Later implementation is done when a visitor on a phone can open Contact, switch skills, open a project dialog, and reach Music Technology groups without a desktop tab bar.
