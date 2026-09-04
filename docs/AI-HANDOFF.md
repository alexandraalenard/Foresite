# Foresite — AI Handover

_Last updated: 4 September 2026_

Read this first if you are an AI assistant or a developer picking this up.

---

## What this project is

**Foresite** is a solo web-design business for Australian small businesses. The offer:
rebuild a client's outdated website AND set it up so it's easy to find — by Google, by
Google Maps, and by AI tools like ChatGPT and Google's AI answers.

This repo is the **Foresite marketing website** itself (the site that sells the service).

- **Owner:** Alexandra (GitHub: `alexandraalenard`) — NON-TECHNICAL. Explain every step in
  plain English. Never assume knowledge of git, terminal, VS Code, Vercel, or code.
- **Live site:** https://foresite-git-main-bears3.vercel.app
- **GitHub repo:** https://github.com/alexandraalenard/Foresite
- **Hosting:** Vercel (free "Hobby" plan) — auto-deploys from the `main` branch.

---

## How the site is built

- One `index.html` file plus a `frames/` folder of images. No framework, no build step,
  no database. Plain HTML, CSS and JavaScript.
- Push to `main` on GitHub → Vercel republishes within about a minute.

---

## The hero eye (the centrepiece)

Three stages, driven by what the visitor does:

| Stage | Trigger | What happens |
|---|---|---|
| 1. Human | page loads | a still, human eye |
| 2. Cybernetic | first mouse move (or tap) | the eye blinks once and reopens as an AI eye; from then on **the iris follows the cursor** |
| 3. Explosion | scrolling the hero | cuts to the fibre-optic burst, scrubbed by scroll position, finishing at 75% so the headline lands before the burst ends |

### Framing

The whole video frame is shown, fitted inside the hero rather than cropped to fill it. On
a screen much taller than 16:9 — a phone held upright — fitting it whole would leave a
thin letterboxed strip, so it grows until it fills a reasonable share of the panel,
cropping forehead and cheek but never the eye. See `SAFE_W`/`SAFE_H` in the script.

### How the eye follows your cursor

**Whole, untouched video frames are swapped as the cursor moves. Nothing is composited,
retouched, masked or shifted at runtime.** This is the single most important thing to
know, because four other approaches were tried first and every visual defect this project
hit came from one of them. They are written up in `DECISIONS.md`; do not repeat them.

Cursor position maps onto **where the pupil actually sits** in each frame (`GAZE_POS` in
the script, measured off the video), not onto the frame number. The eye does not move at
an even rate through the clip, so mapping to frame number put the eye hard left when the
cursor was dead centre.

**The video only moves the eye sideways.** Vertical cursor movement does nothing. Faking
vertical movement would mean cutting the iris out, so don't. If a wider sweep is ever
wanted, the answer is a new source clip with a bigger, *slower* eye movement in it — not
retouching this one.

### Where the frames come from (two clips)

There are two source clips, and the hero uses both:

- **Clip 2** (`Eye_transforms_into_cybernetic_eye_202609041155.mp4`, 4 Sept) — the human
  eye, the blink, and all seven gaze positions. Bolder AI iris, and sharp almost
  throughout. **It has no explosion.**
- **Clip 1** (`Human_eye_transforms_into_AI_202609040711.mp4`, 3 Sept) — the explosion
  only. It is the only clip that has one.

The two were generated from the same base image and overlay almost exactly, so the burst
is cut in from clip 1 at the frame where the sparks have already swallowed the iris, and
faded over four scroll indices. The join lands on white particles rather than on a
visibly different eye.

### Two rules the frame builder follows

The builder is `build3.py` (kept with the working files, not in the repo).

1. **Only frames where the eye was AT REST are used.** Frames caught mid-flick are motion
   blurred in the source footage. Sharpness is measured as the variance of the Laplacian
   in a ring around the pupil: mid-flick frames score under 200, resting frames score
   1000–2200. Using consecutive frames meant using blurred ones, which is why the iris
   once looked soft everywhere except hard left.
2. **Every frame is registered to a common reference before export.** The camera in clip
   2 drifts about 70px sideways across its ten seconds. Because the gaze frames come from
   moments far apart in the clip, using them raw would slide the whole face as the cursor
   moved. Each frame is translated back onto frame 86 (phase correlation on a patch of
   cheek) and all frames are cropped to the same rectangle, so only the iris moves.

Frames are also chosen to keep the **eyelid opening** as consistent as the footage allows
— a big step in lid opening between neighbouring frames reads as the eye blinking open as
the cursor moves.

### The frame files

| Files | Count | What |
|---|---|---|
| `eye_human.webp` | 1 | stage 1, the still human eye |
| `blink_000` … `blink_025` | 26 | the blink and transformation |
| `gaze_000` … `gaze_006` | 7 | the eye looking around, left to right |
| `expl_000` … `expl_025` | 26 | the explosion |

60 files, about 2.9 MB. Only `eye_human.webp` is needed for the first paint; the rest
loads in the background, explosion frames last, and each one is decoded once off screen
at load so that scrubbing never stutters.

**Frame files are requested with a `?v=` tag** (`V` in the script). The filenames stay the
same between versions, so without it browsers and Vercel's CDN serve old images against
new code — which has happened, and looked like the fix had failed. **Bump it whenever the
frames change.** Currently `?v=10`.

The counts in the script (`BLINK_N`, `GAZE_N`, `EXPL_N`) and the length of `GAZE_POS`
must match the files on disk. If they don't, the eye pins to one position and stops
following the cursor. Check them after any rebuild.

---

## The deploy pipeline

```
Edit files  ->  commit to GitHub main  ->  Vercel auto-deploys  ->  live
```

Three ways to get files into the repo:

1. **GitHub website** — https://github.com/alexandraalenard/Foresite/upload/main, drag
   files in, click "Commit changes".
2. **VS Code** — the repo is cloned at `Desktop\Foresite`. Copy files in, then Source
   Control panel → message → Commit → Sync.
3. **Git Bash** — `cd` into the repo, `git add .`, `git commit -m "..."`, `git push`.
   NOTE: pasting into Git Bash inserts junk characters (`^[[200~`) and fails. Type
   commands, don't paste.

### What an AI assistant can and cannot do

Depends entirely on the tools it has:

- A **plain chat window** cannot touch the owner's computer at all. It can only prepare
  files for her to upload by hand.
- A session with **Cowork device access** (a connected folder on her PC) *can* read and
  write files in that folder directly, which is how this version was delivered.
- Neither can `git push` on her behalf: the credentials live in Windows, and the sandbox
  that runs commands is a separate Linux VM that can't see them. **Pushing is always the
  owner's step.** Say so up front rather than attempting workarounds.

### A trap: the connected folder cannot delete files

The Cowork bridge mounts the folder read/write but **without permission to unlink**. Two
consequences:

- `git add` leaves a `.git/index.lock` behind that it cannot remove, and VS Code then
  fails with *"Unable to create '.git/index.lock': File exists."* Move the lock out of the
  way after any git command that writes.
- `tar -xzf` fails with "File exists". Use `tar --overwrite -xzf`, which writes in place.
- Shell redirection (`>`) works fine, because it truncates rather than unlinks.

---

## Owner's working preferences

- Plain English only. No jargon. Explain every click.
- If something can't be done, say so IMMEDIATELY — don't burn time on workarounds.
- Never pretend something is done when it isn't. Never guess.
- Report errors as: Problem / Cause / Possible Fix / Recommended Fix / Est. Time / Confidence %.
- Build whole features, not fragments.
