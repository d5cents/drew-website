# Hosting: GitHub Pages and similar static hosts

Drew’s brief lists **GitHub Pages, Cloudflare Pages, or Netlify**. The site is a personal musical-theatre portfolio with no login, no CMS, and no server-side app. All three can host that. The useful question is which one to **start on**, and what would justify switching later.

## What this site actually needs from a host

Must have:

- Serve HTML, CSS, JS, images from git
- HTTPS
- Custom domain later (optional at launch)
- Free or near-free for a low-traffic personal site

Nice to have, not required for v1:

- Preview URLs on pull requests
- Server-side redirects
- Built-in contact forms
- High bandwidth for self-hosted audio/video

Does **not** need:

- Serverless functions
- A database
- Incremental builds or a framework adapter

Because the recommended stack is plain files (see `Research/Stack/`), the host is a static file server plus DNS. Switching later is a DNS change, not a rewrite.

## Option A — GitHub Pages (recommended default)

**What it is.** GitHub turns a repository into a public website. Official overview: [GitHub Pages documentation](https://docs.github.com/en/pages).

**Fit.** This repo already lives on GitHub. A vanilla site can publish with **no build step**: an `index.html` at the publishing root, plus CSS/JS. If GitHub’s default Jekyll pass would mangle files, add an empty `.nojekyll` in the publishing source ([Creating a GitHub Pages site](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site)).

**Publishing modes** ([Configuring a publishing source](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)):

| Mode | When to use |
| --- | --- |
| Branch + `/` or `/docs` | Simplest for a hand-written site. Research stays in the repo; only the chosen folder is published, **or** the whole repo is published and non-site files are either not linked or kept out of the publish folder. |
| GitHub Actions | Use if a later build appears (image pipeline, HTML includes). Not needed for v1. |

**Project vs user site.** This repo is `drew-website`, so the default URL is a **project site** (`https://<user>.github.io/drew-website/`). Relative URLs (`./css/site.css`) work; root-absolute URLs (`/css/site.css`) break on a project site unless a custom domain is used. A user/org site (`<user>.github.io` repo) gets the apex of `*.github.io`. Decide URL shape **before** hard-coding asset paths.

**Custom domain.** Supported with HTTPS via Let’s Encrypt ([About custom domains](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/about-custom-domains-and-github-pages), [Securing with HTTPS](https://docs.github.com/en/pages/getting-started-with-github-pages/securing-your-github-pages-site-with-https)). GitHub recommends configuring `www` and apex together. Verify the domain to reduce takeover risk. **Defer buying/pointing a domain until the one-page shell exists.**

**Hard limits** ([GitHub Pages limits](https://docs.github.com/en/pages/getting-started-with-github-pages/github-pages-limits)):

- Published site ≤ **1 GB**
- Soft bandwidth **~100 GB/month**
- Soft **10 builds/hour** unless using a custom Actions workflow
- Deploy timeout **10 minutes**
- Rate limiting possible (`429`)

**Media constraint.** Git LFS **cannot** be used with GitHub Pages ([About Git LFS](https://docs.github.com/en/repositories/working-with-files/managing-large-files/about-git-large-file-storage)). Do not store show demos as LFS in this repo expecting them to play on the site. Even without LFS, streaming audio/video from Pages burns the 1 GB / 100 GB budgets and is a poor CDN. Host demos off-site; embed them. **Video:** Wistia (see [`Research/Media/Wistia video hosting and chapters.md`](../Media/Wistia%20video%20hosting%20and%20chapters.md)). **Audio:** SoundCloud, Bandcamp, or small files as appropriate. Thumbnails and small images can live in the repo.

**No server-side redirects.** Path changes later (`/writing` → `/#writing`) need client-side handling or a host that supports `_redirects`. Keep a stable one-page URL from the start so this barely matters.

**Tradeoffs.**

- Pros: zero extra accounts, matches Drew’s first-named intent, no monthly bill, files in git are the site
- Cons: no native forms, no PR preview URLs, weak redirect story, not a media CDN, public source for a public Pages site on the free plan

## Option B — Cloudflare Pages

**What it is.** Git-connected static hosting on Cloudflare’s network ([Getting started](https://developers.cloudflare.com/pages/get-started/), [Git integration](https://developers.cloudflare.com/pages/get-started/git-integration/)). Plain HTML needs **no build command**; publish the site directory.

**Extras vs Pages:** preview deploys on branches, `_redirects`, custom headers, optional Workers later, strong CDN. Custom domains: add the domain **in the Pages project first**, then DNS; apex domains want the zone on Cloudflare ([Custom domains](https://developers.cloudflare.com/pages/configuration/custom-domains/)).

**Limits (Free)** ([Pages limits](https://developers.cloudflare.com/pages/platform/limits/)): 500 builds/month, 1 concurrent build, 20,000 files, 25 MiB per file. Static bandwidth is the selling point versus GitHub’s soft cap.

**Tradeoffs.**

- Pros: easy later move of the same HTML; better if self-hosting large media or wanting previews
- Cons: second vendor; Cloudflare is nudging new work toward Workers rather than Pages; forms are not built-in
- Use if: GitHub bandwidth or file-size limits become real, or Drew wants preview URLs without Netlify

## Option C — Netlify

**What it is.** Git-connected static hosting with a larger “platform” surface ([Git workflows](https://docs.netlify.com/build/git-workflows/overview)). Blank build command + publish directory for vanilla files.

**Distinctive extra:** [Netlify Forms](https://docs.netlify.com/manage/forms/setup) can capture a contact form without a backend (`data-netlify="true"`). Drew’s brief specifies **email + Instagram**, not a form. A `mailto:` link and an Instagram URL meet the spec without locking contact to Netlify.

**Tradeoffs.**

- Pros: Deploy Previews, redirects, forms if a form is added later
- Cons: free-tier bandwidth/credits are easier to bump into than Cloudflare; another account; forms create host coupling in HTML
- Use if: Drew later wants a real contact form and preview comments, and is willing to accept Netlify-specific markup

## Recommendation

| Decision | Choice | Why |
| --- | --- | --- |
| v1 host | **GitHub Pages** | Already on GitHub; vanilla files; listed first in the brief; no extra product |
| Publish shape | Project site **or** `/docs` on `main` | Keep `Research/` in git without serving it as public pages. Prefer a dedicated publish folder (`docs/` or `site/`) once implementation starts |
| Contact | `mailto:DrewNicholsMusic@gmail.com` + Instagram | Matches copy; avoids Netlify Forms |
| Audio/video | Wistia (video) + other embeds for audio | Pages is not a media host; LFS will not play |
| Custom domain | Later | DNS after the shell works on `*.github.io` |
| Escape hatch | Same files → Cloudflare Pages | No rewrite if bandwidth or previews become the issue |

**Do not decide now:** exact custom domain, whether to use Cloudflare as CDN in front of Pages, or a contact form.

## Implementation notes (for later — not this phase)

1. Create a publish folder that contains only the site (not `Research/`).
2. Enable Pages on that folder; add `.nojekyll`.
3. Use relative URLs so a project-site path prefix does not break assets.
4. Keep demo files out of the repo except small thumbnails.
