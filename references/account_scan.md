# Account Scan — profile/channel benchmark workflow

Goal: from one account/channel URL, produce a **benchmark plan** = 콘텐츠 리스트 + 콘텐츠 분석 + Keens 적용 기획안 + kr_batch.json hints. Platform specifics (selectors, login walls, engagement) live in `platforms.md`; this file is the mode-agnostic method.

## 0. Login + browser selection (do first)
Same rule as post mode. If logged out, have the user pick the logged-in browser and log in themselves — never enter credentials, never bypass a bot-check. Confirm the logged-in chrome (left nav / avatar) before scanning. See `platforms.md §login`.

## 1. Profile snapshot
Capture, with `get_page_text` + one screenshot:
- handle / display name / verified
- follower (subscriber) · following · post (video) count
- bio / positioning line (who they are, why trusted — the authority claim)
- profile link (Linktree/inpock/등 = the monetization hub) and pinned highlights/playlists (their evergreen series)

These tell you the account's *positioning formula* (authority + niche + offer), which the Keens plan must answer with Keens' own authority.

## 2. Content list — broad scan (the cover/title IS the hook)
You do **not** need to open every post. The grid cover (IG/TikTok) or video title+thumbnail (YouTube) already carries the hook. Scan breadth-first:
- **IG**: scroll the profile grid; screenshot each row; for each tile read the cover headline. Hover a tile to reveal ❤/💬 overlay, or note reel view counts on the thumbnail. Logged-out scrolling dies after ~12 tiles → must be logged in for a full scan.
- **YouTube**: open the channel → **Videos** tab → sort **Popular** (this surfaces what works); `get_page_text` gives title + view count + age per row. Repeat on the **Shorts** tab (Shorts ≈ the card-news/Reel analog).
- **TikTok**: profile feed tiles show view counts; read cover text + views.

Record 15–30 items in a table: **hook/title · format · hook-type · engagement**. Stop when new items stop adding new *patterns* (you'll see the same 4–6 templates recur).

### Hook-type tags (use these consistently)
`내부정보/비교` · `폭로/내막` · `공포/후회` · `공감/거울` · `큐레이션 TOP-N` · `성공사례/권위` · `방법론/루틴` · `공구/세일즈`. Tagging each item makes the pattern analysis fall out by counting.

## 3. Select representative + top performers → deep-dive
Pick **3–6** items: the 2–3 highest-engagement + 2–3 that cover the remaining formats. Deep-dive each via **POST mode** (`extraction_recipe.md`) to pull: full caption, **comment-keyword → DM funnel** (the actual keyword + offer), hashtag set (count + which), per-slide/frame copy, exact like/comment/view counts. This is where the real mechanics surface (the grid only shows covers).

> Watch for: covers/grid often under-report engagement (old or fresh posts); a deep-dived top performer reveals the account's true ceiling and the funnel wiring.

## 4. Mine the patterns (what the analysis section must answer)
- **Hook formulas** — generalize the recurring headline templates into fill-in-the-blank forms (e.g. "[내부집단]이 무조건 ~하는 것", "[권위자]가 말해주는 진짜 속사정", "~해도 후회하는 것 TOP-N"). Note which template tops engagement.
- **Format mix** — carousel/long-form (save-bait) vs reel/short (reach) vs sales; how often each; how sales is spaced between info.
- **Tone & authority devices** — 1st-person insider voice, named proof (real schools/results/research citations), credibility framing.
- **Caption formula** — the recurring N-beat caption structure (capture the real beat count; info accounts ≈ 고생담→정보격차→권위→리스트→리프레임→CTA, editorial accounts ≈ 도발질문→메커니즘→반전→열린결론).
- **Funnel** — the comment-keyword → DM lead magnet (the engine), cliffhanger "다음 편" series, save/share asks. This, not likes, is the KPI. **If there's no funnel** (담론·share-bait editorial account), name the real KPI (담론/brand authority) — Keens hybridizes by adding a final CTA card.
- **Hashtag strategy** — count usually differs by format (e.g. carousel few, reel many).
- **Cadence** — posting frequency and series cadence (a signature recurring series = the highlight reels).
- **Honest read** — where engagement is weak, where it spikes, what's actually replicable.

## 5. Write the benchmark plan
Use `plan_template.md`. The plan must end in two action layers:
1. **keens 적용 기획안** — hook-conversion table (their template → Keens version), topic ideas N선 grouped by hook-type, a 5-card carousel template, the **caption N-beat formula** (carry the source's actual beat count), the CTA keyword funnel (add a final CTA card even if the source had none), and **brand cautions** (no disparaging rival agencies/idols, no guaranteed claims, sensitive-topic care, verify USP).
2. **kr_batch.json 배치 힌트** — 3–4 of the strongest topics sketched in the `keens-cardnews` batch schema (structure only; copy is regenerated in Keens voice). See `reference_schema.md` for the field mapping; never paste source words.

Save to `references_library/<account>_benchmark_plan.md`. If the user wants, hand the batch hints to the `keens-cardnews` skill to build `kr_batch.json`.

## Time budget / heartbeat
A full account scan is 15–40 browser actions. If running in a short window: finish §1–2 (snapshot + content list) and save; resume at §3 (deep-dives) later. Always persist partial tables so nothing is re-scanned.
