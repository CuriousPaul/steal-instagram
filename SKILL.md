---
name: steal-instagram
description: >-
  Analyze a social reference — a single POST or a whole ACCOUNT/CHANNEL — on Instagram, YouTube, or
  TikTok, and turn it into a structured, reusable reference for Keens card-news. POST mode extracts
  per-slide/frame on-screen copy, hook/structure, design tokens, caption (KO/EN), comment-to-DM lead
  magnet, and engagement. ACCOUNT mode scans a profile/channel, builds a content list with
  engagement, mines the recurring hook formulas / formats / funnel / cadence, then writes a benchmark
  plan: 콘텐츠 리스트 + 콘텐츠 분석 + how to apply it to Keens (+ kr_batch.json batch hints). Use whenever
  someone shares an IG/YouTube/TikTok URL — "이 계정 분석해줘", "레퍼런스 계정인데 우리한테 어떻게 적용", "이 카드뉴스 뜯어봐",
  "훔쳐", "벤치마크 계정", studying a competitor, capturing a hook formula, or building an application plan.
  Requires a browser session LOGGED IN to the platform.
---

# Steal — Social Reference Extractor (IG / YouTube / TikTok)

Turn a competitor's **post** or **whole account** into structured, reusable **patterns** for Keens card-news — never a copy. Specialized sibling of Kakashi's Phase 5 (image/UI analysis), tuned for social card-news/Reels/Shorts: it extracts *content structure, hook formulas, design system, and funnel*, then maps them onto the Keens pipeline.

## Two modes — detect from the URL first
| URL shape | Mode | Goes to |
|---|---|---|
| IG `/p/…` or `/reel/…`, YouTube `/watch?v=…`/`/shorts/…`, TikTok `/@user/video/…` | **POST** | §A Post mode |
| IG `/<handle>/`, YouTube `/@handle`·`/channel/…`·`/c/…`, TikTok `/@handle` | **ACCOUNT** | §B Account mode |

If the user gives an account URL and wants a single post, ask which; if they give a post and want the whole account, climb to the profile.

## Hard prerequisite: a logged-in session
Logged-out platforms gate content: IG hides carousels/video behind a signup modal and blocks scrolling past ~12 posts; YouTube is mostly open but age/region-gates some video; TikTok throttles logged-out browsing hard. Real extraction **requires the controlled browser to be logged in** to the target platform.
If you hit a login wall (IG 로그인/가입하기 modal or "계속하려면 로그인"; TikTok login overlay; video `readyState` stays 0):
1. Tell the user the controlled browser isn't logged into that platform.
2. If multiple browsers are connected, have them pick the logged-in one (the browser tools enforce a selection step — a different Chrome profile may be the logged-in one).
3. Navigate to the platform's login page with `?next=<path>` and ask them to log in **themselves**. You must NEVER enter credentials or bypass any login/bot-check (prohibited).
4. Resume once they confirm.

This is observation of public content only. Extract patterns → generate **original** Keens work (see Ethics).

## Heartbeat model
You may run in short windows. Save the reference/plan file and screenshots incrementally and note progress on the Issue, so a later window resumes without re-capturing.

---

## §A. POST mode — single post deep-dive
Full browser technique (video seek-frame capture, carousel stepping, login, troubleshooting) is in `references/extraction_recipe.md`. Summary:

1. **Open & identify type** — `get_page_text` for caption/metadata; detect `<video>` (Reel/Short/video) vs next-arrow (carousel) vs single image.
2. **Capture frames** — Reel/video: control the `<video>` element, seek evenly spaced timestamps, screenshot ~8–12 frames. Carousel: screenshot, click next, repeat to last slide.
3. **Vision-analyze** — per frame: kicker/label, headline (+ emphasized/colored words), subhead, stat/index, CTA; design tokens (bg, accent hex, fonts/weights, layout); graphic vocabulary.
4. **Caption, signals, funnel** — full caption (KO/EN), hashtags, `dm_keyword`, like/comment/view counts, date, tool credits. Comments ≫ likes usually = a working comment→DM lead magnet.
5. **Write the reference** — save to `references_library/<account>-<topic>.md` using `references/reference_schema.md`. Include source, one-line, stealable patterns, **how it applies to keens-cardnews**, batch-JSON hints, and a Verdict.

