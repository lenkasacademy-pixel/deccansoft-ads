# Deccansoft · Meta ads dashboard

Live: https://lenkasacademy-pixel.github.io/deccansoft-ads/

Reporting starts **22 Sep 2026**; earlier data is deliberately left out.

One self-contained page (`index.html`) for the Deccansoft Home ad account
(`1864644430272738`) and its pixel (`666052152973589`). Every figure lives in the
`DATA` block at the top of `index.html`; the rest of the page is computed from it.

## Daily update

Easiest: ask Claude **"refresh the Deccansoft dashboard"**. By hand:

1. **`updated`**: the time you refreshed. **`throughDay`**: today's date (YYYY-MM-DD).
2. **`ads`**: one row per ad, **lifetime** totals from Ads Manager
   (Ads tab, date range "Maximum"):
   `spend` (amount spent, ex-GST), `impr` (impressions), `reach`,
   `clicks` (link clicks), `lpv` (website landing page views),
   `leads` (leads), `regs` (registrations completed), `status`.
   A new ad needs a new row; `group` is `quiz` or `webinar`.
3. **`daily`**: one row per day for all ads together:
   `["YYYY-MM-DD", spend, impressions, linkClicks, leads, registrations]`.
   **Re-enter the last 2–3 days each time**, not only today: Meta keeps adjusting
   recent days for about 48 hours.
4. **`pixel`**: website events per day from Events Manager → dataset
   `666052152973589` → Overview, **browser events only** (every event also arrives
   from the server; counting both doubles it). Days are IST.
5. **`notes`**: the alerts at the top. `level` is `critical`, `serious`, `warning` or `good`.

Commit and push to `main`. Pages redeploys in about a minute.

## What the numbers mean

- **Spend is ex-GST**, matching Ads Manager. Meta bills 18% GST on top.
- **Leads / registrations** are the ones Meta credits to an ad (7-day click, 1-day view).
- **Quiz events are website-wide**: every visitor (ads, organic, test traffic).
  Meta can't split them per ad, and `QuizStart` / `QuizAnswer` / `QuizComplete`
  fire on both the quiz page and the webinar page's own quiz.
- **`Lead` includes the KickStarter checkout**, which fires Lead + Purchase on
  the same pixel. Use `CompleteRegistration` for the webinar.
