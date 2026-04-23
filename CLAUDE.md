# Wabasso Ranch Landing Page

## What This Is

The public landing page for Wabasso Ranch — a placeholder-brand site for a USDA-inspected beef processing facility under construction in Avon Park, FL. The facility won't open until ~Q2 2027; this site exists to capture community attention during the ~15-month permit/construction stretch and funnel it into the Beehiiv newsletter, which will functionally become the pre-launch customer list.

This repo was split off from `~/Desktop/wabassobrain/landing-page/` on 2026-04-22 so the site can live as its own thing.

---

## Deployment

- **Live:** https://wabassoranch.info/
- **Host:** Vercel (auto-deploys from `main`)
- **Repo:** https://github.com/lukeduke1031/wabasso-landing (public)
- **Newsletter target:** https://wabassoranch.beehiiv.com/ — every CTA on the site points here

No Vercel config file in the repo; it's a pure static site (single `index.html` + `assets/`) and Vercel auto-detects.

---

## Current State (as of 2026-04-22 Session 2)

**Two HTML files live at the root:**

- `index.html` — **the minimal page plus FAQ.** Full-viewport dark hero (cattle-faces photo, logo top-left, "Avon Park, Florida" badge with pulsing green dot, "Florida Beef. / For Floridians." headline, one paragraph, "Get updates" CTA to Beehiiv) followed by a white FAQ section carrying the same 10 questions as the full site. No nav, no story, no timeline, no footer — still intentionally spare.
- `full.html` — **the full site, preserved intact.** Nav, hero, "Why we're building this" story, build section with facility renders, 5-step timeline, sunset divider, 10-item FAQ, signup block, footer. Still reachable at `/full.html` but not linked from `index.html`.

**Why the split:** Luke shipped the full site on 4/22 (Session 1), then within 24 hours pulled it back. Reasoning: the full site has good bones but commits to a narrative (story → build → timeline → FAQ) he hasn't fully blessed as the first public impression. The minimal page lets the newsletter list keep growing without locking in a first-impression narrative that might need to change. Re-promoting the full site is a single `git mv` away.

---

## Brand Decisions (load-bearing — don't undo casually)

**Voice and positioning:**
- **Customer-first, not family-first.** Early drafts of the story section led with 3rd-gen rancher / herd-size / history. Luke killed it hard: *"im not trying to flex on here. im trying to explain the why, so our customers know why we are helping, not just flex on them about how many cows we have."* The story leads with "Florida is one of the top cattle-producing states, yet almost none of the beef on local grocery shelves was processed here..." Keep every section customer-facing.
- **No self-quotes.** An early draft had a Luke Dickens pullquote; he cut it (*"is it kind of head ass to include a quote from myself?"*). Don't reintroduce.
- **Single CTA only.** Every call-to-action on the site goes to Beehiiv. No donation ask, no crowdfund, no preorder. Just email list.
- **Transparency over marketing-speak, community-gathering over industrial-efficiency.** These tone choices are rehearsals for the actual Wabasso Beef brand voice at launch.

**Visual system (pulled from the Butcher app for consistency):**
- Fonts: **Chirp** (Twitter-style sans, 4 weights) + **Burnest** (custom display) — both in `assets/fonts/`
- Palette: black `#000000` bg, Twitter blue `#1d9bf0` accent, green `#00ba7c` for live-status dots
- **Dark-by-default, white-where-reading** (for the full site): dark sections for atmosphere (hero, build banner, sunset divider, footer), white sections for text-heavy reading (story, timeline, FAQ). A full-light theme was tried and rolled back.
- Logo cropped tight from source for bigger display in nav

---

## Engineering Notes

- Single-file static site, embedded CSS, no build step, no framework.
- When adding section-scoped CSS overrides (e.g. `#updates .tli::before`), **watch ID specificity** — it will beat `.tli.done` / `.tli.active` state modifiers. Scope overrides with `:not(.done):not(.active)` or use the state class first.
- Inline styles beat external CSS rules — avoid inline `style=` on section containers; they'll override light-theme / dark-theme CSS.
- OG/Twitter share tags use **absolute URLs** with explicit width/height, `og:site_name`, and `twitter:card`. Comment-only previews on Facebook stopped working ~2017 — only standalone post shares unfurl. If an OG tag is changed, force FB re-scrape at https://developers.facebook.com/tools/debug/

---

## Git History

- `210edab` — Initial commit: Wabasso Ranch landing page
- `ba7b5db` — Remove stats strip between hero and story
- `696892f` — Update share preview title to 'Wabasso Ranch - Coming soon'
- `3697f8f` — Use absolute URLs for OG/Twitter share tags + image dimensions
- `1f80239` — Add coming-soon.html minimal landing + trim index.html hero
- `1ab3fa3` — Promote minimal page to root; preserve full site as full.html

---

## Open Threads

- **Decide direction for `full.html`** — iterate privately and re-promote when ready, break into `/about` or `/story` subpage, or rebuild from the minimal view once brand voice is clearer.
- **Beehiiv subscriber count** — worth checking periodically. Past ~1,000 with decent open rates = real organic pull at launch. Stuck at a few hundred sleepy subscribers = brand needs a rebuild in 2027.
- **Share link cache** — iMessage/FB/Twitter previews cache for a few days. Old shares may still show stale OG previews.
- **No About / Team page** — intentionally deferred. Only add if list grows enough that people want to know who's behind it.

---

## Local Preview

```
python3 -m http.server 8787
# then open http://localhost:8787/
```

---

## Broader Context

This is the first public artifact in the Wabasso Beef brand. Strategic backdrop lives in `~/Desktop/wabassobrain/` (operations, financials, slaughterhouse permit timeline, people). Reach over there only when a question genuinely requires business context that isn't in this repo — for landing-page work itself, everything needed should be here.
