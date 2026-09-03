# Foresite — AI Handover

_Last updated: 3 September 2026_

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
| 1. Human | page loads | a still, human eye (video 0:00) |
| 2. Cybernetic | first mouse move (or tap) | the eye blinks once and reopens as an AI eye; from then on **the iris follows the cursor** (video 1:00 → 3:00) |
| 3. Explosion | scrolling the hero | cuts to the fibre-optic burst, scrubbed by scroll position, finishing at 75% so the headline lands before the burst ends (video ~7:50 → 10:00) |

### Framing

The whole video frame is shown, fitted inside the hero rather than cropped to fill it. On
a screen much taller than 16:9 — a phone held upright — fitting it whole would leave a
thin letterboxed strip, so it grows until it fills a reasonable share of the panel,
cropping forehead and cheek but never the eye. See `SAFE_W`/`SAFE_H` in the script.

### How the eye follows your cursor

It is real footage. The eye genuinely looks around in the source video: across frames
96-120 the pupil travels 93px while the iris, the glowing ring and the lashes all stay
consistent. Cursor position scrubs that run - cursor on the right of the screen shows the
start of it, where the pupil sits furthest right; cursor on the left shows the end.

Nothing is composited, retouched or reconstructed. That matters, because an earlier
version *was*: it cut the iris out of a single frame, rebuilt the white of the eye behind
it and slid the iris around. Every visual defect this project hit came from that, and the
fix was to stop doing it and use the footage that was in the video all along.

**The video only moves the eye sideways.** Vertical cursor movement gets a small parallax
of the whole image instead of a moving iris. Faking vertical movement would mean going
back to cutting the iris out, so don't.

If a wider sweep is ever wanted, the answer is a new source clip with a bigger eye
movement in it - not retouching this one.

### The frame files

| Files | Count | What |
|---|---|---|
| `blink_000` … `blink_027` | 28 | the blink and transformation |
| `gaze_000` … `gaze_024` | 25 | the eye looking around (video frames 96-120) |
| `expl_000` … `expl_026` | 27 | the explosion |

About 3.7 MB in total. Only `eye_human.webp` is needed for the first paint; the rest loads
in the background, explosion frames last, and each one is decoded once off screen at load
so that scrubbing never stutters.

**Frame files are requested with a `?v=` tag** (`V` in the script). The filenames stay the
same between versions, so without it browsers and Vercel's CDN serve old images against
new code. Bump it whenever the frames change.

---|---|
| `eye_ai_iris.webp` | the iris on its own, as a disc with a transparent edge |
| `eye_ai_mask.webp` | the shape of the eye opening, as a transparency mask |

The iris is drawn into a small offscreen canvas, masked to the eye opening, and only then
painted onto the page. That mask is what makes the iris slide *behind* the eyelid instead
of over the top of the lashes. The iris may travel 66px horizontally and 42px vertically
in the frames' own 1440×810 coordinate space; those are `GAZE_X` and `GAZE_Y` in the
script.

Three things had to be right for this to look real, and each took a couple of attempts:

- **The sclera behind the iris** is rebuilt by Laplace diffusion — the surrounding white
  of the eye is allowed to flow inward until it fills the gap. Earlier attempts used a
  flat colour, which showed up as a pale disc, and a radial smear, which left a grey arc.
- **The lashes were removed from the iris disc itself**, by copying from the mirror-image
  point across the pupil. Otherwise a ghost set of lashes travelled around with the iris.
- **The eye opening was traced by hand** off frame 186. Every automatic detector either
  leaked into the eyelid or cut the sclera in half; the lid margins are easy to read off
  the picture and a hand-traced curve is smooth by construction. The control points are
  in `rig.py` terms `UX`/`UY`/`LY`.

If you ever regenerate these three layers from a different video frame, the disc's
position and radius are baked into the `IRIS` and `LID` constants in the script — they
must be regenerated together.

### The frame files

| Files | Count | What |
|---|---|---|
| `eye_human.webp` | 1 | stage 1, the still human eye |
| `blink_000` … `blink_028` | 29 | the blink and transformation |
| `expl_000` … `expl_026` | 27 | stage 3, the explosion |

Total about 2.4 MB. Only `eye_human.webp` is needed for the first paint; everything else
loads in the background, explosion frames last.

The older `frame_000.webp` … `frame_047.webp` are from a previous version and are no
longer referenced. They can be deleted.

---

## The deploy pipeline

```
Edit files  ->  commit to GitHub main  ->  Vercel auto-deploys  ->  live
```

Three ways to get files into the repo:

1. **GitHub website** — https://github.com/alexandraalenard/Foresite/upload/main, drag
   files in, click "Commit changes".
2. **VS Code** — the repo is cloned locally. Copy files in, then Source Control panel →
   message → Commit → Sync.
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

---

## Owner's working preferences

- Plain English only. No jargon. Explain every click.
- If something can't be done, say so IMMEDIATELY — don't burn time on workarounds.
- Never pretend something is done when it isn't. Never guess.
- Report errors as: Problem / Cause / Possible Fix / Recommended Fix / Est. Time / Confidence %.
- Build whole features, not fragments.
