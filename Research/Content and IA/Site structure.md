# Content and information architecture

Source of truth for copy: [`Research/My details/My Details.md`](../My%20details/My%20Details.md). That file is still a brief-plus-bio, not finished website copy. IA should assume **more shows, more credits, and more media will arrive after the first HTML exists.**

## What Drew already specified

Global:

- One-page feel
- Header: **DREW NICHOLS** left; **About** and **Contact** right
- About / Contact open as pop-ups (not new pages)
- Below the header: three modes — **Writing**, **Orchestration**, **Music Technology**
- Writing and Orchestration: **cards** (thumbnail, short text) → pop-up with more copy and audio/video
- Music Technology: **CV list**, not cards
- Mobile “may need a different approach than the tabs”

Audience (inferred from the bio, not stated as a persona workshop):

- Directors, producers, MDs, programmers, and peers looking up a writer/orchestrator/programmer
- They arrive busy; they want **proof of work** (shows, demos) faster than a long bio

That argues for: name + skill switcher first; About as optional context; Contact always one tap away.

## Proposed page map (still one HTML document)

```
[ Header ]
  Drew Nichols          About    Contact
[ Skill switcher ]      Writing | Orchestration | Music Technology
[ Main panel ]
  Writing ........... card grid
  Orchestration ..... card grid
  Music Technology .. grouped CV
[ Footer, optional ]    email · Instagram · BMI / Time Step one-liners
```

Dialogs (overlays, not routes):

| Dialog | Opens from | Content |
| --- | --- | --- |
| About | Header | Career narrative from My Details (edited down) |
| Contact | Header | Instagram, email; label as Contact (see naming below) |
| Project | A writing or orchestration card | Title, collaborators, status, longer blurb, media, links |

No fourth top-level nav item. Socials live inside Contact. Memberships (BMI, Time Step) can sit at the end of About, not in the header.

## Naming inconsistencies to resolve **now**

These are small and block UI labels:

1. Header says **“Contact”**; the section heading says **“SOCIALS/CONTACT.”** Use **Contact** in the chrome. Put Instagram + email inside. “Socials” is not a second destination.
2. Brief intro lists skills as “Orchestrating/Producing” and “Music Technology and Design”; tabs say **ORCHESTRATION** and **MUSIC TECHNOLOGY.** Use the **tab labels** on the site. The longer phrases can appear inside the panel intro sentence.
3. “Orchestraton” typo in the brief → **Orchestration** everywhere in UI.

## Card model (Writing and Orchestration)

Copy is incomplete (missing mixer credit, missing blurbs, missing media). Do **not** wait for perfect copy. Freeze a **card schema** so HTML can ship with placeholders:

| Field | Required for v1 card? | Notes |
| --- | --- | --- |
| Title | Yes | Canonical show/song name |
| One-line role/credit | Yes | e.g. “Book/music/lyrics” vs “orchestration / production” |
| Status | If known | Workshop-ready, rewrite in progress, pitch, benefit, assignment |
| Thumbnail | Placeholder OK | 16:9 or 1:1 — pick one ratio and keep it |
| Short description | Placeholder OK | 1–2 sentences on the card |
| Long description | Dialog; can equal short at first | |
| Collaborators | Dialog | Jessie Kleinman, Ryan Kleinman, Alyssa Payne, Emily Boyd Dahab, etc. |
| Media | Dialog; optional | External URL + type (audio/video) |
| Missing facts | Internal only | e.g. Crush mixer still `_ _ _ _` — **do not publish blank credits** |

**Rule:** If a credit is unknown, omit the line. Do not ship “mixed by ________.”

### Writing inventory (from My Details)

Treat these as first-wave cards. Order is a **now** decision (recommendation below).

| Working title | What we know | Suggested status chip | v1 card? |
| --- | --- | --- | --- |
| The Likely Heroes | With Jessie & Ryan Kleinman; four informal book readings; song demos; ready for formal reading/workshop | Ready for workshop | Yes — lead |
| McCobb Mortality Services | Own musical; radio-musical podcast + OCR; rewrite with Emily Boyd Dahab; workshop again within a year | Rewrite in progress | Yes |
| The Good Place | BMI workshop demos | Workshop demos | Yes if a sentence + audio exist; else hold |
| The Muppets | Pitch | Pitch | Only with a one-liner Drew is willing to show publicly |
| Count of Monte Cristo | Podcast theme and scored moments | Media work | Yes as a small card if audio exists |

**Recommended writing order:** Likely Heroes → McCobb → then only items that have a public-facing sentence. Hide pitch work until Drew confirms it should be public.

