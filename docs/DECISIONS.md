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

- **The site is light, not dark.** The video's own edges are pale - warm skin on the left,
  light grey on the right, averaging about `#BEB1AE`. Against black the frame always ended
  on a visible edge, however it was feathered. Against a warm off-white it dissolves. The
  page background is `#F4EFEA`, and the hero frame is inset slightly (`FIT` in the script)
  with its edges faded out (`FEATHER`), so the footage melts into the page rather than
  sitting on top of it.

  The colour tokens were **renamed, not just re-valued**: `--ink` now means the page
  background and `--paper` the text, which would have read backwards on a light site.
  They are `--bg`, `--bg-raised`, `--text`, `--text-2`, `--text-3`, plus `--line`,
  `--line-soft`, `--signal`, `--signal-dim`, `--shut` and `--good`.

  Every foreground/background pair was checked against WCAG AA and adjusted until it
  passed: body text 16.4:1, secondary 7.7:1, small mono labels 5.1:1, the gold accent
  5.3:1 (it had to darken from `#E9B15C` to `#8F5409` to clear 4.5:1 on a light ground),
  button borders 3.3:1. Rules and hairlines sit below that deliberately - they are
  decoration, not information.

- **Media queries live at the END of the stylesheet, and must stay there.** The stylesheet
  declares its layout rules twice: a base pass and a components pass. The responsive
  blocks were sitting between the two, so the components pass silently overrode every one
  of them. **The mobile layout had never actually applied** - phones were being served the
  desktop two-column grid, and the whole page could be swiped sideways to about 1024px on
  a 390px screen. Moving the media queries below the components pass fixed it, along with
  two genuine layout faults it had been masking: grid items default to `min-width: auto`,
  so the pricing tiers forced their column wider than the screen, and the contact section
  never collapsed to one column. Verified at 360, 390, 768 and 1500px: no horizontal
  overflow at any of them.

- **Pricing.** Flat fees ($750 / $1,500) for honesty and simplicity vs hourly. Care plans
  ($100 / $250) are the real recurring value; hosting costs about nothing to deliver.

- **The hero leads on the AI shift, not on the service.** The old opening line described
  what Foresite does; it created no urgency. It now reads as one sentence - *"We're on the
  cusp of the AI revolution. Is your business invisible to AI?"* - with the owner's
  existing bold headline kept exactly as it was and the new framing wrapped around it.

  "Future-proof" was deliberately **not** used, though it was the owner's first instinct.
  It is an absolute promise about an unknowable future and sits badly next to the
  misleading-conduct rule below. The supporting copy says what the work *is* - modern,
  fast, structured so AI tools can read and understand the business - and stops short of
  promising what it will *achieve*.

  The supporting paragraph is built on one contrast: *"Google offered your customers ten
  options. AI offers them one."* "Names" is used rather than "recommends" because it is
  colder and closer to what actually happens. The closing line - *"The time to move your
  business into the AI revolution is now"* - deliberately echoes the headline's opening, so
  the paragraph lands back where it started.

  **One phrase was corrected against the owner's draft.** She wrote *"most small business
  websites can't be read at all."* That is not true - AI can read almost any website; what it
  cannot do is make sense of most of them. It now reads *"most small business websites were
  never built to be read by AI agents,"* which completes the "read" thread and is accurate -
  the claim is about what those sites were designed for, not about what is technically
  possible. Overstating is
  precisely what undercuts an honest-broker positioning, and it is the kind of claim a
  prospect can disprove in thirty seconds. Hold this line if the copy is revisited.

  Note on capitalisation: "AI revolution" is lower-case in both the opening line and the
  closing one. Keep them matching.

  Note for whoever edits this next: the hero has no dimming overlay behind it any more, so
  every line of hero text carries its own light halo instead. The lead-in was the one piece
  that did not, and it washed out over the bright part of the eye. If the copy changes
  again, re-check the contrast rather than assuming.

- **Honesty positioning.** No "GEO" buzzword in customer copy. Never promise a business
  WILL appear in AI answers — that is a misleading-conduct risk under Australian Consumer
  Law. Sell the setup work only. The footer carries a disclaimer to that effect.

- **Founding-clients section** instead of fake testimonials — honest about being new, and
  turns it into a fair-deal hook.
