---
id: horizon-prompt-oneshot
name: Horizon Prompt One-shot
status: draft
version: 1
modes: [calm, punchy]
use_when: [AI tool show-off / "watch what it makes" teaser, prompt-to-result demo, course or service promo opener, launch teaser for an AI feature, channel bumper with a logo end, no-person graphics-only video]
avoid_when: [talking head on screen, real screen-recording proof (looks staged next to it), data-heavy explainers, long tutorials with many steps, any video that would need real third-party logos without permission]
brand: any
blocks: [yt-camera-move-9x16, glass-cards-9x16, tracking-typography-9x16, vfx-text-cursor, flash-through-white]
approved_by:
approved_on:
approved_words:
skill: style-horizon-prompt-oneshot
---
# Horizon Prompt One-shot

**Tone (one sentence):** A premium, quiet product-film feel — one continuous camera on a near-black stage lit by a soft planet-horizon glow, where a glass app bar, a cursor and a prompt box morph into each other until the typed prompt "blooms" into a full-frame result, then a logo sting closes it.
**Inspired by (technique, not a copy):** the 16.9 s 16:9 reference the owner shared on 2026-10-03 (Downloads, creator unknown; SFX-only, no voice, no music bed). Techniques: one-shot camera with no hard cuts, digital punch-ins instead of cuts, UI shapes that morph (horizon arc → pill → send button → image tile → full frame), cursor-driven beats, live typing with a highlight on the newest letters, bottom-up light wipe to a logo end card, every visual event hit-synced to its own UI sound.

## Look
- **Palette:** roles, not hex — the brand fills them. Palette = roles; the brand fills the hex. Test default (the reference, sampled with ffmpeg region means): stage #020000 · glow-hot #e6e6f8 · glow-mid #9195cc · glow-band #6786d5 · glow-floor #ecedfd · accent #316ded · rim/text #ffffff — stage fills ≥ 85% of every frame until the result; the accent appears on ONE element at a time (send button, then the result tile, then the wipe band), max ~3% of the frame; glow comes only from one edge (top-left corner, then the bottom floor, then a bottom dome).
  - Roles: `stage` near-black canvas · `glow` (hot → mid → band → stage, a 4-stop radial falloff) from the brand primary lightened · `floor` the pale top of the bottom glow · `accent` brand primary (button, tile, wipe band) · `rim` 1–2 px white-ish outline on every glass shape · `text` white.
- **Type:** Arabic IBM Plex Sans Arabic 500/700 or Alexandria 500 (vendored) · Latin Inter 500 / DM Sans 500 · weights 500 for UI text, 500–700 for the wordmark · sentence case, UI-sized: prompt text = 2.0% of frame height in the wide shot, 4.2% after the punch-in; wordmark = 8% of frame height at its hero size.
- **Texture:** none — clean digital; soft glow only (no grain, no noise, no bloom on text). Glass = black fill + 1.5 px rim + 18–30 px outer white glow at 25–40% opacity.
- **Grade:** none — graphics only; the generated result image keeps its own warm-sunset grade as the one colour burst of the video.

## Camera, light, performance
- **Camera:** one virtual camera, never cut: slow push (~3%/s scale) and drift on every hold; 2 digital punch-ins (3.03 s ×≈1.5, 8.9 s ×≈1.7) that jump scale in 1 frame; a 0.7 s pan right (10.3–11.0 s) to follow the action to the send button; the result tile scales to full frame in 0.35 s (12.6–12.95 s).
- **Lighting:** a single soft "planet" light source per scene — top-left corner glow (0–4.6 s), a horizon arc with a white rim and indigo falloff (5.7–6.8 s), a lavender-white glow floor across the bottom 35% (6.8–14.4 s), a dome glow rising from the bottom on the end card (15.0–16.9 s). Selected items get a blue halo.
- **Performance:** none — no person. The "actor" is the cursor: hovers (icon scales ~1.3×), clicks (halo + sound), leaves frame after each action.

## Edit
- **Rhythm (measured):** 0 hard cuts in 16.9 s (ffmpeg scene score max 0.32, only at the end wipe 14.47 s) · a new beat every ~1.6 s (about 10 beats) · longest hold ~1.9 s (result image 13.0–14.4 s) · beats land on the cursor click or a UI sound, not on music (there is no music).
- **Grammar:** one-shot morph chain — glass bar draws in (0–0.4 s) → icons pop in (0.5–1.1 s, ~0.1 s stagger) → hover across icons (3.1–4.3 s) → click, others fade (4.3–4.7 s) → logo alone, wordmark + horizon arc rise (5.6–6.5 s) → arc squashes into a pill (6.8–7.4 s) → placeholder, then punch-in and typing (~17 chars/s, 9.0–10.3 s) → pan to send, click (11.0 s) → button grows into a rounded tile that rises and fills with the result (11.1–12.5 s) → tile to full frame (12.6–12.95 s) → glass caption pill (13.0–13.5 s) → bottom-up light wipe (14.4–14.7 s) → logo end card (14.8–16.9 s).
- **Transitions:** shape morph (arc → pill → button → tile), digital punch-in, scale-to-full-frame (zoom-through on a tile), bottom-up gradient wipe (accent band → white → black, 0.3 s). No dissolves, no glitch, no hard cuts.

