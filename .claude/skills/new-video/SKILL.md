---
name: new-video
description: Make a new video with a beginner, start to finish — a few easy questions, pick a look from this repo's styles, build it with HyperFrames, check the frames, render and show it. Use when the student says "new video", "make a video", "اعمل فيديو", "عايز فيديو", "reel", "animation", or asks how to start a video. Hands the technical HyperFrames rules to the official hyperframes skills.
---

# New video — beginner flow

Talk in their language, short sentences. Ask only what changes the video. Do the rest yourself.
If setup was never done (no `node_modules/`), run `/setup` first.

## 1. Four quick questions (one message, with choices)
1. **What is it about?** One sentence: the message, or what people should do after watching.
2. **Shape:** phone / Reels / TikTok (vertical 9:16) — recommended — or YouTube (wide 16:9)?
3. **Length:** 10, 20 or 30 seconds? (Recommend the shortest one that fits the message.)
4. **Text language** on screen: Arabic, English or both?

Optional, only mention once: "Do you have a logo, colours, a voice-over or video clips? Drop the
files in the chat or tell me where they are — or we go without." Never invent facts, prices or names.

## 2. Pick a look
List the styles in `video-projects/_library/styles/` (skip `_template`). For each one, one line from
its `style.md` (what it feels like, what it is good for). Show the images in its `frames/` folder if
there are any. Recommend the one that fits their topic, or "a simple clean look" if none fits.
Wait for their pick.

## 3. Write the words first
Write the on-screen text scene by scene (one short line per scene, 2–4 seconds each) and show it as a
short numbered list. Ask: "Change anything?" Build only after they say OK.

## 4. Build
```bash
cd my-videos
npx hyperframes init <short-name> --example blank --resolution portrait --non-interactive   # or landscape
cd <short-name>
```
- If the style has a demo block or kit, use it (how: see "Looks" in `CLAUDE.md`), and follow its style
  skill `.claude/skills/style-<name>/SKILL.md`.
- Follow the official `hyperframes` skills for the composition rules.
- Copy any files they gave you into `assets/` inside the video folder.

## 5. Check before showing
```bash
npx hyperframes lint
npx hyperframes snapshot
```
Read the frames yourself: text inside the screen (not cut at the edges), nothing blank, nothing
overlapping, Arabic joined and right-to-left, scenes in the right order. Fix and check again.

## 6. Show it
```bash
npx hyperframes render --quality draft
```
Tell them where the MP4 is (`renders/` inside the video folder) and offer to open it. Also mention
`npx hyperframes preview` to watch and scrub it in the browser.
Ask: "What would you change?" Change it, check again, render again.
When they're happy: `npx hyperframes render --quality standard` for the final file.
