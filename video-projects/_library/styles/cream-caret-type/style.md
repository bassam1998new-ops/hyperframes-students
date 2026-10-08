---
id: cream-caret-type
name: Cream Caret Type
status: draft
version: 1
modes: [calm, punchy]
use_when: [channel or "who am I" intro reel, course or service intro hook, 3–6 s opener before a talking head, word-play promise line ("I explain / test / filter … tech for you"), series bumper or end card, text-only reel with no voice]
avoid_when: [talking head on screen the whole time, real screen-recording proof, data-heavy explainers, full spoken-subtitle captions over a long voice-over, music-led montage]
brand: any
blocks: [mk-hook-title-ar-portrait, mk-callout-highlight-9x16, icon-animation-9x16, yt-camera-move-9x16, mk-cta-endcard-portrait]
approved_by:
approved_on:
approved_words:
skill: style-cream-caret-type
---
# Cream Caret Type

**Tone (one sentence):** A quiet, clever "text editor" intro — Arabic words are typed with a coloured caret on a flat two-colour page, selected, deleted and retyped, and one coloured dot jumps out of a word into a flat vector eye before the line becomes a one-word-swap promise, every move landing on its own small sound.
**Inspired by (technique, not a copy):** the 16.1 s Arabic (Levantine) creator intro the owner shared on 2026-10-03 (Downloads; 720×1280, 30 fps, no voice, no music — the text IS the voice). Techniques only: typewriter Arabic with a caret, a Figma-style measuring guide on the first word, select-highlight then retype, a flat profile silhouette as the only image, a dot-to-iris match cut, a zoom-through the iris, a fixed noun with a swapping bold verb every 16 frames, a pixel-art icon on the sign-off, an app-icon monogram end card. Never his name, words, silhouette, logo or "> letter _" mark.

## Look
- **Palette:** roles, not hex — the brand fills them. Test default (the reference, measured with ffmpeg area-average): night #0E1A2B · paper #F8F1EC · accent #FA692C · muted #8E93A8 (fading words, guide labels; lightest grey seen #C0BEC5) · tile #16233B (end-card tile, one step lighter than night). Rule: only TWO big fields (night, paper) that swap by hard cut; accent ≤ 3% of the frame (caret, selection, one dot, underline, icon) except the eye scene where the iris is ~10%; no gradients.
  - Palette = roles; the brand fills the hex. night = brand dark canvas (also the silhouette and the ink on paper) · paper = brand light canvas (also the sclera and the ink on night) · accent = brand primary (one thing at a time) · muted = brand muted · tile = night lifted ~5%.
