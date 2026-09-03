# Foresite — Key Decisions (and why)

_Last updated: 3 September 2026_

- **Plain HTML, one file + frames folder — no framework.** Simple, fast, cheap to host,
  and understandable by a non-technical owner. No build step to break.

- **GitHub → Vercel auto-deploy.** Set up by IMPORTING the repo into Vercel (not a bare
  or CLI-created project) — the import is what wires up the auto-deploy hook. A project
  created another way did NOT auto-deploy; re-importing fixed it.

- **Frames as separate files, not embedded in the HTML.** Embedding them as base64 made a
  ~5.5 MB `index.html` that some viewers rendered as a black screen. Separate files keep
  each one small, let the browser cache them, and let the page paint before the heavy
  ones arrive.

- **Video frames rather than a still photo.** A photo can lean and zoom but cannot blink
  or explode. The supplied video (1920×1080, 240 frames, 24fps) contains all three
  moments: human eye to ~frame 31, blink and transformation 31–70, settled AI eye to
  ~186, explosion 188–240.

- **The iris tracks the cursor by compositing, not by moving the whole picture.**
  The obvious approach — nudging the entire eye image toward the cursor — reads as the
  whole face sliding around, not as an eye looking at you. Instead the iris was cut out
  as its own layer, the sclera behind it reconstructed, and the eyelid painted back over
  the top. The iris now slides across the white of the eye and disappears behind the lid.
  Costs three image files instead of one; worth it, since this is the thing visitors
  actually look at.

- **The iris travels a modest distance, on purpose.** The lashes that cross the open part
  of the eye are baked into the iris image, so a wide sweep drags them along with it and
  reads as a glitch. Two attempts to cut them out of the iris and re-draw them separately
  both made it worse — a "dark = lash" test also catches the dark parts of this iris, and
  a thinness test left speckles. Halving the travel instead (`GAZE_X`/`GAZE_Y` in the
  script) keeps the movement clearly legible while the lashes stay convincingly attached.
  If it ever needs to sweep further, the honest fix is a second source frame with the eye
  actually looking sideways — not more retouching.

- **Following the cursor repaints only the eye, not the whole hero.** Redrawing a
  full-screen image on every animation frame stuttered on large displays. The tracking now
  clips to the eye-opening rectangle, and the canvas backing store is capped at 1.5x
  device pixels.

- **Frame files are requested with a `?v=` tag.** The filenames stay the same between
  versions, so without it browsers and Vercel's CDN serve old images against new code —
  which is exactly what happened once, and looked like the fix had failed. `vercel.json`
  pairs this with must-revalidate on the HTML and long-lived caching on the images. **Bump
  the number in the script whenever the frame files change.**

- **The blink is the transformation.** Human eye closes, circuitry traces across the lid,
  eye reopens cybernetic. Tying the change to the blink means there is no cross-fade or
  cut to explain — it reads as one event.

- **The explosion finishes at 75% of the scroll**, not 100%, so the "Ready to be found?"
  headline arrives while the burst is still on screen rather than after it.

- **Framing is anchored on the iris, not the picture.** A fixed crop that looks right on
  a widescreen monitor pushes the iris almost off a tall phone screen. The canvas now
  positions the iris at 45% of the width on every screen shape.

- **The hero keeps scroll travel on phones.** It previously collapsed to one screen tall
  below 900px wide, which left no room for the explosion to play. Now 220vh.

- **Pricing.** Flat fees ($750 / $1,500) for honesty and simplicity vs hourly. Care plans
  ($100 / $250) are the real recurring value; hosting costs about nothing to deliver.

- **Honesty positioning.** No "GEO" buzzword in customer copy. Never promise a business
  WILL appear in AI answers — that is a misleading-conduct risk under Australian Consumer
  Law. Sell the setup work only. The footer carries a disclaimer to that effect.

- **Founding-clients section** instead of fake testimonials — honest about being new, and
  turns it into a fair-deal hook.