---

## §B. ACCOUNT mode — profile/channel benchmark
Full workflow in `references/account_scan.md`; platform-specific selectors/JS in `references/platforms.md`. Summary:

1. **Profile snapshot** — handle, follower/subscriber count, bio/positioning, profile link (monetization hub), highlights/playlists, post/video count.
2. **Content list (broad scan)** — scan the grid (IG) / Videos+Shorts tabs sorted by Popular (YouTube) / profile feed (TikTok). For each item capture the **cover hook / title**, format, and **engagement** (likes·comments·views). The cover/title IS the hook payload. Aim for 15–30 items; record in a table.
3. **Pick representative + top performers** — choose 3–6 items that (a) are the highest-engagement and (b) span the account's format range. Deep-dive each with §A Post mode to pull full caption, funnel keyword, hashtags, and frame copy.
4. **Mine the patterns** — recurring **hook formulas** (generalize the headline templates), format mix (carousel vs reel/short, info vs emotion vs sales), **tone & authority devices**, the **comment-keyword → DM funnel**, hashtag strategy (count differs by format), posting cadence, and what actually outperforms.
5. **Write the benchmark plan** — save to `references_library/<account>_benchmark_plan.md` using `references/plan_template.md`. Sections: 계정 스냅샷 · 콘텐츠 리스트(표) · 콘텐츠 분석(후킹 공식·포맷·톤·퍼널·해시태그·한계) · **keens 적용 기획안**(후크 변환표·주제 N선·카드 템플릿·캡션 공식·CTA 퍼널·주의) · **kr_batch.json 배치 힌트**.

---

## Output — what good looks like
A reference/plan that lets the Keens content engine reuse the *patterns* (structure, hook formula, design tokens, funnel) to generate **original** content. The account-mode plan ends with concrete next actions and a `kr_batch.json` draft the `keens-cardnews` skill can build from. See `examples/prompt_what-claude-cardnews.md` for a worked post example.

## Ethics & IP (non-negotiable)
- Extract **ideas, structure, design principles, tactics** (not copyrightable) → generate original copy and visuals. Do **not** reproduce a competitor's slides, photos, titles, thumbnails, or caption verbatim.
- Respect each platform's ToS; don't scrape at scale, don't store commenters' personal data, no PII.
- Honor Keens brand guardrails when applying: no exaggerated/guaranteed claims; careful with trainee mental-health, body, or appearance topics; verify USP claims before publishing.
- Generated references are drafts from public info; the user is responsible for final use. Mirrors Kakashi's "Steal Like an Artist": learn the pattern, make it yours.

## Report back on the Issue
Summarize: mode, platform, items scanned + deep-dived, the dominant hook formula, design tokens, funnel mechanic, and the 2–3 most actionable upgrades for Keens. Link the saved reference/plan file (+ batch JSON if written).

## Bundled resources
- `references/account_scan.md` — ACCOUNT-mode workflow (scan → content list → top-performer selection → synthesis → plan).
- `references/platforms.md` — IG / YouTube / TikTok specifics: URL detection, login walls, engagement extraction, selectors & JS snippets.
- `references/extraction_recipe.md` — POST-mode browser technique (video seek-frame capture, carousel stepping, login, troubleshooting).
- `references/reference_schema.md` — POST-mode reference .md schema + batch-JSON mapping.
- `references/plan_template.md` — ACCOUNT-mode benchmark-plan .md template + kr_batch.json hint mapping.
- `examples/prompt_what-claude-cardnews.md` — full worked example from a real Reel.
