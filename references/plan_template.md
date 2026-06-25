# Benchmark Plan — output template (ACCOUNT mode)

Save to `references_library/<account>_benchmark_plan.md`. Fill every section; keep tables skimmable. The value is reusable **patterns + an application plan**, not a transcript. A real worked instance: `benchmark_elena_mom_분석_기획안.md` in the project root.

```markdown
# 벤치마크 분석 — @<account> → keens seoul 적용 기획안

> 작성일 <YYYY-MM-DD> · 대상 <platform> <account URL>
> 수집: 그리드/채널 스캔 N개 + 로그인 상태 대표 M건 본문·해시태그·인게이지먼트 정밀 수집.
> 프로필 링크: <link> (수익 허브)

## 1. 계정 스냅샷
| 항목 | 내용 |
|---|---|
| 핸들 | @<account> (<verified?>) |
| 규모 | 팔로워/구독 <n> · 게시물/영상 <n> |
| 포지셔닝 | <authority + niche + offer 한 줄> |
| 수익화 | <공구/제휴/상담 + 링크 허브> |
| 시그니처 시리즈 | <highlights/playlists> |

**핵심 정체성**: <권위 + 정보 + 감정자극의 공식 1–2문장>

## 2. 콘텐츠 리스트 (수집 샘플)
| # | 후크(커버/제목) | 포맷 | 후크 유형 | 인게이지먼트 |
|---|---|---|---|---|
| 1 | <…> | 캐러셀/릴스/숏/영상 | 내부정보·공포·공감… | ❤/💬/▶ |
| … | | | | |

> 정밀 수집 M건(본문 확인) 하이라이트 표 + 최고 성과 유형 한 줄.

## 3. 콘텐츠 분석
### 3-1. 후킹 공식 (헤드라인 템플릿, 빈칸형)
1. <[내부집단]이 무조건 ~하는 것> …  (심리: FOMO/공감/공포…)
2. …
### 3-2. 포맷 패턴
<캐러셀=저장형 / 릴스·숏=도달 / 세일즈 분산 비율>
### 3-3. 캡션 N단 공식 (실측 구조)
<도입 고생담 → 정보격차 → 권위해결 → 리스트 → 리프레임 → CTA …>
### 3-4. 핵심 엔진 — 댓글 키워드 → DM 퍼널
<키워드 + 제안. 좋아요가 아니라 댓글·저장·DM 전환이 KPI>
### 3-5. 해시태그 / 권위장치 / 발행 주기
<포맷별 해시태그 수, 연구·실명 인용, 업로드 케이던스>
### 3-6. 솔직한 평가
<어디서 터지고 어디가 약한지, 무엇이 복제 가능한지>

## 4. keens seoul 적용 기획안
> keens 톤: 미국식 listicle 카드뉴스 + 현직 전문가의 정직·냉정 피드백, 도발 후크 + 데이터 근거 + 레벨테스트 CTA. 타깃: 아이돌/실용음악 지망생 학부모·본인. 과장·보장 금지, 멘탈·외모 민감주제 주의.

### 4-1. 후크 변환표 (레퍼런스 → keens)
| 레퍼런스 패턴 | keens 변환 예시 |
|---|---|
| <…> | <…> |

### 4-2. 주제 N선 (다음 배치 후보) — 후크 유형별 그룹
A. 공포/후회 … B. 내부정보/폭로 … C. 공감/거울 … D. 권위/성공사례 … E. 실전 가이드 …

### 4-3. 카드 구성 템플릿 (5장 캐러셀, build_cards 호환)
- 01 커버: 후크 한 줄, 키워드만 레드(#E8472B)
- 02–05: 넘버드 리스트/체크리스트/비교표 + 현직 전문가 한 줄 코멘트
- 푸터: `Keens | @handle ··· 0N/05`
- CTA 카드: "댓글에 'LEVEL' → 무료 레벨테스트 DM"

### 4-4. 캡션 N단 공식 + CTA 퍼널
<레퍼런스 공식 차용, 키워드 댓글 퍼널(ManyChat dm_keyword), 다음편 떡밥, 해시태그 운용>

### 4-5. 운영 권고 / 주의
<카드+릴스 병행, 시그니처 시리즈, 민감주제 가드, USP 사전검증>

## 5. kr_batch.json 배치 힌트
<주제 3–4건을 keens-cardnews 배치 스키마로 스케치(구조만, 카피는 keens 보이스로 재생성)>

## 6. 다음 액션
1. … 2. … 3. …
```

## kr_batch.json hint mapping
Translate the **structure** of a strong reference into the `keens-cardnews` batch schema. Copy is regenerated in the Keens voice — never paste source words. (Same mapping as `reference_schema.md`.)
```json
{ "post_id": "REF-<slug>", "lang": "ko", "total": 5,
  "cards": [
    {"kicker": "<label>", "headline": "<hook, <span class='hl'> on key word>", "subhead": "..."},
    {"kicker": "...", "stat": "1", "headline": "...", "subhead": "..."},
    {"kicker": "...", "stat": "2", "headline": "...", "subhead": "..."},
    {"kicker": "...", "stat": "3", "headline": "...", "subhead": "..."},
    {"kicker": "...", "headline": "...", "cta": "댓글에 'LEVEL' → 무료 레벨테스트 DM"}
  ],
  "caption": "<original Keens caption: 고생담→정보격차→권위→리스트→리프레임→CTA>",
  "dm_keyword": "LEVEL", "hashtags": ["#아이돌지망생","#실용음악입시","#보컬학원"] }
```
Only field shape transfers. Always end with the brand guardrail: no guaranteed claims, sensitive-topic care, verify USP.
