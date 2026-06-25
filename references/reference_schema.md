# Output Reference Schema

Save each analyzed post to `references_library/<account>-<topic>.md`. Keep it skimmable and action-oriented — the value is reusable *patterns*, not a transcript.

## Template
```markdown
# Reference — @<account> "<short title>"

## Source
- **Origin:** <post URL>
- **Account:** @<account> (<who/niche>)
- **Type:** Carousel / Reel / Image — <KO|EN|both> caption
- **Signals:** ❤️ <likes> / 💬 <comments> / 🔁 <reposts> / ▶ <views> (note the engine: comments ≫ likes → comment→DM lead magnet; reposts/shares high → share-bait/담론형; saves high → save-bait reference)
- **Tool/editor credits:** <if shown>
- **Extracted:** <YYYY-MM-DD>
- **Tags:** #hook #carousel #design-tokens #cta #<topic> ... (add #no-funnel / #editorial when applicable)

## One-line
<what it is + why it's worth stealing, 1–2 sentences>

## Content structure
<card-by-card skeleton: e.g. 도입(hook) → 문제정의 → 관점전환 → 체크리스트 → CTA; # slides; pager style>

## Hook formula
<the cover hook pattern, generalized (e.g. "[No-X 배지] + [성과] + [저노력/시간]", or "A처럼 보이는 건 사실 B였다" 반전형). Note which slides reuse the same template.>

## Caption formula (if a long caption)
<the recurring N-beat structure, generalized: e.g. 고생담 → 정보격차 → 권위해결 → 리스트 → 리프레임 → CTA. Editorial/reflective captions have their own beats (도발질문 → 메커니즘 → 반전 → 열린결론) — capture whichever applies.>

## Design system (from frames)
- Colors: <bg / accent hex estimates; note if NO color highlight (white-on-dark editorial) vs keyword-color listicle>
- Type: <font family + weight hierarchy>
- Graphic vocabulary: <index numbers / formula cards / tick lines / bars / checkboxes / photo vs flat / italic footnote>
- Layout: <where text sits, scrim, footer/handle, pager>

## Funnel / CTA
<comment-keyword → DM lead magnet? the keyword + the value offer. If NONE (담론·share-bait editorial), say so explicitly and name the real KPI (담론/brand authority via 공유·저장·댓글 논쟁) — this is a valid pattern, not a gap.>

## Stealable patterns → how it applies to keens-cardnews
<concrete: which content_engine_prompts.md / brand_and_voice.md / template changes this suggests. If the source is no-funnel, note the **CTA-card add-on**: Keens appends a final 레벨테스트 CTA card to keep 도달(에세이)+전환(리드젠) hybrid.>

### 브랜드 가드 (when applying)
- 타 기획사·아티스트·아이돌 폄하/단정 금지 → 교육적·중립 프레이밍으로 재작성.
- 과장·보장 표현 금지; 멘탈·외모·체중 민감주제 압박 금지; USP 성과표현 게시 전 사실 확인.

## Batch-JSON hints (optional)
<if the structure maps cleanly, sketch cards[] in the keens-cardnews batch schema; add a final CTA card if the source had none>

## Verdict
- **Reference (format/tone) / Skill (recurring engine) / Clone-spec** — and what to absorb first.
- IP note: ideas & structure only; regenerate original Keens copy/visuals — never the source's slides, sentences, photos, titles, or caption.
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
