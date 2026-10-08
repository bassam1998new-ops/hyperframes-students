---
name: setup
description: First-time setup for the HyperFrames student studio. Checks the computer (Git, Node.js, FFmpeg, the render browser), explains in plain words what is missing, recommends what to install, asks before installing anything, then makes a 3-second test video to prove it all works. Use when the student says "setup", "install", "اعمل setup", "نزّل البرامج", "it doesn't work", "command not found", when node_modules is missing, or when `npx hyperframes doctor` shows a red item. Safe to run again any time — it skips what is already done.
---

# Setup — get a beginner's computer ready

The student is a beginner. Talk in their language, short sentences, one step at a time.
Do the checks yourself. Ask before every install. Never type a password for them.

## 0. Right folder?
This must run inside the studio folder (it has `CLAUDE.md` and `video-projects/_library/`).
If you are somewhere else, find the folder or ask where they cloned it, and `cd` there.

## 1. Check what is there
Find the system (Windows / macOS / Linux) and run these. Don't show the raw output; show a short list.

| Check | Command | Needed? | What it is, in one line |
|---|---|---|---|
| Git | `git --version` | yes | downloads this studio and its updates |
| Node.js 22 or newer | `node --version` | yes | runs HyperFrames |
| npm | `npm --version` | yes | comes with Node.js |
| FFmpeg + FFprobe | `ffmpeg -version`, `ffprobe -version` | yes | joins the frames and the sound into an MP4 |
| Free disk | (doctor shows it) | ~3 GB | for the tools and your videos |

Show it like:
```
✓ Git
✗ Node.js — not installed (needed: it runs HyperFrames)
✓ FFmpeg
```
If everything is ✓, say so and go to step 3.

## 2. Install what is missing — ask first, one at a time
For each ✗: say what it is (one line), that it is free, what you recommend, and ask "Shall I install
it?". Wait for a yes.

**Windows** (winget is built into Windows 10/11):
- Node.js: `winget install -e --id OpenJS.NodeJS.LTS --accept-package-agreements --accept-source-agreements`
- FFmpeg: `winget install -e --id Gyan.FFmpeg --accept-package-agreements --accept-source-agreements`
- Git: `winget install -e --id Git.Git --accept-package-agreements --accept-source-agreements`
- If Windows shows a "Do you want to allow this app to make changes?" box, tell them to click **Yes**.
- If `winget` itself is missing: send them to https://nodejs.org (the LTS button), https://git-scm.com
  and for FFmpeg say "install App Installer from the Microsoft Store, then I'll try again".

**macOS** (uses Homebrew):
- Check `brew --version`. If missing, they must run the installer themselves, because it asks for their
  Mac password. Tell them: open the **Terminal** app, paste the command from https://brew.sh, press
  Enter, type their Mac password (it stays invisible while typing — that's normal), and tell you when
  it's done.
- Then: `brew install node ffmpeg git`

**Linux:** these need their password, so they run them in their own terminal:
`sudo apt install -y git ffmpeg`. For Node.js 22+, recommend the LTS installer from https://nodejs.org.

**After installing anything:** the new program is not visible to this Claude window yet. Tell them:
"Close Claude Code completely, open it again in this same folder, and type `/setup` — I'll continue
from here." Then stop and wait. (When they come back, step 1 will show the new ✓.)

## 3. Install the studio's own parts
Say what each one does and roughly how big it is, then run them in order:
1. `npm install` — downloads HyperFrames into this folder (about 120 MB, about a minute).
2. `npx hyperframes skills` — teaches Claude the official HyperFrames rules (small). Ask first: it
   installs skills for Claude on this computer.
3. `npx hyperframes browser ensure` — downloads a private copy of Chrome used only for making videos
   (~150 MB). Their normal browser is not touched.
4. `npx hyperframes doctor` — the final check. Explain only the red items that matter:
   Node.js, FFmpeg, FFprobe and Chrome must be ✓. These are **optional — ignore them**: a newer
   version available, whisper-cpp (automatic captions), MusicGen (AI music), Docker.

## 4. Prove it works: a 3-second test video
```bash
mkdir -p my-videos && cd my-videos
npx hyperframes init hello-test --example blank --resolution portrait --non-interactive
cd hello-test
```
Put one big word on screen (their name, or "Hello") that fades in, keep it 3 seconds, then:
```bash
npx hyperframes lint
npx hyperframes render --quality draft
```
Find the MP4 in `my-videos/hello-test/renders/`, tell them where it is, and offer to open it.
If it fails, read the error, fix it, and try again. Don't hand them a broken step.

## 5. Done
Tell them, short:
- "Setup is done. Your videos will live in the `my-videos` folder."
- "To make a video, type `/new-video`."
- "Next time: open Claude Code in this same folder." Tell them the folder path you used.
