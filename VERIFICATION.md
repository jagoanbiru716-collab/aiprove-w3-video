# Motion verification

Method: extract frames 1 s apart, convert to grayscale at 320x180, compute the
mean absolute pixel difference between consecutive frames (0–255 scale).
A near-static clip scores < 5; a clip with real subject/camera motion scores
well above 15 on every step. Frames were also read visually.

## Source clips (each 1280x720, 24 fps, 10.0 s)

| Clip | Scene | Mean diff / 1 s step | Min step | Max step | Visual check |
|---|---|---|---|---|---|
| 1 — bootup | Robot wakes, stretches, stands in workshop; lights switch on; camera orbits | 37.94 | 19.86 | 59.68 | t=0: robot lying on bench, eyes dim. t=5: robot standing, lights on, new angle. Real subject + camera motion. |
| 2 — ticker tunnel | High-speed flight through streaming market-ticker tunnel | 40.57 | 28.44 | 49.09 | t=0: tunnel vanishing point. t=5: close-up ticker boards, different numbers/charts. Continuous forward flight. |
| 3 — finish line | Robot sprints across finish line; confetti, cheering crowd, trophy | 43.76 | 35.50 | 52.90 | t=0: robot at FINISH banner. t=5: arms raised, trophy close, confetti falling. Real subject + camera motion. |

Per-second step values:

- Clip 1: 30.8, 31.3, 26.0, 19.9, 33.7, 45.2, 57.1, 59.7, 37.7
- Clip 2: 40.0, 43.1, 39.0, 28.4, 30.5, 44.9, 44.1, 46.1, 49.1
- Clip 3: 52.9, 39.9, 43.1, 44.9, 46.5, 46.3, 43.8, 40.9, 35.5

All three clips PASS: no step below 19.8, no static segment.

## Final video — `aiprove-w3-explainer.mp4`

- ffprobe: 60.125 s, 1280x720, H.264 + AAC, 21,671,558 bytes (~20.7 MB)
- 60 frames extracted at 1 fps; mean per-second diff **38.75**, min **18.81**
  (excluding the intentional static end card), max 62.74.
- Only zero-diff steps are t=56–59 s: the static end card (55–60 s), which is
  a title card by design, not footage.
- Timeline: clip 1 x2 (0–20 s), clip 2 x2 (20–40 s), clip 3 + first 5 s of
  clip 3 (40–55 s), end card (55–60 s). Narration runs 0.3–59.1 s.
- Visual spot checks: t=5 s workshop robot standing; t=25 s ticker boards;
  t=45 s finish-line celebration; t=57 s end card reading
  "AIProve — Free to enter · Graded in the open · Paid in stock — Join now:
  aiprove.fun/r/f753a2d6 — Entry by ZephyrNode".
