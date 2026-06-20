# Danielle's Car Decision

An interactive, single-page decision aid for weighing a **used Tesla** against a **comparable used gas car** — built to help Danielle and Sergei think through a real purchase after Danielle's old car was totaled.

**Live site:** https://cpoland88.github.io/Danielles-Car-Decision/

---

## What it does

The page lets you build a car-buying scenario with live sliders and toggles, then shows the **true total cost of ownership** of three options side by side — not just the sticker price or the monthly payment. The core message: the cheapest car to *buy* is rarely the cheapest car to *own*, and whether an EV wins depends on price, mileage, and how long you keep it.

It's a teaching tool, not a quote. Every number is a reasonable estimate meant to frame the decision, and the site says so.

## The scenario it's built around

- Danielle's old car was totaled; she's receiving a **$9,200 insurance payout** (modeled as cash-in-hand / down payment, not a car price).
- They have access to a **4.50% APR credit-union loan** (better than typical dealer financing).
- **Sergei is the driver** — ~70 miles/day, 5 days/week ≈ **18,200 mi/year**. This is the daily driver; the second family vehicle is a truck with 200k miles.
- They live near **Indian Head, MD (20640)**, which drives the local pricing defaults and the Maryland EV incentives.

## The three options compared

1. **$9,200 cash car** — the trap: spend the whole insurance check on an older, higher-mileage car. Cheapest to buy, most expensive to own (repairs + near-zero resale).
2. **Used gas sedan** — the sensible benchmark (Camry/Accord vintage, financed at the CU rate).
3. **Used Tesla** — the question being asked.

## Page sections

1. **Build the deal** — sliders (prices, down payment, APR, term, miles, years held, gas price) + two toggles (CPO, DIY maintenance).
2. **What each option really costs** — three cost cards with full breakdowns, retained resale value, and a monthly-payment footer.
3. **Where the money actually goes** — stacked bar chart breaking each car into purchase / interest / fuel / insurance / maintenance, plus a live verdict.
4. **Maryland perks that tip the math** — charger rebate, EV electricity rates, CPO.
5. **How old is too old?** — Model 3 and Model Y year-by-year buying guidance.
6. **Two real certified cars** — actual Tesla.com CPO listings (examples Craig pulled together).
7. **The five things to actually check** — battery/warranty, home charging, loan term, insurance quote, depreciation.

---

## Key modeling assumptions

These are the estimates baked into the calculator. They live in the `compute()` function in `index.html` and are easy to adjust.

| Input | Assumption |
|---|---|
| Gas car efficiency | 28 mpg |
| Tesla charging | $0.045/mile (home charging) |
| Gas insurance | $1,500/year |
| Tesla insurance | $1,950/year (EVs cost more to insure — pricier repairs) |
| Gas maintenance | $850/year ($380/year with DIY toggle — roughly parts-only) |
| Tesla maintenance | $350/year ($120/year if CPO; $290/year with DIY) |
| Gas depreciation | ~11%/year (strong residuals) |
| Tesla depreciation | ~15%/year + high-mileage penalty |
| CPO premium | +$2,000 to Tesla price, drops maintenance to near-zero |
| Home charger | ~$1,500 installed, **−$700 MD rebate = ~$800 net**, folded into the charging line |
| Cash car | $9,200 purchase, $2,200/yr repairs, ~24 mpg, near-zero resale |

### Decisions worth remembering (the "why")

- **The $700 charger rebate is NOT free money.** Earlier drafts credited it as a standalone gain, which double-counted the benefit. It's now correctly netted against the ~$1,500 install cost (~$800 real out-of-pocket) and included as a subcomponent of the Tesla's charging line. Don't revert this.
- **CPO and DIY don't stack on the Tesla.** If CPO is on, Tesla maintenance is already near-zero under warranty, so the DIY toggle doesn't apply a second discount. DIY's real effect is on the **gas car**, where the wrenchable work (oil, brakes, fluids, filters) lives — that's the point of the toggle. A handy owner narrows the Tesla's running-cost edge.
- **High annual mileage is the EV's biggest tailwind.** At Sergei's ~18k mi/year, cheap per-mile charging vs. $4 gas is a large swing — this is the input most responsible for the Tesla "winning" at defaults.
- **Resale is the softest number in the model.** Used-EV residuals have been volatile. The verdict is sensitive to the Tesla depreciation assumption; treat "worth at the end" as an estimate, not a promise.
- **Net cost, not gross spend.** Headline figures subtract retained resale value. The stacked bars show gross *spending*; the number on the right is *net* of resale.

### Model-year guidance (the heat-pump breakpoint)

- **Model 3:** the **2021 facelift** is the line — it added the heat pump (big cold-weather efficiency gain), double-pane front windows, chrome delete. Avoid 2017–18; 2019–20 buyable but not preferable; 2021 the upgrade; 2022 the sweet spot. VIN 10th character "M" = 2021. (Note: many Nov–Dec 2020 builds are 2021 model-year and *do* have the heat pump.)
- **Model Y:** launched 2020 *with* a heat pump, so here it's reliability, not features. Independent scoring flags 2020–21 as the weakest years (2021 worst); 2022+ is the value sweet spot. Early heat pumps had a known expansion-valve failure, fixed under warranty — verify the recall/valve fix on any 2020–21.

### Maryland specifics

- $700 home-charger rebate via the Maryland Energy Administration (subject to change / funding limits).
- EV-friendly or time-of-use electricity rates via Potomac Edison and Delmarva Power.
- Source: https://www.tesla.com/support/incentives#Maryland

---

## Technical notes

- **Single self-contained file.** All HTML, CSS, and JavaScript are inline in `index.html`. No build step, no dependencies, no framework. Any static host works.
- **To edit the math:** open `index.html`, find the `compute()` function. All assumptions are named variables near the top of that function.
- **To publish updates:** replace `index.html` in this repo (keep the filename exactly `index.html`). GitHub Pages rebuilds automatically in 1–3 minutes. Hard-refresh (Ctrl/Cmd+Shift+R) or use incognito to beat the browser/CDN cache when verifying.
- **Hosting:** GitHub Pages, served from the `main` branch root.

## Caveats to keep in mind

- All figures are estimates for framing a decision, not financial advice or quotes.
- The two Tesla listings in section 6 are live links that **will go dead** once those cars sell.
- Rebate amounts, utility rate programs, insurance costs, and used-car prices all drift over time — confirm current numbers before relying on them.
- The DIY toggle shows dollar savings only; it doesn't price Sergei's time, tools, or workspace.

---

*Built as a favor — a "Craig financial advice conversation" turned into a shareable tool. Last updated June 2026.*
