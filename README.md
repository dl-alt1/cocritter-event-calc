# Clash of Critters — Event Value Calculator

A single-page calculator for comparing the payout of Clash of Critters events.
Price each reward once in pinballs, then see what every event returns for a
given spend, where the efficiency peaks, and which event is worth your time.

No build step, no dependencies, no server. One HTML file.

**Live:** https://dl-alt1.github.io/cocritter-event-calc/

---

## What it does

Reward values are set once at the top and shared across every event, so
changing what a wishbox is worth revalues all five ladders at the same time.
Each event tab shows its own placing and ROI, recalculated live.

| Event | Structure | Conversion |
|---|---|---|
| Fishing | 70 tiers to 20M points | pinballs → rods → points, across four luck bands |
| Zobo Shooter | 70 tiers to 100M points | pinballs → coins → points, scaled by team share |
| Marathon Party | 54 tiers to 128km | pinballs → skates → distance, scaled by team share |
| Treasure Hunt | 12 stages across 4 pairs | pinballs → pickaxes, with key milestones |
| Cozy Farm | 100 tiers to 1.45M points | pinballs → fertilizer → kg, via a growth model |

Every breakpoint row expands to show what that step adds and the running
cumulative total.

## Notes on the modelling

- **Candy and coins are excluded.** They scale per player and aren't
  comparable between accounts.
- **Fishing** applies a different points-per-rod rate in each luck band, so
  rod costs account for crossing bands rather than using one flat rate.
- **Cozy Farm** feeds at max growth speed and grows naturally at average
  speed over a fixed 72 hours. Feed crits (10% 2x, 4% 3x, 1% 4x, 1% 5x)
  average 1.25x and can be toggled on or off.
- **Marathon Party** chests give one pick, resolved as
  wishbox > pinball > capsule > skate. Skates and blue bento therefore never
  get taken. The 8.5–9.5km tiers are estimates from partial data.
- **Treasure Hunt** keys aren't priced directly — they pay out through the
  4/8/12/16 milestones. Stage thresholds are cumulative per pair.
- **Team events** scale your own contribution up by your share, so a lower
  share means the team reaches further than you paid for.

## Editing the data

Everything lives in the one file, near the top of the `<script>` block:

- `RODS_T`, `ZOBO_T`, `MARA_T`, `FERT_T` — tier tables, one row per
  breakpoint: `[points, pinball, capsule, wishbox, blue, purple, gold]`
- `HUNT_S` — Treasure Hunt stages, `[cumulative pickaxes, rewards]`
- `KEYREWARDS` — key milestones
- `RANKS` — team ranking rewards for places 1–10
- `VALS` — default reward values
- `EV` — per-event defaults (spend, conversion rates, luck bands, speeds)

## Local use

Open `index.html` in a browser. That's it — there's nothing to install and
nothing to run.

## Caveats

Values are estimates for comparison, not guarantees. Reward pricing is
subjective and the defaults are one reasonable set, not the correct one —
change them to match how you actually value each item.
