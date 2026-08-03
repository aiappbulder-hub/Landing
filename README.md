# Landing

The front door for everything at [github.com/aiappbulder-hub](https://github.com/aiappbulder-hub) —
a single-page showcase of all seven apps, with a live link and source link for each.

**Live:** https://aiappbulder-hub.github.io/Landing/ *(once Pages is enabled — see below)*

## What's on it

| App | What it is | Link |
|---|---|---|
| **Inferno** | Dante's *Inferno* as a cinematic 2D platformer, plus a 3D *Purgatorio* chapter | [play](https://aiappbulder-hub.github.io/inferno/) · [src](https://github.com/aiappbulder-hub/inferno) |
| **Wordle** | Wordle clone with a clue button and a live possible-words solver | [play](https://aiappbulder-hub.github.io/Wordle/) · [src](https://github.com/aiappbulder-hub/Wordle) |
| **Finance Dashboard** | Property, investments, super and retirement countdown — installable PWA | [open](https://aiappbulder-hub.github.io/Finance-Dashboard/) · [src](https://github.com/aiappbulder-hub/Finance-Dashboard) |
| **RunTrack** | Twelve running calculators + My Plan — installable PWA | [open](https://aiappbulder-hub.github.io/Runtrack/) · [src](https://github.com/aiappbulder-hub/Runtrack) |
| **HVAC Sales Tool** | Room-by-room sizing, VEU rebate estimator, unit selection | [open](https://aiappbulder-hub.github.io/hvac-tool/) · [src](https://github.com/aiappbulder-hub/hvac-tool) |
| **Whack-a-Dog** | Whack-a-mole with dogs, combos, and sleeping-dog penalties | [play](https://aiappbulder-hub.github.io/Whackadog/) · [src](https://github.com/aiappbulder-hub/Whackadog) |
| **Pawn Shop** | Godot 4 shop sim — appraise and haggle. In development | [src](https://github.com/aiappbulder-hub/Pawnshop) |

## How it's built

One dependency-free `index.html` — same convention as the rest of the apps. No framework,
no build step, no external fonts or scripts, so it works offline and can't break from a CDN.

Design notes:

- **Every card's accent colour is lifted from that app's own interface** — RunTrack's teal
  `#00897B`, HVAC's orange `#f97316`, Wordle's green `#6aaa64`, and so on. The page reads as a
  set because the apps do.
- **The card artwork is bespoke per app**, hand-built in CSS/SVG rather than screenshotted:
  Inferno gets a receding tunnel with rising embers and a silhouette on the platform, Wordle
  gets five tiles flipping through their verdicts, RunTrack a closing pace ring, Finance a
  self-drawing portfolio line, HVAC an airflow scan across a grille, Whack-a-Dog pups popping
  from holes, Pawn Shop the three golden balls on a swinging sign.
- Pointer-tracked spotlight and a subtle 3D tilt on hover; filter chips for Games / Tools /
  Installable; scroll reveal with a timeout safety net so nothing can stay invisible.
- Fully responsive, and every animation is disabled under `prefers-reduced-motion: reduce`.

## Running it locally

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

Or just open `index.html` in a browser.

## Enabling GitHub Pages

The included workflow (`.github/workflows/deploy-pages.yml`) publishes the site on every push
to `main`. To turn it on: **Settings → Pages → Source → GitHub Actions**.

## Adding a new app

Copy any `<article class="card">` block in `index.html`, change the `--accent` colour, the
`data-tags` (`game`, `tool`, `pwa`), the copy, and the two links. Bump the counts in the hero
stats and the filter chips. If you want bespoke artwork, add a matching `.a-yourapp` block in
the artwork section of the stylesheet — otherwise the accent gradient alone still looks fine.