## Motion (HTML / GSAP)
```json
{ "ease": { "enter": "power3.out", "exit": "power2.in", "emphasis": "back.out(1.4)", "morph": "expo.inOut", "camera": "sine.inOut" },
  "duration_ms": { "micro": 100, "standard": 350, "hero": 700 },
  "stagger_ms": 100,
  "bar_draw_ms": 400, "icon_pop_stagger_ms": 100, "hover_scale": 1.3, "click_halo_ms": 300, "fade_others_ms": 300,
  "arc_rise_ms": 800, "arc_to_pill_ms": 600, "punch_in_scale": [1.5, 1.7], "punch_in_frames": 1,
  "camera_push_pct_per_s": 3, "pan_ms": 700, "type_chars_per_s": 17, "new_letter_highlight_ms": 250,
  "button_to_tile_ms": 300, "tile_fill_ms": 400, "tile_to_full_ms": 350, "caption_in_ms": 450, "result_hold_ms": 1400,
  "wipe_ms": 300, "end_logo_fade_ms": 250, "end_wordmark_ms": 700, "glass_rim_px": 1.5, "glass_glow_px": [18, 30] }
```
- **Text animations:** live typing with a caret and a 250 ms blue-white highlight on the newest characters; placeholder fade-in; wordmark reveal next to the logo while the logo slides left; caption pill fades in with tracking settling. Arabic: typing by whole word or by grapheme cluster on the joined string (never split into separate letter spans); the end wordmark reveals as a clip-mask wipe from the right, never per letter.
- **Rules:** one moving thing at a time (the camera, the cursor or a morph); every morph keeps the same rim + glow so the eye tracks one object; the accent colour lives on one element at a time; hold ≥ 1.2 s on the result; RTL — on Arabic the prompt box is mirrored (send button on the left, pan goes left).

## Sound
- **Music:** none in the reference — pure UI sound design. With a voice-over add a quiet ambient/tech bed from `_library` music / the bgm catalogue (never generate music) at about −24 LUFS.
- **SFX:** hit-sync on every beat, about 12 in 16.9 s: soft riser/shimmer under the icon pop-ins, `ui-click` on hover/click, a tonal chime when the logo lifts, `riser`/whoosh into the arc, `ui-type` ticks during typing, `ui-click` on send, a bright arpeggio while the tile fills, `impact-soft` + whoosh on tile-to-full (the loudest hit, −6 dB RMS at 12.8–13.0 s), a whoosh on the wipe, a soft stinger on the end logo. Short silences (≈0.1–0.3 s) right before the click, send and expand make them land.
- **Mix:** measured reference: −15.1 LUFS integrated, LRA 4.3 LU, true peak −0.8 dBFS, no speech (faster-whisper base VAD: 0 segments). Ours: SFX-only at −15 LUFS; with voice, voice −14 and SFX tucked 6–8 dB under it.

## Modes
- **calm:** the reference pace — beat every ~1.6 s, slow 3%/s push, 1.4–2 s hold on the result, soft SFX, no stinger.
- **punchy:** beat every ~1 s, skip the icon dock (start on the logo + arc), 3 punch-ins, typing at ~25 chars/s, 3–4 results in a row (each tile → full frame → next prompt), stinger + impact on every result.

## Prompt parts
<!-- The UI and motion are built in HyperFrames. AI tools are only for the RESULT image/clip that blooms out of the tile. -->
- **Style block:** premium cinematic still, natural golden-hour light, rich warm colour, high detail, wide composition with a clear centre for a caption pill, no text {SUBJECT}
- **Keep:** the result is the only warm/colourful thing in the video; the UI stays near-black with brand glow; one subject per result.
- **Avoid:** watermark, written text or Arabic in the image, logos, UI chrome in the image, distorted hands, oversaturated HDR.

## Per tool
- **images-gpt:** only for the result image(s), with the style block — not checked yet (2026-10-03)
- **flow-veo:** optional for a moving result (slow push-in on the generated still) — not checked yet
- **higgsfield:** none — never spend credits on this look unasked
- **hyperframes:** the whole UI chain (glass bar, icons, cursor, arc, pill, typing, tile, wipe, end card) — hand-built, no kit yet; motion tokens above, palette roles as CSS variables

## Frames
- frames/01-glass-bar-corner-glow.png (not in the public repo) — the empty glass bar drawing in on black, the hot corner glow top-left (0.9 s, reference, 16:9)
- frames/02-horizon-arc-wordmark.png (not in the public repo) — logo + wordmark above the rising horizon arc with a white rim and indigo falloff (6.3 s, reference)
- frames/03-pill-on-glow-floor.png (not in the public repo) — the arc squashed into a thin pill sitting on the lavender glow floor (7.9 s, reference)
- frames/04-typing-punch-in.png (not in the public repo) — punched-in prompt box mid-typing, newest letters highlighted, send button in the accent blue (9.9 s, reference)
- frames/05-result-tile-rise.png (not in the public repo) — the send button grown into a rounded tile filled with the result, rising off the pill (12.1 s, reference)

## Do / Don't
- **Do:** keep it one continuous camera; morph shapes instead of cutting; let the cursor cause every beat; sync one sound to each beat; give the result a real hold; brand roles for every colour; build our own 9:16 frames (brand roles, our logo or none) before asking the owner to approve.
- **Don't:** use real third-party AI logos/wordmarks (the reference shows several — technique only); send the reference frames to AI tools; split Arabic per letter; put more than one accent-coloured thing on screen; add grain, glitch or dissolves; spend credits.

## Tests
- (test notes are kept in the private workspace)