Also mentioned in About but not in the Writing list: *Invincible*, *Rathskeller*, *Beyond Perfection*, *Of Leto*, *The Light Rail*. Those can stay in About (credits in prose) until they get cards. **Do not silently drop them from the bio** when shortening About.

### Orchestration inventory

Song/video credits for Alyssa Payne plus “Higher” (Time Step). These are **tracks**, not full musicals — card chrome should look like recordings (title + artist), not like a Broadway show bible.

Missing: mixer on “Crush”; video URL for the Theatrely Tony piece; audio for the rest.

**v1:** one card per listed title, short credit line “orchestration / production (with Alyssa Payne)” where true; “Higher” as “dance arrangement, Time Step Symposium.” Add media when URLs exist.

Full-musical orchestration credits currently live only in the About paragraph (*Of Leto*, *The Light Rail*, *Invincible*, *McCobb*, benefits). Either:

- Add them as orchestration cards later, or
- Keep them in About until there is a demo

Recommend: **About holds the long-form orchestration résumé; the Orchestration tab is the listen/watch grid.** That avoids an empty-feeling tab while tracks are still gathering files.

### Music Technology inventory

This is a **long CV**, already grouped:

1. Intro paragraph (intersection of MD, keys, orchestration, programming)
2. Associate for Randy Cohen Keyboards — onsite/programming list
3. Same — installation/support list
4. Associate/Assistant for Stuart Andrews — onsite
5. Same — installation/support

Keep those five chunks. Do not turn 40+ titles into cards. On desktop, two subheads per employer is enough. On mobile, those subheads become **accordions** (see Mobile research).

Watch for spelling/normalization later (Cincinnati, Theatre, 12th Night vs Twelfth Night, etc.). Copy-edit pass is **after** structure, not a blocker.

## About dialog — copy still too long for a pop-up

The About block is one dense paragraph plus two project updates plus affiliations. For a modal:

1. **Lead** (2–3 sentences): who Drew is (writer / orchestrator / keyboard programmer) and the childhood hook *or* the ASU *Invincible* hook — not both at full length
2. **Selected work** as a short list, not a run-on sentence
3. **Current:** McCobb rewrite; Likely Heroes workshop-ready
4. **Affiliations:** Time Step, BMI Advanced

Keep the full paragraph in `My Details.md` as the canonical essay. The site gets an **edited About**. Editing is a content task before implementation, not something CSS can fix.

## Contact dialog

Keep it short:

- Email: `DrewNicholsMusic@gmail.com` (use a `mailto:` link)
- Instagram: [@drewcomposed](https://instagram.com/drewcomposed)

No contact form in v1 (see Hosting). Optional later: representation / location. Not in the brief.

## Incomplete copy: IA implications

| Risk | IA response |
| --- | --- |
| Cards without descriptions | Title + role + status chip is a valid card. Empty “lorem” is worse than a thin card |
| Cards without thumbnails | Shared fallback (initials, or a single site pattern) — do not delay the grid |
| Cards without audio | Dialog still useful as a credit sheet; “Demo forthcoming” only if Drew wants that language |
| About still in draft | Ship dialog with the edited short bio; do not block the grid |
| New shows appear often | Card grid must be **append-only HTML** (or later JSON). No IA that assumes a fixed five writing projects |
| Music tech list grows every season | Grouped lists + accordion; not a new tab per employer |
| Public vs private (Muppets pitch, in-progress rewrite) | Explicit **show/hold** flag in My Details when Drew updates it |

**Content workflow:** update `My Details.md` first, then the HTML. The research folders are not a second copy of the bio.

## SEO and sharing (light)

A one-page site can still have:

- `<title>` + meta description naming musical theatre writer / orchestrator / keyboard programmer
- Open Graph tags later for link previews
- Hash URLs so “here is Likely Heroes” is pasteable

Do not create a blog or news IA. Nothing in the brief asks for it.

## Recommendations (IA)

1. One document, three skill panels, two header dialogs, project dialogs from cards.
2. Writing tab leads with workshop-ready and current work; do not auto-publish every title in the notes.
3. Orchestration tab = playable/visible pieces; prose résumé stays in About until there are demos.
4. Music Technology tab = grouped CV, not cards.
5. Contact chrome label; omit unknown credits rather than blanks.
6. Treat `My Details.md` as inventory + long bio; site copy is a subset with a status per item.

**Decide now:** chrome labels; card schema; which writing titles are public in v1; Music Tech as list not cards.

**Decide later:** final About edit; thumbnail art; demo hosts per project; whether *Invincible* et al. get their own cards; footer contents.
