# Foresite — Current State

_Last updated: 3 September 2026_

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
- Tested in a real browser at 1440×900, 1280×800 and 390×844: no console errors, no
  failed requests, no broken layout.

## 🔄 Waiting on the owner

- **The new `index.html` and `frames/` are sitting in the `foresite-explode` folder on
  the PC but have NOT been pushed to GitHub.** Nothing is live until they are.
  See NEXT-TASKS.md, task 1.

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
