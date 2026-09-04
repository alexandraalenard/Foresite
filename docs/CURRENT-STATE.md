# Foresite — Current State

_Last updated: 4 September 2026_

## ✅ Done

- Full marketing website designed and built (single `index.html`).
- All copy written and reviewed: problem section, "how we got here" timeline, what's
  included, 4-step process, pricing, care plans, founding-clients note, contact form,
  footer with legal disclaimer.
- Pricing set: Basic website $750 flat, Premium website $1,500 flat, dashboards "get a
  quote". Care plans: Basic $100/mo, Premium $250/mo.
- Site is LIVE on Vercel: https://foresite-git-main-bears3.vercel.app
- GitHub → Vercel auto-deploy pipeline working.
- Git installed on owner's PC; repo cloned; VS Code connected.
- **Hero eye, all three stages, built and tested.** Human eye on landing → blink and
  transform to a cybernetic eye on first cursor movement → iris follows the cursor →
  explosion scrubbed by scroll. Works on desktop, on phones (tap instead of cursor,
  with the iris drifting gently on its own), and under "reduce motion" accessibility
  settings.
- **Hero rebuilt from the second eye clip (4 Sept).** Bolder AI iris, and sharp at every
  cursor position instead of only when looking left. Seven gaze positions, all taken from
  frames where the eye was at rest; every frame registered so the face stays locked and
  only the iris moves. The explosion is still cut in from the first clip, the only one
  that has one. 60 files, 2.9 MB, cache tag `?v=10`.
- Light palette across the whole site, interactive consumer-behaviour timeline, and the
  glass panel behind the hero paragraph: all in and tested.
- Tested in a real browser at 1920×1080, 1500×900, 768×1024, 390×844 and 360×800: no
  console errors, no failed requests, no sideways scroll, 60fps while the cursor sweeps,
  and text contrast passing WCAG AA against all five hero backgrounds (worst 6.83:1).

## 🔄 Waiting on the owner

- **The new eye is on a branch called `new-eye-2`, not on the live site.** Commit and
  sync it in VS Code, look at the Vercel preview, and say yes or no before it goes to
  `main`. See NEXT-TASKS.md, task 1.

## ⏳ Not started (human-only — no coding needed)

- Fill in placeholders in `index.html`:
  - `[YOUR NAME]` and `[YOUR TOWN/REGION]` (contact section)
  - `PLACEHOLDER@gmail.com` (contact email, appears twice)
  - `WEB3FORMS_ACCESS_KEY_PLACEHOLDER` (contact form — free key at web3forms.com)
  - `PLACEHOLDER-ADD-YOUR-ABN` (footer)
- Register the business name "Foresite" with ASIC (~$44 for 3 years) before trading.
- Check "Foresite" on the IP Australia trademark register.
- Buy a domain (e.g. foresite.com.au — needs an ABN, ~$20–25/yr).
- Decide hosting for the real launch: **Vercel's free plan is non-commercial.** Either
  Vercel Pro (~$20/mo USD) or a free-for-commercial host like Cloudflare Pages.
- (Optional) Stripe payment links for the two care plans.

## Known quirks

- The repo still contains the old, unused `frame_000.webp` … `frame_047.webp` and a stray
  `index.html2`. Harmless, but about 1.8 MB of dead weight — delete when convenient.
- Vercel preview URLs sometimes show a login redirect when fetched by a tool. That's
  Vercel's protection, not a broken file. View while logged in.
