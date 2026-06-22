# Adding `steal-instagram` to the kakashi repo

This folder (`steal-instagram/`) is repo-ready — drop it at the **root** of the kakashi repo next to `steal-skill/` and `skill-scoreboard/`.

## 1. README — add to the Skills table
```
| steal-instagram | Instagram 게시물(카드뉴스/릴스/이미지) → 화면문구·디자인토큰·후크구조 레퍼런스 추출 | v1.0.0 ✅ |
```

## 2. README — optional section
```
### steal-instagram — Instagram 레퍼런스 추출 (Kakashi Phase 5 특화)

인스타 URL을 주면 카드뉴스/릴스를 프레임 단위로 분석해 화면 문구·디자인 토큰·후크 구조·
댓글→DM 리드마그넷을 구조화 레퍼런스로 추출합니다. **로그인된 브라우저 세션 필요**
(로그아웃 시 표지+캡션만 가능). 영상은 <video> seek-프레임 캡처 기법 사용.

"이 카드뉴스 훔쳐 https://www.instagram.com/p/XXXX/"
→ references_library/<account>-<topic>.md ✅
```

## 3. Install (OpenClaw)
```
cp -r kakashi/steal-instagram ~/.openclaw/skills/
```

## 4. Notes for kakashi conventions
- Tool names in `references/extraction_recipe.md` are written for a Claude-in-Chrome–style browser MCP;
  for OpenClaw, map to its `browser` / `web_fetch` / `image` tools (the markdown workflow is agent-agnostic).
- Complements `steal-skill` Phase 5 (image/UI) — this one is Instagram-specialized (carousel/Reel grammar,
  hook + funnel extraction) rather than generic app UI analysis.
- Ethics/IP section mirrors steal-skill: extract patterns, generate original work; respect ToS; no PII.

## Commit (you run this — pushing needs your GitHub auth)
```
# from your kakashi clone, after copying steal-instagram/ in:
git add steal-instagram README.md
git commit -m "Add steal-instagram skill (Phase 5 IG-specialized reference extractor)"
git push
```
