---
name: style-cream-caret-type
description: Build a video in the Cream Caret Type look (style card cream-caret-type) — Arabic words typed with a coloured caret on a flat two-colour page (night and paper that swap on hard cuts), select-highlight → delete → retype, a flat profile silhouette, one coloured dot that match-cuts into a flat vector eye, a zoom-through the iris, a fixed noun with a bold verb swapping every 16 frames, a pixel-art icon on the sign-off and a monogram end card — one sound per event, silence between. Use when the director picked this card, or the owner says "the typing intro", "caret type", "cream caret", "زي فيديو الكتابة", "الكلام اللي بيتكتب", "intro بالكتابة", or the video is a channel / "who am I" intro, a course or service intro hook, a short opener before a talking head, a word-play promise line or a bumper. 9:16 only, Arabic-first. Not for talking heads the whole time, screen-recording proof, data-heavy explainers or full spoken subtitles. DRAFT — untested.
---

# Style: Cream Caret Type

A "live text editor" intro: two flat fields, one accent colour, Arabic typed letter by letter with a caret, edited on screen, one dot that becomes an eye, then a noun with a swapping bold verb. The text is the voice; every move has its own small sound.
Card: `video-projects/_library/styles/cream-caret-type/style.md` — status **draft** (say so to the owner until he approves it on the board). Nothing of this look has been built or rendered yet.

**Look first** (in the style folder): `frames/01-typed-word-measure-guides.png (not in the public repo)` · `frames/02-select-highlight-silhouette.png (not in the public repo)` · `frames/03-flat-eye-blur-slide.png (not in the public repo)` · `frames/04-verb-swap-icon-underline.png (not in the public repo)` · `frames/05-bold-word-pixel-icon.png (not in the public repo)`. These are **reference stills of another creator** — look only, never send them to AI tools, replace them with our own frames after the first build. Motion: `refs/ref-typing-10fps.jpg (not in the public repo)`, `refs/ref-dot-to-eye-matchcut-10fps.jpg (not in the public repo)`, `refs/ref-eye-zoom-through-10fps.jpg (not in the public repo)`; sound: `refs/ref-audio-spectrogram.jpg (not in the public repo)`; story: `refs/README.md (not in the public repo)`.

