# Trial: the second eye clip (branch `new-eye`)

_Created 4 September 2026_

## What this branch is

A trial of the re-shot video (`Human_eye_transforms_into_AI_202609040711.mp4`), which was
commissioned specifically because the first clip barely moved the eye. It is **not** on
`main`. Compare it against the live site, then keep it or throw it away.

## Why it is better

| | first clip | this clip |
|---|---|---|
| pupil sweep used | 93px | **303px** |
| gaze frames | 25 | 19 |
| ending | fibre-optic burst | burst → shattering → **rotating globe → world map** |
| total frames | 81 (3.7 MB) | 73 (2.8 MB) |

## The usable window, and why it is not the whole clip

The eye is on screen from frame 54 to frame 138, and the pupil covers 777-1087px in that
time — a 310px sweep. Only **frames 92-110** are actually usable, giving 303px.

The reason is that the iris changes identity partway through. Measuring the blueness of
the iris ring (blue channel minus red) frame by frame:

- frames 54-108: 48-61 — strongly blue, consistent
- frames 109-114: falls 44 → 21, and a warm ring appears around the pupil
- frames 130+: goes gold/human

The run was first cut at 108, where the colour is perfectly consistent. That turned out to
be wrong for a different reason: measured against the centre of the eye opening (x=950),
it put the pupil **172px left of centre but only 58px right**, so the eye had almost no
right-hand travel and the tracking felt dead on that side. Extending to frame 110 balances
it at -172/+130 and costs only a faint warm tint at the extreme right, reached only when
the cursor is at the very edge of the screen.

Colour-grading frames 111-114 back to match was tried and abandoned: the drift is not a
global colour shift but a structural one - a gold ring genuinely appears around the pupil -
so a per-channel gain brightens the frame without removing it.

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
| `gaze_000` … `gaze_018` | 19 | 92-110, every frame |
| `expl_000` … `expl_026` | 27 | 139-240, every 4th |

Cache tag is `?v=5`.

## Smoothness

19 frames across a 303px sweep is a 16px step, which reads as a stutter when the eye is
this large on screen, so the two neighbouring frames are **cross-faded** by the fractional
part of the position. Blending them straight onto the screen meant two full-size scaled
draws per frame and dropped to ~30fps on a large display; they are now mixed in an
offscreen canvas at the frames' own resolution and scaled once. Measured flat 60fps at
1920x1080 afterwards, with no dropped frames.

## Weight of the overlays

The gradients that sit over the hero exist to keep the text readable. On the dark site
they darkened the image; inverted for the light site they were washing the eye out. They
are now at about 45% of their original strength, which was verified rather than guessed:
sampling the rendered page behind each piece of text gives 11.8:1 for the headline (3:1
required), 14.3:1 for the body copy and 16.5:1 for the small mono labels (4.5:1 required).
There is room to go lighter still if the eye should be more solid again.

## One thing to decide

The clip ends on a world map with a **"My Business"** label burnt into the footage. It
reads as a placeholder. It cannot be edited out — it is part of the video — so either it
stays, or that section of the clip is cut short, or the clip gets re-generated without it.

## Testing done

Desktop 1500x900 and 1920x1080, phone 390x844 and 360x800, tablet 768, and with
reduce-motion on. No console errors, no failed requests, no horizontal overflow at any
width, and a flat 60fps while the eye tracks.