- **Type:** Arabic: one geometric Arabic sans in 2 weights — the reference looks like IBM Plex Sans Arabic (not verified); use IBM Plex Sans Arabic 400 + 700 (local in `_library/assets/fonts (not in the public repo)`), or Cairo 400/700 / Alexandria 500/800 if the brand says so · Latin: the same family's Latin cut (IBM Plex Sans Arabic latin 400/700) · weights: 700 for hero words, 400 for the "fixed" word, and the two-weight pair inside one line (first word 400 + second word 700; noun 400 + verb 700) · sizes measured on a 1080×1920 frame: hero typed word glyph box 357 × 188 px (≈ 200 px font, the guide labels read these numbers), side word ≈ 115 px, swap row ≈ 85 px, sign-off word ≈ 120 px, small line ≈ 55 px, name-style line ≈ 48 px · ONE word or one short line on screen at a time, never a paragraph · letter-spacing 0.
- **Texture:** none — flat fills, no grain. Optional for the first beat only: a measuring-guide overlay (1 px dashed hairlines at the text box edges running full width/height, paper-on-night ≈ #2A3A55 / night-on-paper ≈ #D9D1CB, plus 10–12 px muted "357px / 188px" labels that update as the word grows), gone by ~1.5 s.
- **Grade:** none — graphics only. When a real face plate is used, flatten it to a silhouette (night fill) rather than grading it.

## Camera, light, performance
- **Camera:** 2D only. Static centred page for type; one fast digital push on the silhouette (0.2 s, motion-blurred, 2.47–2.67 s) that re-frames the profile from centred to cropped left half (face edge at x ≈ 0.45 W); one zoom-through into the iris (0.14 s, 8.63–8.77 s) that cuts to the paper page; no drift, no shake.
- **Lighting:** none — flat two-colour fills; the only highlight is the white catch-light dot in the iris.
- **Performance:** no person on camera. The "actor" is the caret (types, selects, deletes) and the eye (lid opens 7.0–7.2 s, pupil turns to a slit, iris darts right with a 3-ghost motion trail 7.3–7.5 s and back 7.7–8.0 s). A silhouette of the presenter's profile stands in for the face (made from the owner's own photo — never generated, never the reference's).

## Edit
- **Rhythm (measured, ffmpeg scdet):** hard cuts at 0.53 · 1.60 · 2.67 · 6.40 · 8.70 · 14.40 s → 7 shots, average 2.3 s, shortest 0.53 s (night intro), longest 5.7 s (the swap page 8.7–14.4) · inside the long page the bold verb swaps every 0.53 s = 16 frames (9.07, 9.60, 10.13, 10.67, 11.20) · typing ≈ 0.1 s per letter for a hero word (أ at 0.3 → full 5-letter word at 0.7), ≈ 0.06 s per letter for a small line · each text holds 0.8–1.7 s after it is complete · end card holds 1.7 s.
- **Grammar:** type → (hold) → select-highlight → delete → retype a new word (the "edit the sentence live" gag); word fades to muted except ONE letter-dot that turns accent → hard cut to a giant shape whose centre is that dot (match cut); fixed noun + swapping verb slot; text-only beats separated by background colour flips (night ↔ paper) on hard cuts.
- **Transitions:** hard cut with a colour flip · match cut (dot → iris) · digital push-in with motion blur · zoom-through (push into the iris until it fills, cut to paper) · horizontal slide-in with motion blur for a word entering beside the eye. No dissolves, no wipes, no glitch.

## Motion (HTML / GSAP)
```json
{ "ease": { "enter": "power3.out", "exit": "power2.in", "emphasis": "back.out(1.7)", "push": "expo.in", "slide": "expo.out" },
  "duration_ms": { "micro": 100, "standard": 300, "hero": 530 },
  "stagger_ms": 60,
  "type_ms_per_letter_hero": 100, "type_ms_per_letter_small": 60, "type_unit": "grapheme cluster (Intl.Segmenter), never a code unit",
  "caret": { "width_px": 4, "height_px_on_188px_word": 151, "solid_while_typing": true, "blink": false, "hide_after_done_ms": 400 },
  "select_highlight": { "fill": "accent", "alpha": 0.4, "in_ms": 100, "hold_ms": 200 },
  "swap_every_ms": 533, "swap_icon_px": 36, "underline_draw_ms": 200,
  "fade_to_muted_ms": 300, "match_cut_hold_ms": 100,
  "push_in_ms": 200, "push_scale": 1.9, "zoom_through_ms": 140, "zoom_through_scale": 12,
  "slide_in_px": 260, "slide_in_ms": 300, "motion_blur_px": 18,
  "eye": { "lid_open_ms": 200, "dart_ms": 200, "ghosts": 3, "ghost_alpha": [0.45, 0.25, 0.12] },
  "end_card_hold_ms": 1700 }
```
- **Measured vs estimated:** cut times, swap period, typing speed, holds, sizes and colours are measured; push_scale, zoom_through_scale, slide_in_px, motion_blur_px and the eye timings are read off 10 fps strips (±0.1 s / ±20%).
- **Text animations:** Arabic typewriter (substring reveal of whole grapheme clusters in ONE text node — the browser re-shapes the joined word each step, exactly like the reference "أهل → أهلين") with a solid accent caret on the left (RTL end) of the text; select-highlight (accent at 40% behind the word) → delete → retype; fade-to-muted with one accent dot kept; bold-verb swap (hard swap on the frame, no tween, + a 36 px accent icon pop above the verb with back.out); stepped underline draw-on under the fixed word (accent first, then ink); slide-in with horizontal blur; pixel-art icon pop + 2-cycle wave.
- **Rules:** one word or one short line at a time; typing never splits a word into per-letter elements (shaping breaks) — only grow one string; shadda and other marks type together with their letter; the caret sits at the visual LEFT of Arabic text; swaps cut on frame boundaries (no crossfade); every visual event gets one sound; safe zone x 60–960, y 220–1500 — the reference's side text reaches x ≈ 1005 on a 1080 frame, ours stops at 960.

## Sound
- **Music:** none in the reference — sound-design-led with true silence (< −40 dB) between hits. Calm mode keeps it that way; if a bed is wanted, a very quiet minimal pluck/lo-fi bed from `_library/assets/music (not in the public repo)` or the bgm catalogue at −28 LUFS (never generate music).
- **SFX:** one sound per visual event (spectrogram-checked): soft thump + click on each hard cut (low body ~100 Hz, 0.53 / 1.60 / 13.33 s) · keyboard clicks while typing (2.4–2.9, 12.3–12.8 s) · short pitch-drop blip as a word builds (4.8 s) · deep boom with a ~1.4 s sub tail on the match cut to the eye (6.4 s) · reverse swell into the zoom-through (8.5–8.7 s) · five tonal pops on the verb swaps, each a step higher (fundamental ≈ 550 → 900 Hz, a rising scale) · sub boom + noise tail under the end card (14.4 s → end). Library: `sfx/el/ui-type.mp3`, `impact-soft.mp3` / `impact-tight.mp3`, `impact-deep.mp3` or `sub-drop.mp3`, `whoosh-reverse.mp3`, `ui-pop.mp3` (pitch each swap up with `playbackRate` steps or 5 pre-pitched copies), `stinger-brand.mp3`.
- **Mix:** reference integrated −15.4 LUFS, LRA 4.6 LU, true peak +1.6 dBFS (it clips — don't copy). Ours: SFX-only master at −14 LUFS, ceiling −1 dBTP. With the owner's voice-over: voice −14 LUFS first, SFX ducked ~−6 dB under speech, keep the gaps silent.

## Modes
- **calm:** the reference pace — typing at 0.1 s/letter, 0.8–1.7 s holds, one match cut, swaps every 0.53 s for 4–5 verbs, no music, soft thumps.
- **punchy:** typing 0.05 s/letter, holds 0.5–0.8 s, a colour flip on every line, swaps every 0.4 s (12 frames), push-ins on every hero word, a faint quiet pluck bed under the SFX.

## Prompt parts
<!-- The look is HTML type + flat SVG; AI image tools are only for an optional extra flat icon or silhouette clean-up. -->
- **Style block:** flat vector illustration, two flat colours only ({BRAND NIGHT} and {BRAND PAPER}) with one small {BRAND ACCENT} detail, solid fills, no outlines, no gradients, no texture, no shadow, centred on an empty plain background, vertical 9:16 {SUBJECT}
- **Keep:** two flat fields + one accent dot, solid shapes, lots of empty space, centred composition.
- **Avoid:** any letters or Arabic text in the image (all words go in HyperFrames), gradients, 3D, photo texture, outlines, extra colours, logos, watermarks, the reference creator's likeness.

## Per tool
- **images-gpt:** only for an optional flat icon or to turn the owner's own profile photo into a clean silhouette (or do it free in code: threshold + fill) — not checked yet (2026-10-03). Do NOT send frames/ 01–05 to AI tools: they are reference stills of another creator.
- **flow-veo:** none — not needed; everything is type and flat shapes in HTML.
- **higgsfield:** none — never spend credits on this look.
- **hyperframes:** motion tokens above + palette as CSS variables (`--night`, `--paper`, `--accent`, `--muted`, `--tile`); type with local IBM Plex Sans Arabic; eye and icons as inline SVG; the typewriter, guide overlay, match cut, zoom-through and verb-swap slot are not in the library yet (hand-build at the first job — see the skill).

## Frames
- frames/01-typed-word-measure-guides.png (not in the public repo) — reference still @1.0 s (upscaled to 1080×1920): a bold hero word just typed on paper, centred at y ≈ 48%, Figma-style dashed guides and "357px / 188px" labels
- frames/02-select-highlight-silhouette.png (not in the public repo) — reference still @2.3 s: flat night profile silhouette on paper, the word inside the head selected with a 40% accent box and the accent caret
- frames/03-flat-eye-blur-slide.png (not in the public repo) — reference still @7.55 s: the match-cut eye (paper sclera, accent iris, night slit pupil, white catch-light) mid-dart, a word sliding in from the right with horizontal blur
- frames/04-verb-swap-icon-underline.png (not in the public repo) — reference still @9.3 s: centred row "noun 400 + verb 700" with an accent dot above the verb and a stepped accent underline under the noun
- frames/05-bold-word-pixel-icon.png (not in the public repo) — reference still @13.55 s: one bold sign-off word with a pixel-art waving hand

## Do / Don't
- **Do:** let typing carry the voice (one idea per line); keep two flat fields + one accent; grow Arabic as one string per grapheme cluster; put one sound on every event and silence between; make our own 3–6 frames from the first HyperFrames build (with the owner's silhouette and Egyptian copy) and replace the reference stills before asking for approval.
- **Don't:** copy the creator's name, lines ("بفهّمك/ببسّطلك… التقنية", "وهلأ كلو تمام"), silhouette, logo or "> م _" mark; send frames/ to AI tools; split Arabic into per-letter spans or put `dir="rtl"` on `<html>`; crossfade the swaps; let side text pass x 960; clip the master (+1.6 dBTP in the reference).

## Tests
- (test notes are kept in the private workspace)
