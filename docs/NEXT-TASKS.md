# Foresite — Next Tasks (in order)

_Last updated: 4 September 2026_

## 1. Look at the new eye  ← YOU ARE HERE

The second eye clip has been built into the hero on a branch called **`new-eye-2`**.
**Nothing on the live site has changed.** Everything is already staged in
`Desktop\Foresite`.

In VS Code:

1. Click the **Source Control** icon on the left (the branching arrows).
2. Type a short message, e.g. `New eye clip`.
3. Click **Commit**, then **Sync Changes**.

Then go to vercel.com → the Foresite project → click the newest **Preview** deployment.
It will be labelled `new-eye-2`, not `main`.

Check:

- [ ] Land on the page without touching the mouse — a human eye.
- [ ] Move the mouse — it blinks once and reopens as a blue cybernetic eye.
- [ ] Move the cursor left and right — the iris follows, and stays sharp everywhere.
- [ ] Scroll — it cuts to the explosion, and "Ready to be found?" arrives before the
      burst finishes.
- [ ] Same on a phone: tap, then scroll.

Tell me yes or no. If yes, I'll merge it into `main` and it goes live.

## 2. Fill in the placeholders

In `index.html`, replace: `[YOUR NAME]`, `[YOUR TOWN/REGION]`, `PLACEHOLDER@gmail.com`
(twice), `WEB3FORMS_ACCESS_KEY_PLACEHOLDER`, `PLACEHOLDER-ADD-YOUR-ABN`. Push the same way.

## 3. Make the contact form actually send

Sign up free at web3forms.com, get an "access key", paste it over
`WEB3FORMS_ACCESS_KEY_PLACEHOLDER`. Test by submitting the form to yourself.

## 4. Business setup (no coding)

- Register "Foresite" as a business name with ASIC (~$44 for 3 years).
- Check the name on the IP Australia trademark register.
- Buy a domain (foresite.com.au needs an ABN, ~$20–25/yr).

## 5. Sort real hosting before taking customers

Vercel's free plan is non-commercial. Move to Vercel Pro (~$20/mo USD) or Cloudflare
Pages (free, commercial use allowed) before this is your live business front.

## 6. Tidy up (optional)

- `frames/gaze_007.webp`, `frames/gaze_008.webp` and `frames/expl_026.webp` are left over
  from the previous build and are no longer used. About 150 KB.
- Delete the `_claude-junk-delete-me` folder on your Desktop.
- Delete the old `new-eye` branch once you're happy with `new-eye-2`.
- `Downloads\foresite-new-eye.tar.gz` was just the transfer bundle — safe to delete.

## 7. (Later) Stripe care-plan links

Two recurring payment links ($100/mo, $250/mo AUD); swap them into the "Enquire about
Basic/Premium" buttons when ready to accept payment.
