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

- **The lashes over the iris are reflections, and they belong to the surface, not the iris.**
  This was the bug behind every "glitchy" report. The pale strokes and the bright highlight
  across the iris are the lashes mirrored in the wet front of the eye. They were baked into
  the iris image, so the iris dragged them around with it.

  Three attempts to detect them failed, and it is worth recording why so nobody repeats
  them: testing for *dark* pixels also catches the dark parts of this iris and gouged holes
  in it; testing for *thin dark* structures (a black top-hat) catches the iris's own radial
  fibres, which are equally thin and dark; and simply shortening the iris's travel hid the
  problem rather than fixing it.

  What worked is a property of the eye, not of the pixels: **an iris ring is the same
  brightness all the way round, and a reflection is not.** Converted to polar coordinates
  the iris is near-constant along the angular axis at any given radius, so a localised
  bright anomaly is a reflection by definition. Those are flagged, the gap is filled from
  the unflagged angles at the same radius (which preserves the fibre texture), and the
  reflection is stored separately as *pure added light* - the original minus the cleaned
  iris.

  The browser draws it with the `lighter` blend at a fixed position, over the moving iris.
  Two consequences worth knowing: at rest the composite reproduces the original video frame
  exactly, and the reflection has no cut-out edge, because it is light being added rather
  than a patch being pasted. `eye_ai_refl.webp` is stored **lossless** for that reason -
  compression noise in its black areas would lay a haze over the whole eye.

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
