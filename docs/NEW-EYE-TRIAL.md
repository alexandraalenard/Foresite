# Trial: the second eye clip (branch `new-eye`)

_Created 4 September 2026_

## What this branch is

A trial of the re-shot video (`Human_eye_transforms_into_AI_202609040711.mp4`), which was
commissioned specifically because the first clip barely moved the eye. It is **not** on
`main`. Compare it against the live site, then keep it or throw it away.

## Why it is better

| | first clip | this clip |
|---|---|---|
| pupil sweep used | 93px | **231px** |
| gaze frames | 25 | 17 |
| ending | fibre-optic burst | burst → shattering → **rotating globe → world map** |
| total frames | 81 (3.7 MB) | 73 (2.8 MB) |

## The usable window, and why it is not the whole clip

The eye is on screen from frame 54 to frame 138, and the pupil covers 777-1087px in that
time — a 310px sweep. Only **frames 92-108** are actually usable, giving 231px.

The reason is that the iris changes identity partway through. Measuring the blueness of
the iris ring (blue channel minus red) frame by frame:

- frames 54-108: 48-61 — strongly blue, consistent
- frames 109-114: falls 44 → 21
- frames 130+: goes gold/human

Splicing across that fade would look like the eye changing colour as you moved the mouse,
not like it looking around. So the run stops at 108. **This is the same failure mode as
the first clip** — an AI-generated video re-draws the eye slightly differently at
different moments — so check it on any future clip before trusting the full range.

## Direction

This clip's run starts with the pupil furthest **left** and sweeps right. The first clip
ran the opposite way. The cursor mapping in the script (`target = ...`) has to match, and
getting it backwards is silent — the eye simply looks away from the cursor. Check it.

## Frames

| Files | Count | Source frames |
|---|---|---|
| `eye_human.webp` | 1 | 1 |
| `blink_000` … `blink_027` | 28 | 19-53 every 2nd, then 56-91 every 4th |
| `gaze_000` … `gaze_016` | 17 | 92-108, every frame |
| `expl_000` … `expl_026` | 27 | 139-240, every 4th |

Cache tag is `?v=5`.

## One thing to decide

The clip ends on a world map with a **"My Business"** label burnt into the footage. It
reads as a placeholder. It cannot be edited out — it is part of the video — so either it
stays, or that section of the clip is cut short, or the clip gets re-generated without it.

## Testing done

Desktop 1500x900 and 1920x1080, phone 390x844 and 360x800, tablet 768, and with
reduce-motion on. No console errors, no failed requests, no horizontal overflow at any
width, and a flat 60fps while the eye tracks.
