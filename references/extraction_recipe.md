# Extraction Recipe — exact browser technique

> Tools assumed: a Claude-in-Chrome–style browser MCP with `navigate`, `get_page_text`,
> `javascript_tool` (run JS in page), and a `computer` screenshot action. Adapt names to your agent.

## 0. Login handling (do this first)
- Navigate to the post. Screenshot. If you see 로그인/가입하기 (top-right) or a "가입하기" modal, or the
  `<video>` won't play (`readyState` stays 0), the session is **logged out**.
- Navigate to `https://www.instagram.com/accounts/login/?next=/p/<shortcode>/` and ask the user to log in.
  Do NOT type credentials yourself.
- If several browsers are connected, the browser tools force a selection step — have the user pick the
  one that's logged into IG (it may be a different Chrome profile than the default).
- Re-navigate to the post and confirm the left nav shows the logged-in IG icons before continuing.

## 1. Identify media type
```js
(() => {
  const v = document.querySelector('video');
  const nextBtn = document.querySelector('button[aria-label*="다음"],button[aria-label*="Next"]');
  return JSON.stringify({ hasVideo: !!v, hasNext: !!nextBtn });
})()
```
- `hasVideo` → Reel/video (use §2A). `hasNext` (no video) → carousel (use §2B). Neither → single image.

## 2A. Reel / video — seek-and-capture (the reliable method)
Control the `<video>` element and screenshot evenly spaced frames. Do NOT rely on it playing.
```js
// inspect
(() => { const v=document.querySelector('video'); v.muted=true; v.pause();
  return JSON.stringify({duration:v.duration, readyState:v.readyState, vw:v.videoWidth, vh:v.videoHeight}); })()
```
Then, for each timestamp (≈ duration/10 spacing): run a seek, wait ~1s for the frame to settle, screenshot.
```js
(() => { const v=document.querySelector('video'); v.pause(); v.currentTime = <T>; return 'ok'; })()
```
Tips:
- Batch `[seek → wait 1s → screenshot]` triples to cut round-trips.
- `readyState` should be 4 (HAVE_ENOUGH_DATA) before seeking; if 0, it's still gated/loading (recheck login).
- These tutorials swap slides every 1–3s; if a transition is missed, add an intermediate timestamp.
- Caption text is separate — get it with `get_page_text` (don't try to OCR it from frames).

## 2B. Carousel — step through slides
- `get_page_text` → caption.
- Screenshot slide 1. Click the right/next arrow (`button[aria-label*="다음"]` / `*="Next"`), wait, screenshot.
  Repeat until the "N/N" indicator stops advancing or the next arrow disappears.
- Logged-out carousels usually won't advance past slide 1 — needs login.

## 3. Read frames (vision)
For each frame: kicker/label, headline (+ emphasized/colored words), subhead, stat/index numbers, CTA,
plus design tokens (bg, accent hex estimate, font family/weights, layout) and graphic vocabulary
(index numbers, formula/structure cards, tick lines, bars, checkboxes, photo vs flat, tone inversions).

## 4. Troubleshooting
| Symptom | Cause | Fix |
|---|---|---|
| Only cover frame, play does nothing | logged out | log in (§0) |
| `readyState` 0, `duration` null | not loaded / gated | confirm login, wait, re-inspect |
| `get_page_text` empty | SPA still rendering | wait 2–3s, retry |
| Screenshot "page still loading" | perpetual network (rare on IG) | use `javascript_tool` to read DOM instead |
| Carousel won't advance | logged out | log in |
| JS result comes back `{}` | async/serialization hiccup | return a plain string/JSON string, retry |
