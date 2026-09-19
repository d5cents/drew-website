# Media: Wistia video hosting and chapters

**Decision (Drew):** Host portfolio **video** on [Wistia](https://wistia.com/), not in the git repo and not primarily on YouTube/Vimeo for these embeds.

**Pattern:** Related clips are **one uploaded video** in Wistia (e.g. the Alyssa Payne orchestration/production set). The site still shows **separate cards or links** per song/piece; each link **jumps to a chapter** (timestamp) inside that single embed.

GitHub Pages remains the site host; Wistia is only the video CDN/player ([Hosting research](../Hosting/GitHub%20Pages%20and%20static%20hosts.md)).

## Why Wistia fits this site

| Need | Wistia | YouTube embed on Pages |
| --- | --- | --- |
| Branded player, no ads | Yes (Free shows Wistia branding; paid can remove) | Ads, YouTube chrome |
| Chapters on timeline | Built-in + AI chaptering ([Chapters help](https://support.wistia.com/en/articles/8283768-chapters-in-your-video)) | YouTube chapters (description + timeline) but less control in your modal |
| Jump to time from **your** page links | [Embed Links](https://docs.wistia.com/docs/embed-links) without custom JS | Possible with `?t=` but not the same single-embed chapter workflow |
| Captions / transcript | Automated transcripts/captions on paid tiers; Free includes basics per [pricing](https://wistia.com/pricing) | Auto captions, less control |
| Analytics | Per-embed and heatmaps (plan-dependent) | YouTube Studio only |

Audio-only writing demos can still use **SoundCloud, Bandcamp, or native `<audio>`** pointing at small files or another host. This note is **video-first**.

## Plan and limits (check before uploading a long reel)

As of 2026, Wistia’s **Free** plan ([pricing](https://wistia.com/pricing)): **25 GB storage**, **200 GB/month bandwidth**, **1 user**, Wistia branding on the player. Free accounts **cannot** buy extra storage/bandwidth; playback or uploads stop at the cap ([storage](https://support.wistia.com/en/articles/13944217-understanding-storage-limits), [bandwidth](https://support.wistia.com/en/articles/8264552-account-usage-and-bandwidth)).

A single compiled Alyssa reel plus a few writing videos is usually fine on Free. If the library grows (many full-length demos), revisit Business or trim/archive in Wistia.

## One video, many entry points (Alyssa set)

### In Wistia (authoring)

1. **Export one file** (or use Wistia’s editor) that concatenates the Alyssa-related pieces in a fixed order. Order should match how you want chapters to read top-to-bottom on the site.
2. Upload to Wistia. Note the media **hashed ID** (from Embed & Share), e.g. `a62xl92vp9`.
3. **Chapters** in Customize → Chapters ([help](https://support.wistia.com/en/articles/8283768-chapters-in-your-video)): title + start time per segment. Optional: AI chaptering from transcript.
4. Add **captions** (upload or auto) for WCAG; chapter titles are not a substitute for captions on dialogue/lyrics.
5. Save player customizations. Use the **standard** embed (full control bar). Simplified/oEmbed players may hide chapter markers ([chapters FAQ](https://support.wistia.com/en/articles/8283768-chapters-in-your-video)).

Suggested chapter titles (align with [`My Details`](../My%20details/My%20Details.md); adjust times when the master is cut):

| Chapter title (example) | Source in brief |
| --- | --- |
| Broadway’s Never Been More Alive | Theatrely / Tony Awards piece |
| Crush | Alyssa Payne |
| Everyone Is Getting Married / Falling | Alyssa Payne |
| Island Files | co-written with Alyssa Payne |
| For the Plot | Alyssa Payne |

**“Higher”** (Time Step Symposium) is a different context; keep it as a **second Wistia media** (or audio), not forced into the Alyssa reel unless Drew wants one long “orchestration sampler.”

### On the portfolio site (behavior)

**One Wistia embed** on the Orchestration panel or inside a shared project dialog—not one iframe per card.

**Cards stay separate** for credits and thumbnails. Clicking a card should:

1. Open the project dialog (if not already open).
2. Ensure the Alyssa embed is visible.
3. **Seek** to that chapter’s start time.

Two supported mechanisms (vanilla-friendly):

#### A. Embed Links (preferred for minimal JS)

Wistia’s [Embed Links](https://docs.wistia.com/docs/embed-links) let page links control the embedded player when the link uses the same hashed ID as the embed:

```text
#wistia_<HASHED_ID>?time=20s
```

Longer formats: `?time=00h01m30s` ([annotation links](https://support.wistia.com/en/articles/8284284-annotation-links)). Links can live on cards, a chapter list in the dialog, or CTAs—no playlist required.

**Requirement:** The embed on the page must use that same `<HASHED_ID>`. Use Wistia’s async embed snippet from Embed & Share.

#### B. Chapters plugin + optional Player API

Configure `chapterList` in embed options ([embed options / chapters](https://docs.wistia.com/docs/embed-options-and-plugins)) so the play bar shows markers. For a **custom list outside the player**, Wistia notes that chapter markers in the bar are in-player only; an on-page list uses Embed Links or the Player API `time(val)` ([chapters FAQ](https://support.wistia.com/en/articles/8283768-chapters-in-your-video)).

Use the API only if Embed Links cannot target the embed from inside a `<dialog>` (test early). Keep JS small per [Stack](../Stack/Vanilla%20HTML%20CSS%20JS.md).

### IA mapping

| UI element | Data |
| --- | --- |
| Orchestration card (per Alyssa track) | Title, credit line, thumbnail (still image or Wistia still), `wistiaHash`, `chapterTime` (seconds or embed-link URL) |
| Dialog | Same embed; card click sets time via Embed Link behavior or API |
| Optional “full reel” control | Link with `#wistia_HASH?time=0` |

Do **not** store video files in git. Store **hashed ID + chapter times + titles** in HTML or a small `orchestration-media.json` later.

## Writing tab and other video

Same pattern when it helps: one Wistia video per **show** with chapters for individual demos, or one video per demo when chapters do not make sense. Writing projects with unrelated lengths (BMI demos vs pitch) may be **separate Wistia medias** rather than one reel.

## Accessibility

- **Captions** on every published segment (WCAG 1.2.2).
- On-page chapter list: real `<button>` or `<a>` elements with clear names (“Play: Crush — Alyssa Payne”), not hover-only.
- Do not rely on chapter markers alone for screen-reader users; the card title + dialog text still carries the credit.

## What to decide before implementation

| Now | Later |
| --- | --- |
| Wistia for orchestration (and likely writing) video | Remove Wistia branding (paid) |
| Alyssa pieces → **one** master + chapters | Exact chapter timestamps (after final cut) |
| Cards → same hash, different `time=` | Whether Higher shares a reel or separate media |
| Standard Wistia embed on site | Player API vs Embed Links only (prototype one dialog) |

## Sources

- [Embed Links](https://docs.wistia.com/docs/embed-links) — chapter jumps from page links
- [Chapters in your video](https://support.wistia.com/en/articles/8283768-chapters-in-your-video) — in-player chapters
- [Embed options & plugins (chapterList)](https://docs.wistia.com/docs/embed-options-and-plugins)
- [Annotation links / time URLs](https://support.wistia.com/en/articles/8284284-annotation-links)
- [Wistia pricing](https://wistia.com/pricing) — Free storage/bandwidth
