# Output Reference Schema

Save each analyzed post to `references_library/<account>-<topic>.md`. Keep it skimmable and action-oriented — the value is reusable *patterns*, not a transcript.

## Template
```markdown
# Reference — @<account> "<short title>"

## Source
- **Origin:** <post URL>
- **Account:** @<account> (<who/niche>)
- **Type:** Carousel / Reel / Image — <KO|EN|both> caption
- **Signals:** ❤️ <likes> / 💬 <comments> (note if comments >> likes → lead-magnet working)
- **Tool/editor credits:** <if shown>
- **Extracted:** <YYYY-MM-DD>
- **Tags:** #hook #carousel #design-tokens #cta #<topic> ...

## One-line
<what it is + why it's worth stealing, 1–2 sentences>

## Content structure
<card-by-card skeleton: e.g. 도입(hook) → 문제정의 → 관점전환 → 체크리스트 → CTA; # slides; pager style>

## Hook formula
<the cover hook pattern, generalized (e.g. "[No-X 배지] + [성과] + [저노력/시간]")>

## Design system (from frames)
- Colors: <bg / accent hex estimates>
- Type: <font family + weight hierarchy>
- Graphic vocabulary: <index numbers / formula cards / tick lines / bars / checkboxes / photo vs flat>
- Layout: <where text sits, scrim, footer/handle, pager>

## Funnel / CTA
<comment-keyword → DM lead magnet? the keyword + the value offer>

## Stealable patterns → how it applies to keens-cardnews
<concrete: which content_engine_prompts.md / brand_and_voice.md / template changes this suggests>

## Batch-JSON hints (optional)
<if the structure maps cleanly, sketch cards[] in the keens-cardnews batch schema>

## Verdict
- Reference / Skill / Clone-spec — and what to absorb first.
- IP note: ideas & structure only; regenerate original Keens copy/visuals.
```

## Batch-JSON mapping (to keens-cardnews)
When a post's structure is clean, translate it into the `keens-cardnews` batch schema so the content engine can reuse the *shape* with original Keens copy:
```json
{ "post_id": "REF-<slug>", "lang": "ko", "total": <n>,
  "cards": [
    {"kicker": "<label>", "headline": "<hook with <span class='hl'> on key word>", "subhead": "..."},
    {"kicker": "...", "stat": "<index/number>", "headline": "...", "subhead": "..."},
    {"kicker": "...", "headline": "...", "cta": "<CTA>"}
  ],
  "caption": "<original Keens caption + lead-magnet keyword>", "dm_keyword": "<KEYWORD>" }
```
Only the **structure/field shape** transfers. Copy text must be regenerated in the Keens voice — never paste the source's words.
