---
name: steal-instagram
description: >-
  Analyze an Instagram post — carousel "card news", Reel/video, or single image — from its URL and
  extract a structured reference: per-slide on-screen copy, hook/structure, design tokens (colors,
  fonts, layout), graphic vocabulary, caption (KO/EN), CTA / comment-to-DM lead magnet, and engagement
  signals. Use whenever someone shares an Instagram URL and wants it analyzed, "훔쳐"/"이거 분석해"/"이 카드뉴스
  뜯어봐"/"레퍼런스로 저장", wants to study a competitor's carousel or Reel, capture a hook formula, or turn an
  IG reference into reusable card-news patterns. Outputs a reference .md (and optional batch-JSON hints
  for the keens-cardnews pipeline). Requires a browser session that is LOGGED IN to Instagram.
---

# Steal Instagram — Reference Extractor

Turn an Instagram post into a structured, reusable **reference** for card-news work. Specialized sibling of Kakashi's Phase 5 (image/UI analysis), tuned for Instagram card-news/Reels: it extracts the *content structure and design system*, not generic app data models.

## Hard prerequisite: a logged-in IG session
Logged-out Instagram blocks video playback and gates carousels behind a signup modal — you'll only get the cover frame + caption. Real frame extraction **requires the controlled browser to be logged into Instagram**. If you hit a login wall (top-right shows 로그인/가입하기, or a "가입하기" modal, or playback won't start / `video.readyState` stays 0):
1. Tell the user the controlled browser isn't logged into IG.
2. Navigate to `https://www.instagram.com/accounts/login/?next=<post path>` and ask them to log in themselves (you must NOT enter credentials — entering passwords is prohibited).
3. If multiple browsers are connected, have them pick the logged-in one (the browser tools enforce a selection step).
4. Resume once they confirm.

Never enter credentials, never bypass the login or any bot-check. This is observation of public content only — extract patterns, generate original work (see Ethics).

## Heartbeat model
You may run in short windows. Save the reference file and screenshots incrementally and note progress on the Issue, so a later window resumes without re-capturing.

## Workflow

### 1. Open and identify media type
Navigate to the URL (browser tools). Read the caption + metadata with `get_page_text`. Determine the type:
- **Single image** → one screenshot.
- **Carousel** (multi-image, "1/N" dots, next arrow) → step through slides.
- **Reel / video** (play button, `<video>` element) → seek-and-capture frames (recipe below).

If unsure, look for a `<video>` element (Reel) vs. a next-arrow button (carousel).

### 2. Capture frames — the working recipe
Full technique with exact JS in `references/extraction_recipe.md`. Summary:

**Reel / video** — control the `<video>` element directly and screenshot evenly spaced frames (this is more reliable than watching it play):
```js
// 1) inspect
const v=document.querySelector('video'); v.muted=true; v.pause();
// returns duration, readyState, videoWidth/Height
// 2) for each timestamp t in evenly spaced 0..duration:
v.pause(); v.currentTime = t;   // then wait ~1s and screenshot
```
Sample ~8–12 frames across the duration. On-screen text is the payload — slides in these tutorials change every 1–3s, so denser sampling near transitions helps.

**Carousel** — screenshot slide 1, click the next arrow, screenshot, repeat to the last slide (watch the "N/N" indicator). Caption comes from `get_page_text`.

### 3. Vision-analyze the frames
For each captured frame/slide, read:
- **On-screen copy** — kicker/label, headline (note emphasized/colored words), subhead, stat/index numbers, CTA text.
- **Structure** — the card sequence (e.g. 도입→문제→관점전환→체크리스트→CTA), number of slides, pager style ("04/10", "넘겨보기 →").
- **Design tokens** — background, accent/highlight color (hex estimate), font family, weight hierarchy, layout (where text sits), radius/spacing feel.
- **Graphic vocabulary** — index numbers, formula/structure cards, tick lines, bars, checkboxes, photo vs. flat, tone inversions.
- **CTA / lead magnet** — is there a "comment a keyword → DM" mechanic? capture the keyword and offer.

### 4. Pull caption, signals, funnel
From `get_page_text`: full caption (KO and/or EN), hashtags, `dm_keyword`, like/comment counts, posted date, tool/editor credits. High comment-vs-like ratio usually signals a working comment→DM lead magnet — note it.

### 5. Write the reference
Save to `references_library/<account>-<topic>.md` using the schema in `references/reference_schema.md`. Always include: Source metadata, one-line, stealable patterns, **how it applies to keens-cardnews** (concrete), batch-JSON hints if the structure maps cleanly, and a Verdict (Reference vs. Skill vs. Clone-spec). Tag it (#hook #carousel #design-tokens #cta etc.).

## Output — what good looks like
A reference that lets the content engine reuse the *patterns* (structure, hook formula, design tokens, funnel) to generate **original** Keens content — not a copy. See `examples/prompt_what-claude-cardnews.md` for a complete worked example produced from a real Reel (incl. extracted project-instruction principles and design system).

## Ethics & IP (non-negotiable)
- Extract **ideas, structure, design principles, tactics** (not copyrightable) → generate original copy and visuals. Do **not** reproduce a competitor's slides, photos, or caption verbatim.
- Respect Instagram ToS; don't scrape at scale, don't store personal data of commenters, no PII.
- Generated references are drafts from public info; the user is responsible for final use.
- This mirrors Kakashi's "Steal Like an Artist" principle: learn the pattern, make it yours.

## Report back on the Issue
Summarize: media type, # slides/frames captured, the hook formula, design tokens, funnel mechanic, and the 2–3 most actionable upgrades for keens-cardnews. Link the saved reference file.

## Bundled resources
- `references/extraction_recipe.md` — exact browser technique (video seek-frame capture, carousel stepping, login handling, troubleshooting).
- `references/reference_schema.md` — output reference .md schema + batch-JSON mapping.
- `examples/prompt_what-claude-cardnews.md` — full worked example.
