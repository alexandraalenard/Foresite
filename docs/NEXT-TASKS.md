# Foresite — Next Tasks (in order)

_Last updated: 3 September 2026_

## 1. Push the new eye live  ← YOU ARE HERE

A ready-to-commit clone of the repo sits at `Desktop\Foresite`, with every change already
staged: the new `index.html`, the 61 new frame files, these docs, and the removal of the
48 old unused frames plus the stray `index copy.html` and `index.html2`.

In VS Code: **File → Open Folder → `Desktop\Foresite`** → Source Control icon → type a
message → **Commit** → **Sync**.

There is an older Foresite clone elsewhere on this machine (the one VS Code had open
before). Once this push has gone through, delete it or run Pull on it, so there is only
ever one working copy.

Wait about a minute for Vercel, then test on the live link:

- [ ] Land on the page without touching the mouse — a human eye.
- [ ] Move the mouse — it blinks once and reopens as a blue cybernetic eye.
- [ ] Move the cursor around — the iris follows it.
- [ ] Scroll — it cuts to the explosion, and "Ready to be found?" arrives before the
      burst finishes.
- [ ] Same on a phone: tap, then scroll.

## 2. Fill in the placeholders

In `index.html`, replace: `[YOUR NAME]`, `[YOUR TOWN/REGION]`, `PLACEHOLDER@gmail.com`
(twice), `WEB3FORMS_ACCESS_KEY_PLACEHOLDER`, `PLACEHOLDER-ADD-YOUR-ABN`. Push the same way.

## 3. Make the contact form actually send

Sign up free at web3forms.com, get an "access key", paste it over
`WEB3FORMS_ACCESS_KEY_PLACEHOLDER`. Test by submitting the form to yourself.

## 4. Business setup (no coding)

- Register "Foresite" as a business name with ASIC (~$44 for 3 years).
- Check the name on the IP Australia trademark register.
- Buy a domain (foresite.com.au needs an ABN).

## 5. Sort real hosting before taking customers

Vercel's free plan is non-commercial. Move to Vercel Pro (~$20/mo USD) or Cloudflare
Pages (free, commercial use allowed) before this is your live business front.

## 6. Tidy up (optional)

Delete the unused `frame_000.webp` … `frame_047.webp` and `index.html2` from the repo —
about 1.8 MB of dead weight.

## 7. (Later) Stripe care-plan links

Two recurring payment links ($100/mo, $250/mo AUD); swap them into the "Enquire about
Basic/Premium" buttons when ready to accept payment.
