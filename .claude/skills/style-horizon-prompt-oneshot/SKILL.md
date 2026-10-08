---
name: style-horizon-prompt-oneshot
description: Build a video in the Horizon Prompt One-shot look (style card horizon-prompt-oneshot) — one continuous camera on a near-black stage lit by a soft planet-horizon glow; a glass app bar, a cursor and a prompt box morph into each other, a prompt is typed, the send button grows into a tile that blooms into a full-frame result, then a light wipe to a logo end card, every beat hit-synced to a UI sound. Use when the director picked this card, or the owner says "horizon prompt", "the prompt one-shot", "the ChatGPT-style promo", "زي فيديو البرومبت", "الكيرسر اللي بيكتب البرومبت", or the video is an AI tool show-off / prompt-to-result demo, a course or service promo opener, a launch teaser or a channel bumper. Not for talking heads, real screen-recording proof, data-heavy explainers or long tutorials. DRAFT — untested.
---

# Style: Horizon Prompt One-shot

A quiet premium product-film: one virtual camera, no cuts — glass UI shapes morph (arc → pill → button → tile → full frame) while a cursor drives every beat, and one sound lands on each beat.
Card: `video-projects/_library/styles/horizon-prompt-oneshot/style.md` (status **draft** — say so to the owner until he approves it on the board). Nothing in this look has been built or rendered yet; everything below is from measuring the reference.

**Look first** (in the style folder): `frames/01-glass-bar-corner-glow.png (not in the public repo)` · `frames/02-horizon-arc-wordmark.png (not in the public repo)` · `frames/03-pill-on-glow-floor.png (not in the public repo)` · `frames/04-typing-punch-in.png (not in the public repo)` · `frames/05-result-tile-rise.png (not in the public repo)` — these are 16:9 reference stills with third-party logos: look only, never send them to AI tools. Motion: `refs/ref-arc-to-pill-10fps.jpg (not in the public repo)`, `refs/ref-send-to-result-10fps.jpg (not in the public repo)`.

## 0. Apply the card first
```bash
node tools/vid.mjs style apply horizon-prompt-oneshot <project> [--mode calm|punchy]
node tools/vid.mjs style show horizon-prompt-oneshot
```

## 1. Colours = roles (the brand fills the hex)
Never ship the reference indigo/blue unless the brand says so. Never show real third-party logos (OpenAI, Google, Microsoft, Anthropic…) without permission — use the brand's own mark, neutral glyphs or lucide icons.
| Role | CSS token | From `brand/<name>.md` | Test default (reference) |
|---|---|---|---|
| stage | `--stage` | darkest canvas | #020000 |
| glow hot → mid → band | `--glow-hot/-mid/-band` | primary lightened 70% / 40% / 15% | #e6e6f8 / #9195cc / #6786d5 |
| floor | `--floor` | light canvas | #ecedfd |
| accent (one element at a time) | `--accent` | primary | #316ded |
| rim + text | `--rim`, `--text` | white / text-on-dark | #ffffff |

## 2. Build it (hand-built — no kit yet)
- **Library pieces** (`node tools/vid.mjs use <block> <project>`, read their notes first):
  - `yt-camera-move-9x16` — the digital punch-in (scale jump in 1 frame) for the 2 camera beats.
  - `glass-cards-9x16` — glass rim + glow recipe for the bar, pill and caption pill.
  - `tracking-typography-9x16` — camera that follows a UI target (the pan to the send button).
  - `vfx-text-cursor` (16:9, WebGL) — typing caret reference; for Arabic, type whole words in one joined string.
  - `flash-through-white` (16:9, WebGL) — closest to the end wipe; the reference wipe is simpler (accent band → white → black, bottom-up, 0.3 s) and is easier as a CSS gradient mask.
- **Missing, hand-build in one composition:** one `#camera` wrapper (scale/x/y tweens = the whole camera); SVG/CSS shapes that morph — horizon arc (big circle with a white rim + radial glow) → pill (`border-radius` + width/height tween, `expo.inOut` 600 ms) → send button → rounded tile → full frame; a cursor sprite with hover-scale and click-halo; a typing tween (`textContent` by grapheme/word from `t`, seek-safe) with a 250 ms highlight span on the newest word; the glow floor as a blurred radial gradient rising from the bottom.
- **Result image:** the one colourful thing. Free first — images-gpt with the card's style block, or a frame from the owner's own footage. Never spend credits unasked.
- **Layout 9:16 (1080×1920):** stage full frame; the glass bar / pill centred at y ≈ 860, width 820 px wide shot (≈ 76% of width, matching the reference bar ratio); punch-in keeps the prompt text inside x 60–960; the result tile rises to centre (540, 860) before going full frame; caption pill at y ≈ 1100; glow floor only in the bottom 35%; nothing important below y 1500. Arabic: mirror the prompt box (send on the left, pan goes left).
- **Layout 16:9:** the reference layout; bar centred, glow corner top-left.
- **Rhythm:** a beat every ~1.6 s (calm) / ~1 s (punchy); 0 hard cuts; hold the result ≥ 1.4 s. Full timeline with times in the card under **Edit → Grammar**.
- **Sound:** SFX-only by default, one per beat, from `_library/assets/sfx/el/ (not in the public repo)` (`ui-click`, `ui-type`, `ui-pop`, `riser-ticks`, `whoosh-tonal`, `whoosh-fast`, `impact-soft`, `success-chime`, `stinger-brand`); a 0.1–0.3 s silence before the click, send and expand; −15 LUFS. With voice: voice −14, SFX 6–8 dB under; music only from `_library` / the bgm catalogue, never generated.

## 3. Checks before the owner sees it
1. `npx hyperframes lint` (inside the project) — 0 errors.
2. `npx hyperframes snapshot --at <bar, arc, pill, typing, tile, full, end>` — Read every frame.
3. `npx hyperframes render --quality draft` → `node tools/vid.mjs judge <draft.mp4>` → Read `sheet.jpg` and `safe-sheet.jpg`.
4. Safe zone x 60–960, y 220–1500 · Arabic joined, right-to-left, never split per letter, no `dir="rtl"` on `<html>`.
5. Style checks: ffmpeg scene score < 0.35 everywhere except the end wipe (no accidental hard cuts) · only one accent-coloured element per frame · every morph keeps the same rim + glow · each beat has its sound within ±2 frames · no third-party logos · compare 10 fps strips against `refs/` for the arc → pill and send → result moves.
6. Before asking for approval: replace frames 01–05 with our own 9:16 snapshots in brand roles.

## Do / Don't
- **Do:** one camera wrapper; morph instead of cut; cursor causes every beat; one sound per beat; brand roles; real hold on the result.
- **Don't:** real third-party logos; reference frames to AI tools; per-letter Arabic; grain, glitch, dissolves; more than one accent element at once; spend credits; approve the card yourself.

After the job: `node tools/vid.mjs style comment horizon-prompt-oneshot "<what worked or not>"`.
