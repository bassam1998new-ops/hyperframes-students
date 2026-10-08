# HyperFrames student studio — make videos with Claude Code

Reusable looks for [HyperFrames](https://hyperframes.heygen.com) (HTML + GSAP → MP4), shared from a
working video studio that makes short Arabic and English videos (mostly 9:16 reels), plus a
beginner setup so Claude Code can install everything and guide you.

There are no projects, recordings, renders or brand files in here — only the parts you can reuse.

## Start here (beginners)

You only need [Claude Code](https://claude.com/claude-code) installed. Open it, and paste:

> Install the HyperFrames student studio for me. I am a total beginner, so explain every step in
> simple words and ask me before you install anything. First check if Git is installed (if not,
> explain and help me install it). Then clone `<this repo's URL>` into my Documents folder, read
> its `CLAUDE.md` and `.claude/skills/setup/SKILL.md`, and follow the setup step by step.

(Get the URL from the green **Code** button at the top of this page.)

After setup, open Claude Code **in the studio folder** and type:
- `/setup` — check or repair the install (safe to run any time)
- `/new-video` — make a video, step by step

Your own videos go in `my-videos/` — Git ignores that folder, so `git pull` (to get new looks) never
touches your work.

## What is inside

| Folder | What it is |
|---|---|
| `CLAUDE.md`, `.claude/skills/setup/`, `.claude/skills/new-video/` | **Beginner starter**: tells Claude Code to talk simply, check your computer, ask before installing, and walk you through a video. |
| `video-projects/_library/styles/<slug>/style.md` | **Style cards.** One whole look each: tone, palette roles, type, camera, edit rhythm, motion JSON (eases, durations, staggers), sound, calm/punchy modes, AI prompt parts, do/don't. |
| `video-projects/_library/styles/_template/` | A blank style card + a blank style skill, to write your own. |
| `video-projects/_library/styles/neon-node-explainer/frames/` | Style frames for the node-explainer look (rendered from the demo blocks). Other cards list their frames, but those images are not published yet. |
| `.claude/skills/style-<slug>/SKILL.md` | **Style skills** for Claude Code: how to build a video in that look, step by step, with the checks before you show it. |
| `video-projects/_library/assets/kits/node-explainer/` | **The node-explainer kit**: `nx.css` (role tokens + parts) and `nx.js` (global `NX`: themes, icons, connectors, seek-safe tween helpers). Its README lists every part and helper. |
| `video-projects/_library/compositions/` | Two demo blocks built with the kit: `node-explainer-16x9.html` (1920×1080) and `portrait/node-explainer-9x16.html` (1080×1920). |

## Colours are brand roles, not hex

A style is the **quality, the structure and the motion** — not the colours. Every card names colour
**roles** (stage, surface, text, accent, role-1…4, ok/warn/danger). Your brand fills them. The hex
values written in a card are only the look of the reference it was studied from; don't ship them
unless they are your brand's colours.

For the node-explainer kit: `NX.theme(root, { bg, surface, border, text, dim, accent, "accent-2",
"role-1", "role-2", "role-3", "role-4", ok, warn, danger })`. Everything else (tints, glows, chip fills,
readable text on filled tiles) is derived. Light stages switch the kit to light mode by themselves.

## How to use it by hand (without the beginner setup)

1. Have a HyperFrames project (`npx hyperframes init`), and read the HyperFrames docs
   (`npx hyperframes docs compositions`).
2. Pick a look: read its `style.md` and its skill in `.claude/skills/style-<slug>/SKILL.md`.
   With Claude Code, copy the `.claude/skills/style-*` folders into your project's `.claude/skills/`
   and ask for "a video in the <name> style".
3. For the node-explainer look, copy `video-projects/_library/assets/kits/node-explainer/` into your
   project's `assets/kits/node-explainer/` and start from one of the demo blocks. The demo blocks load
   GSAP 3.14.2 + DrawSVGPlugin from jsDelivr and the fonts (Alexandria, Cairo, JetBrains Mono — all
   SIL Open Font License) from the Fontsource CDN. For offline, reproducible renders, download those
   files into your project and point the `<script>` / `@font-face` URLs at the local copies.
4. Lint and check before you render: `npx hyperframes lint`, then `npx hyperframes snapshot` and look
   at the frames.

## Notes

- The skills come from a bigger private workspace. Lines like `node tools/vid.mjs style apply …`,
  `vid use`, `vid judge` or `director/decisions.md` refer to its helper CLI and project folders, which are
  not part of this repo. Do the same step by hand: copy the block, set the variables, render a draft,
  look at the frames.
- Paths marked "(not in the public repo)" point to files that were held back (example renders, test
  notes, frames cut from real client or course videos).
- The demo blocks had two small UI sounds; they were removed here. Add your own `<audio>` tags (see the
  kit README, "Sound").
- Arabic text: never put `dir="rtl"` on `<html>`, and never split Arabic text per letter — the cards
  and the kit already follow this.

## License

MIT — see `LICENSE`. The fonts the demo blocks load (Alexandria, Cairo, JetBrains Mono) are under the SIL Open Font License; GSAP has its own license (gsap.com).
