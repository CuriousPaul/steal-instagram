# Platform specifics — IG / YouTube / TikTok

URL detection, login walls, and engagement extraction per platform. Browser tools assumed:
`navigate`, `get_page_text`, `javascript_tool` (run JS in page), `computer` (screenshot/scroll/click).

## §login — universal rules
- Never type credentials; never bypass a login or bot-check (prohibited). If logged out, surface it and ask the user to log in themselves.
- Multiple browsers connected → the tools force a selection step. Have the user pick the profile that's logged into the **target** platform (their default Chrome may not be it).
- Confirm login by a logged-in marker (IG left-nav icons / YouTube avatar / TikTok avatar) before scanning.

## URL → mode/platform detection
```js
(() => {
  const u = new URL(location.href); const h = u.hostname.replace(/^www\./,''); const p = u.pathname;
  let platform='?', mode='?';
  if (h.includes('instagram.com'))      { platform='ig';  mode=/^\/(p|reel|tv)\//.test(p)?'post':'account'; }
  else if (h.includes('youtube.com'))   { platform='yt';  mode=(/\/watch/.test(p)||/^\/shorts\//.test(p))?'post':'account'; }
  else if (h.includes('youtu.be'))      { platform='yt';  mode='post'; }
  else if (h.includes('tiktok.com'))    { platform='tt';  mode=/\/video\//.test(p)?'post':'account'; }
  return JSON.stringify({platform, mode, path:p});
})()
```
Account URL shapes: IG `instagram.com/<handle>/`; YouTube `/@handle`, `/channel/UC…`, `/c/<name>`; TikTok `tiktok.com/@handle`.

---

## §IG — Instagram
- **Login wall**: logged-out shows 로그인/가입하기 (top-right) + a "가입하기" modal; scrolling the grid stops after ~12 tiles with a "계속하려면 로그인" wall. → must be logged in for a full scan.
- **Account scan**: profile page = grid. Scroll with `computer` scroll; screenshot each viewport. Cover headline = the hook. Reels show a play icon + view count on the tile; carousels show a stack icon.
- **Per-tile engagement**: hover a tile → ❤/💬 overlay appears (capture from screenshot). For exact counts, open the post (post mode) — opening is more reliable than hover.
- **Tabs**: default grid = all; the reel/clapper tab = video only; useful to separate carousel vs reel performance.
- **Profile link**: bio link (Linktree/inpock) = monetization hub — note it.
- Caption/hashtags/exact counts only reliable inside a post via `get_page_text` (post mode).

## §YouTube
- **Mostly open** (no login for browsing), but logging in avoids consent walls and unlocks consistent counts. Some videos age/region-gated.
- **Account scan**: go to `<channel>/videos`, then open the **Sort by** menu and pick **인기 동영상 / Popular** to rank by views (this is the goldmine — what works). The menu label follows the browser UI language; if you don't see Korean, look for "Sort by → Popular". `get_page_text` on the Videos grid yields rows of `title · views · age`. Then `<channel>/shorts` for Shorts (the card-news/Reel analog).
- **Title = hook**; thumbnail = visual hook (screenshot the grid to read thumbnail text/face/style).
- **Per-video deep-dive (post mode)**: open `/watch?v=…`; `get_page_text` gives title, view count, like count (exact likes sometimes hidden), description, and top comments. Chapters/timestamps in the description reveal structure. For Shorts, treat like a Reel (seek frames if on-screen text matters).
- **Engagement read**: views + like + comment; "added N months ago" gives cadence. Sort-by-popular already encodes the win/lose signal.

## §TikTok
- **Login wall**: aggressive — a login overlay pops on scroll and video open for logged-out sessions; throttles fast. Logged in strongly recommended.
- **Account scan**: profile feed tiles show **view counts** (always visible) + cover text. Screenshot + read covers; views are the primary signal (likes/comments are inside the post).
- **Per-video deep-dive (post mode)**: open `/@user/video/…`; `get_page_text` gives caption, hashtags, like/comment/share/save counts, sound. On-screen text changes fast → seek-frame capture like a Reel.
- **Note**: TikTok is video-only; "carousel" = photo mode (swipe images) — step through like an IG carousel.

---

## Engagement normalization (for the content-list table)
Different platforms expose different metrics. Record what's available and label it:
- IG: ❤ likes / 💬 comments (reel: ▶ views).
- YouTube: ▶ views / 👍 likes / 💬 comments / age.
- TikTok: ▶ views / ❤ likes / 💬 comments / ↗ shares / 🔖 saves.
When comparing within an account, **views** (reel/short/tiktok) and **saves/comments** (carousel) are the closest proxies for "what the algorithm pushed". Don't compare raw likes across platforms.

## Troubleshooting (account mode)
| Symptom | Cause | Fix |
|---|---|---|
| IG grid stops scrolling, login modal | logged out | log in (§login) |
| `get_page_text` returns covers but no counts | counts are image overlays | hover (IG) or open the post |
| YouTube grid not ranked by performance | default sort = latest | switch sort to Popular/인기 |
| TikTok overlay blocks every action | logged out throttle | log in; or reduce action rate |
| SPA empty on first read | still rendering | wait 2–3s, retry `get_page_text` |