## 0. Apply the card first
```bash
node tools/vid.mjs style apply cream-caret-type <project> [--mode calm|punchy]
node tools/vid.mjs style show cream-caret-type
```
Copy: Egyptian Arabic written natively (never translate the reference's Levantine lines); show the owner the words before building.

## 1. Colours = roles (the brand fills the hex)
Style = quality, structure and motion. **Never ship the reference navy / cream / orange unless the brand says so.**
| Role | CSS token | Test default (reference) | From `brand/<name>.md` |
|---|---|---|---|
| night field, silhouette, ink on paper | `--night` | #0E1A2B | dark canvas / text-strong |
| paper field, sclera, ink on night | `--paper` | #F8F1EC | light canvas |
| caret, selection (40%), one dot, iris, underline, icon | `--accent` | #FA692C | primary — one thing at a time, ≤ 3% of frame |
| fading words, guide labels | `--muted` | #8E93A8 | muted |
| end-card tile | `--tile` | #16233B | night lifted ~5% |

## 2. Build it
- **Library first:** `node tools/vid.mjs find --portrait --arabic-safe …` + `director/library.md`. Closest blocks (`node tools/vid.mjs use <block> <project>`):
  - `mk-hook-title-ar-portrait` — bold Arabic hero word with local Cairo + RTL-safe layout; reuse the shell, replace its mask reveal with the typewriter.
  - `mk-callout-highlight-9x16` — per-word spans driven by one scalar from word timings; use for the 400 + 700 two-weight line and the fade-to-muted with one word kept.
  - `icon-animation-9x16` — Lucide stroke draw-on icons; the 36 px accent icon above the swapping verb.
  - `yt-camera-move-9x16` — digital punch-in with defocus; the 0.2 s push on the silhouette (add motion blur).
  - `mk-cta-endcard-portrait` — base for the monogram tile end card (the owner's own mark, never the reference's).
- **Hand-build (not in the library yet):**
  1. *Arabic typewriter + caret* — one text node, `el.textContent = clusters.slice(0, n).join('')` from a GSAP proxy `{n}` (seek-safe); split with `Intl.Segmenter('ar', {granularity: 'grapheme'})` so shadda/harakat type with their letter. Pattern exists for Latin only in `_library/assets/kits/node-explainer/nx.js` `type()` (it slices code units — don't use it for Arabic as is). Caret = a 4 px accent bar at the text's visual LEFT, solid while typing, hidden ~0.4 s after the word is done (no blink seen).
  2. *Select → delete → retype* — accent box at 40% behind the word (100 ms in, 200 ms hold), then `n` back to 0 in one frame, then type the new word.
  3. *Measuring-guide overlay* (first beat only) — 1 px dashed lines on the text's bounding box, full width/height, and muted 11 px "WIDTHpx / HEIGHTpx" labels read from `getBoundingClientRect()` each update.
  4. *Dot → eye match cut* — the word fades to `--muted` in 0.3 s while one dot (a small accent circle placed over the letter's dot, not the glyph itself) stays; hard cut to an SVG eye whose iris centre = that dot's position. Eye: almond path in `--paper` on `--night`, accent iris + night slit pupil + white catch-light; lid open 0.2 s, dart right 0.2 s with 3 ghost copies (alpha 0.45/0.25/0.12), back.
  5. *Zoom-through* — scale the eye group ~12× into the iris in 0.14 s (expo.in) + blur, hard cut to paper.
  6. *Verb-swap slot* — fixed noun (400) + verb (700) in one RTL line; swap the verb text on exact frame boundaries every 0.533 s (16 frames at 30 fps), icon pops with back.out(1.7), stepped underline (SVG polyline) draws under the noun in 0.2 s.
  7. *Silhouette* — from the owner's own profile photo (threshold + fill `--night`, free, in code or once with ffmpeg); never generated, never the reference's.
  8. *Pixel-art icon* — an SVG of small squares (e.g. waving hand), 2 wave cycles.
- **Layout 9:16 (1080×1920):** single centred word/line at y ≈ 918 (48%); side text beside the silhouette right-aligned at x ≤ 960 (the reference goes to ~1005 — don't); everything inside x 60–960, y 220–1500; bottom 20% empty. Sizes: hero ≈ 200 px (700), side word ≈ 115 px, swap row ≈ 85 px, small line ≈ 55 px, letter-spacing 0, `dir="rtl"` on the text element only.
- **Layout 16:9:** not built — no reference for it.
- **Motion tokens:** the ```json block in the card (typing 100 ms/letter hero, 60 ms small; swap 533 ms; push 200 ms; zoom-through 140 ms; slide-in 300 ms with 18 px blur; end card 1.7 s).
- **Captions:** this look has no subtitle bar — on-screen words are the script. If the owner's voice is added, time each typed line to his words with the `arabic-captions` skill (Scribe first, or local faster-whisper large-v3 aligned to the script; close Whisper after use) and type the KEY phrase only, not every word.
- **Sound:** SFX-only, one hit per event, silence between: `sfx/el/ui-type.mp3` while typing · `impact-soft.mp3` / `impact-tight.mp3` on cuts · `impact-deep.mp3` or `sub-drop.mp3` on the eye · `whoosh-reverse.mp3` into the zoom-through · `ui-pop.mp3` on each swap, pitched up one step each · `stinger-brand.mp3` under the end card. Master −14 LUFS, ceiling −1 dBTP. Music only in punchy mode, quiet, from `_library/assets/music (not in the public repo)` (never generate music).

## 3. Checks before the owner sees it
1. `npx hyperframes lint` inside the project — 0 errors, no remote fonts/GSAP.
2. `npx hyperframes snapshot --at <mid-typing, selected, eye, swap 1, swap 3, end>` — Read every frame: Arabic joined at every typing step (no lone shadda, no broken forms), caret on the left.
3. `npx hyperframes render --quality draft` → `node tools/vid.mjs judge <draft.mp4>` → Read `sheet.jpg` and `safe-sheet.jpg`.
4. Safe zone x 60–960, y 220–1500 · Arabic right-to-left, never per-letter spans, no `dir="rtl"` on `<html>`.
5. Style checks: two fields + one accent only; swaps land on frame boundaries (step through 16-frame spans); every visual event has a sound and the gaps are silent (`ffmpeg … showspectrumpic` next to `refs/ref-audio-spectrogram.jpg (not in the public repo)`); true peak ≤ −1 dBTP; none of the reference's words, name, silhouette or mark.

## Do / Don't
- **Do:** one idea per typed line; grow Arabic as one string by grapheme cluster; use the owner's own silhouette and mark; make 3–6 of OUR frames from the first build and swap out the reference stills; judge typing at 30 fps strips against `refs/ref-typing-10fps.jpg (not in the public repo)`.
- **Don't:** copy the reference copy or identity; crossfade the swaps; add grain, gradients or a third big colour; send frames/ to AI tools; spend credits on this look; approve the card yourself.

After the job: `node tools/vid.mjs style comment cream-caret-type "<what worked or not>"`.
