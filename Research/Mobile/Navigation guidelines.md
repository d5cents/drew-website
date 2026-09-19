# Mobile navigation

Open item from [`My Details.md`](../My%20details/My%20Details.md): *“The mobile version of the site may need to take a different approach than the tabs, for the sake of ease of navigation. We should research mobile guidelines.”*

This note is that research. Desktop can keep a tablist. Narrow viewports should not.

## Why the desktop tabs fail if they are only shrunk

[NN/g: Tabs, used right](https://www.nngroup.com/articles/tabs-used-right/):

- In-page tabs need related content, a clear selected state, and room for labels
- On small screens, **accordions often beat tabs** because tabs need horizontal space and short labels
- Vertical or cramped tab rows get overlooked

[NN/g: Basic patterns for mobile navigation](https://www.nngroup.com/articles/mobile-navigation-patterns/):

- Tab/navigation bars work when there are **few** options (they cite trouble above ~5)
- Controls must stay large enough to tap; crowding or a horizontally scrolling tab strip hides destinations (“out of sight, out of mind”)
- Persistent bars (stay on screen while content scrolls) behave differently from a one-time header that scrolls away

Drew has **three** skill destinations plus **About** in the header and **email / Instagram** in an always-visible footer. That is five chrome touchpoints, but only four compete in the header row (name, About, skill switcher). The skill trio is the primary content switcher; About is secondary (pop-up); contact is always one tap away in the footer, not a dialog.

Long labels: **Music Technology** will wrap or truncate in a three-column tab bar on a 320–390px phone. Truncation is unacceptable (information scent dies). Wrapping a tab bar into two lines looks like six controls.

## Patterns considered

### 1. Keep three tabs, stack or shrink them (not recommended)

Same IA as desktop. Fails label length and 44pt-class touch targets unless the bar becomes a full-width vertical list, at which point it is no longer “tabs.”

### 2. Native `<select>` (“View: Writing”) (acceptable fallback)

Always visible, obvious on mobile, scales if a fourth skill appears. Weak: extra tap, less scent of the other two skills, easy to style poorly. Use only if a segmented control cannot fit the three names.

### 3. Segmented control / equal-width pill group (recommended for the skill switcher)

All three labels visible, selected state obvious, still in-page (not a new URL). If “Music Technology” does not fit at the chosen type size:

- Use two lines inside each segment (“Music” / “Technology”), or
- Shorten **only on small screens** via CSS: “Writing” · “Orch.” is too cryptic; prefer “Writing” · “Orchestration” · “Tech” **only if** the panel heading still says “Music Technology and Design” immediately below

Better than abbreviation: slightly smaller type with wrapping **inside** the segment, min-height 44px.

This can still be a `tablist` in the accessibility tree (same JS as desktop) with a different layout. That is a **CSS change**, not a second component.

### 4. Accordion of three sections (recommended companion for Music Technology *content*)

[NN/g: Accordions on mobile](https://www.nngroup.com/articles/mobile-accordions/): good when users need the gist then one section; bad when a single pane is extremely long with no way back.

Use accordions **inside** Music Technology (Cohen onsite / Cohen support / Andrews onsite / Andrews support), not as a replacement for the three skills. The CV is the long page; Writing/Orchestration grids are not.

If an accordion opens a very long list, keep the subhead sticky or provide a “back to groups” control so users are not trapped mid-scroll ([NN/g accordion article](https://www.nngroup.com/articles/mobile-accordions/)).

### 5. Bottom tab bar (not recommended for v1)

App-like bar: Writing | Orchestration | Tech, with About elsewhere. NN/g notes bottom bars are persistent and familiar on iOS, but:

- Conflicts with mobile browser chrome
- About still needs a home in the chrome; contact already lives in the footer
- This site is a website, not an app with five equal destinations

Revisit only if user testing shows people cannot find the skill switcher after scrolling a long CV.

### 6. Hamburger for skills (not recommended)

[NN/g: Beyond the hamburger](https://www.nngroup.com/articles/find-navigation-mobile-even-hamburger/): hidden nav is slower; with only three skills, hiding them is unjustified. A hamburger that contains Writing/Orchestration/Tech **plus** About mixes levels; contact does not belong in a menu if the footer is always visible.

### 7. Homepage as hub (not recommended)

A landing page of three big buttons would violate “feel all like one page” and add a tap before any work is visible.

## Header on small screens

Desktop: name left, About right; footer with email and Instagram always visible.

Mobile:

- Keep **DREW NICHOLS** as the identity; it can wrap or slightly reduce size, not become a hamburger
- **About** stays a **visible text button**, not icon-only (scent; matches the brief)
- Stack if needed: row 1 name + About, row 2 skill switcher
- Make the header **sticky** so switching skills or opening About does not require scrolling to top on a long Music Technology list ([NN/g discoverability](https://www.nngroup.com/articles/find-navigation-mobile-even-hamburger/) — sticky + visible beats hidden)
- Keep the **footer sticky** (or fixed) so email and Instagram stay reachable while scrolling long CV lists — contact is not behind a dialog

Touch targets: WCAG 2.2 **24×24 CSS px** minimum ([SC 2.5.8](https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html)); aim for **44×44** on header and skill controls ([SC 2.5.5](https://www.w3.org/WAI/WCAG22/Understanding/target-size-enhanced.html), [Apple HIG](https://developer.apple.com/design/human-interface-guidelines/accessibility) 44×44 pt default on iOS).

## Dialogs on mobile

Full-screen or near-full-screen `<dialog>` for About and project details. A small centered “desktop modal” on a phone hides content. Contact stays in the footer, not in a dialog.

Requirements:

- Close control always visible (sticky inside the dialog)
- Body scroll locked behind the dialog
- Long About / CV-in-dialog (if any) scrolls **inside** the dialog
- Media: prefer platform players (YouTube/Vimeo) that already handle small screens; native `<video>` needs `playsinline` and controls

Do not open a project dialog from a card that is itself inside a tiny overlay. One overlay at a time.

## Cards on mobile

Writing/Orchestration: **single column** cards, whole card tappable (large target), thumbnail above title. Do not use a hover-only reveal — there is no hover.

## Recommended mobile IA

| Region | Mobile treatment |
| --- | --- |
| Identity | Visible title, not in a menu |
| About | Visible button → full-screen dialog |
| Email / Instagram | Footer: email copies on tap + “Copied” toast; Instagram opens profile |
| Skills | Visible 3-way segmented control (same tab semantics as desktop) |
| Writing / Orchestration | One-column cards |
| Music Technology | Intro + accordions per CV group |
| Footer | Primary contact chrome; sticky/fixed so links stay visible on long pages |

**Breakpoint:** when three skill labels cannot sit in one row at 16px with 44px min-height and 8px gaps, switch layout (stack header; allow segment labels to wrap). Exact px is a CSS task later; ~600–700px is a typical switch for this chrome.

## What not to do

- Horizontally scrolling tab strip of three items
- Icon-only nav for About or footer contact links
- Different *information* on mobile (same shows, same CV) — only different *chrome*
- A separate `mobile.html`

**Decide now:** mobile ≠ scaled desktop tabs; skills stay visible; Music Tech groups collapse; dialogs go full-viewport.

**Decide later:** exact breakpoint, whether “Music Technology” shortens, whether a bottom bar is worth a test after v1.
