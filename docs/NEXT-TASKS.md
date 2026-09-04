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

## 1b. Launch steps that only you can do (about 30 minutes, all free)

These are setup jobs on other people's websites, so they can't be done in the code.

**Google Search Console** - search.google.com/search-console. Add the site, verify it,
submit `sitemap.xml`. This is how Google finds the pages.

**Bing Webmaster Tools** - bing.com/webmasters. Add the site (there's an "import from
Google Search Console" button that does it in two clicks), submit the sitemap, turn on
IndexNow. Do not skip this one: Bing's index feeds Microsoft Copilot AND ChatGPT's web
results, so it is the single cheapest thing on this list.

**Google Business Profile** - business.google.com. Even without a shopfront, set it up
with service-area suburbs. This is the fastest route to actually being found locally,
and it also feeds what the AI assistants say about you.

**Web3Forms auto-reply** - the auto-responder that emails the enquirer straight back is
a paid Web3Forms feature. Until you have it, the reply promise on the site is yours to
keep manually. It is worth keeping: the research says 78% of customers buy from whoever
replies first.

**When you buy a real domain**, search `index.html` for `foresite-git-main-bears3` and
change every one of those to the new address - there are canonical, Open Graph and
structured-data references. Same in `robots.txt` and `sitemap.xml`. Leaving them stale
tells Google the real site is a copy of the old one.

## 1c. A decision only you can make: the price

The research says your $750 build sits below the Australian market floor. Other
freelancers charge $1,500-$2,500 for a basic site; at 15-25 hours of real work, $750
works out at $30-$50 an hour before tax. And the 200-client survey found price was NOT
the deciding factor - vision, trust and value all ranked above it.

Three options:

1. **Leave it.** Being the low-risk option is a legitimate way to win the first five
   clients. Just price it knowingly, as the cost of acquiring a care-plan client.
2. **Raise the build to $1,200 / $2,200.** Puts you inside the market rather than below
   it, and stops the price itself reading as a warning sign.
3. **Keep $750 but require a 12-month care plan.** The care plans are where the money
   actually is: $150/month at about two hours' work is $75/hour, recurring, and twenty
   clients is $3,000/month.

Tell me which and I'll change the site.

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
