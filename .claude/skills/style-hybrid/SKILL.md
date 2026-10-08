---
name: style-hybrid
description: Remix 2+ existing style cards of the Hyperframes video workspace into one NEW draft style card, layer by layer (palette roles, type, texture, grade, camera, light, edit rhythm, transitions, motion, sound, prompt parts), then let the owner pick the skills for the video and start the director. Use when the owner says "hybrid style", "remix styles", "mix two styles", "combine styles", "اعمل هايبرد", "ادمج الستايلين", or ticks cards and presses "Remix these" on the Styles board.
---

# Style hybrid — remix cards into a new draft

Workspace: the repo root (run commands from there). Agents propose, the owner decides. The new card is a **DRAFT** until he approves it — never write `status: approved` yourself.

## 1. Open the Styles board in hybrid mode
Open **http://localhost:3000/board/styles?hybrid=1** in the Claude desktop in-app browser (Browser pane: `navigate`). Tell the owner in one line: "Tick 2 or more styles, pick a parent per layer if you want, write notes, press **Remix these**."
- First check nothing is already waiting: `node tools/vid.mjs style hybrid list`. If a request is waiting, use it (step 3).
- Home not answering? `curl -s -m 5 http://127.0.0.1:3000/api/state`. Never kill Home yourself — say so.

## 2. Wait for his press (it is a gate — silence is not a yes)
```bash
node tools/vid.mjs style hybrid wait --timeout 1800
```
It returns the request id, the parents, his notes and the layer table. Exit 3 = no press yet → ask him or wait again.
He can also name the styles in chat — then use `--from a,b` instead of a request.

## 3. Compare layer by layer, agree with the owner
```bash
node tools/vid.mjs style hybrid show <request-id>        # or: show a,b   (--full = whole text)
```
Show him a short table: each layer → what each parent does → your suggestion and why. Layers: `palette, type, texture, grade, camera, lighting, performance, rhythm, grammar, transitions, motion, sound, prompt`. Rows he already picked on the board are marked "← the owner picked". Ask only about rows that change the look; take his answer. A layer that comes from neither parent = `new` (written by hand later). Colours stay **roles** — the brand fills the hex.

## 4. Draft the new card
```bash
node tools/vid.mjs style hybrid new <new-slug> --request <id> --take palette=a,type=b,motion=b,sound=a [--name "Name"]
```
- Layers not named come from his board picks, else the first parent.
- It writes `video-projects/_library/styles/<new-slug>/style.md` with `parents: [a, b]`, `layers_from:` (frontmatter), a `## Hybrid recipe` table, status **draft**, and the skill `.claude/skills/style-<new-slug>/SKILL.md` (lists the parents' skills per layer). The request is marked done.
- Then: fill Tone, `use_when`, Modes, Do / Don't by hand; make 3–6 of its **own** frames (free routes: `npx hyperframes snapshot`, images-gpt — never reuse the parents' frames); `node tools/vid.mjs style check <new-slug>`; add the skill to the table in `brain/Jobs/Pick a style.md`.
- Approval only by the owner: board `/board/styles/<new-slug>` or `node tools/vid.mjs style approve <new-slug> --words "<his words>"`.
- The owner cancels → `node tools/vid.mjs style hybrid drop <id>`.

## 5. Pick the skills for the video
Open **http://localhost:3000/board/skills?project=<project-slug>** (the project must exist with `director/` — make it with `node tools/vid.mjs new <type> <slug>` first). The owner ticks the skills (the new `style-<new-slug>` skill plus any workflow skills), optionally writes why, presses **Use these skills**. That writes an earlier project (not public). Wait with `node tools/vid.mjs wait <slug>` (reports "skills picked"). `vid check <slug>` lists the pick and warns on unknown names.

## 6. Start director mode
Load the `director` skill and run the project as usual. **Load exactly the skills in `director/skills.md`** (plus `director`) — no other style skill. Apply the new card: `node tools/vid.mjs style apply <new-slug> <project>`; tell the owner at the direction gate that the style is still a draft.
