# Landing

The front door for everything at [github.com/aiappbulder-hub](https://github.com/aiappbulder-hub) —
a single-page showcase of all twelve, split into Games and Apps, with a live link and
source link for each.

**Live:** https://aiappbulder-hub.github.io/Landing/ *(once Pages is enabled — see below)*

## What's on it

| App | What it is | Link |
|---|---|---|
| **Backfire** | Pandemic strategy where humanity's response is the weapon — arm traps before their trigger exists | [play](https://aiappbulder-hub.github.io/backfire/) · [src](https://github.com/aiappbulder-hub/backfire) |
| **Inferno** | Dante's *Inferno* as a cinematic 2D platformer, plus a 3D *Purgatorio* chapter | [play](https://aiappbulder-hub.github.io/inferno/game/) · [src](https://github.com/aiappbulder-hub/inferno) |
| **Wordle** | Wordle clone with a clue button and a live possible-words solver | [play](https://aiappbulder-hub.github.io/Wordle/) · [src](https://github.com/aiappbulder-hub/Wordle) |
| **Finance Dashboard** | Property, investments, super and retirement countdown — installable PWA | [open](https://aiappbulder-hub.github.io/Finance-Dashboard/) · [src](https://github.com/aiappbulder-hub/Finance-Dashboard) |
| **RunTrack** | Twelve running calculators + My Plan — installable PWA | [open](https://aiappbulder-hub.github.io/Runtrack/) · [src](https://github.com/aiappbulder-hub/Runtrack) |
| **HVAC Sales Tool** | Room-by-room sizing, VEU rebate estimator, unit selection | [open](https://aiappbulder-hub.github.io/hvac-tool/) · [src](https://github.com/aiappbulder-hub/hvac-tool) |
| **Whack-a-Dog** | Whack-a-mole with dogs, combos, and sleeping-dog penalties | [play](https://aiappbulder-hub.github.io/Whackadog/) · [src](https://github.com/aiappbulder-hub/Whackadog) |
| **Pawn Master** | Inherit Merrick's and its $18,000 debt; spot the forgeries — installable PWA | [play](https://aiappbulder-hub.github.io/Pawnshop/) · [src](https://github.com/aiappbulder-hub/Pawnshop) |
| **Fastest Finger** | Millisecond reflex game — stop the clock on target across ten worlds | [play](https://aiappbulder-hub.github.io/fastestfinger/) · [src](https://github.com/aiappbulder-hub/fastestfinger) |
| **Pocket Putt** | Eighteen holes of mini golf — drag to aim, past sand, water, ice and bumpers | [play](https://aiappbulder-hub.github.io/minigolf/) · [src](https://github.com/aiappbulder-hub/minigolf) |
| **Spanish** | Speaking-first Spanish course, Michel Thomas method, with spaced review | [open](https://aiappbulder-hub.github.io/Spanish/) · [src](https://github.com/aiappbulder-hub/Spanish) |
| **FocusTree** | Ten anti-burnout methods in one app; finish a task and it plants a tree | [open](https://aiappbulder-hub.github.io/focustree/) · [src](https://github.com/aiappbulder-hub/focustree) |

### A note on the Inferno link

Inferno's Pages site serves the repo root, but the game is published under `game/` and the
root has no `index.html` — so the bare `…/inferno/` URL 404s and the link here points at
`…/inferno/game/`. Adding a root `index.html` that redirects to `./game/` in the inferno repo
(the same trick Pawnshop already uses to forward `/Pawnshop/` to `/web/`) would let the bare
URL work, at which point this link can be shortened.

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
  from holes, Pawn Master the three golden balls on a swinging sign, FocusTree the 5-4-3-2-1
  count-in and a forest arriving one task at a time, Fastest Finger a needle snapping into
  the target window, Spanish an English prompt with the Spanish blurred out until it
  resolves over a speaking waveform, and Pocket Putt a ball rolling into the cup past a
  gold pin.
  Backfire gets its own logo's B**AC**KFIRE over a planet horizon, with a treatment wave
  that goes out in the blue bloc's colour and comes back red — the trap firing.
- Deliberately bare above the grid: no banner, no hero, no filter bar. The work is the first
  thing on screen. Artwork panels are kept small (76px) so a lot of the set fits at once.
- **Two sections, Games and Apps**, headed by small monospace labels with a hairline rule
  rather than large headings — the split is signposted without putting a wall of type back
  above the cards. Seven games and five apps: the newest game is a full-width **featured card**
  (`.card--wide`, artwork beside the copy, a pulsing *New* tag) so the rest land as 3+3 and
  3+2 in the three-column layout with no orphan row.
- Pointer-tracked spotlight and a subtle 3D tilt on hover; scroll reveal with a timeout safety
  net so nothing can stay invisible.
- Fully responsive, and every animation is disabled under `prefers-reduced-motion: reduce`.

## Running it locally

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

Or just open `index.html` in a browser.

## Enabling GitHub Pages

Pages is enabled, and `.github/workflows/deploy-pages.yml` triggers on pushes to `main` or to
the working branch `claude/landing-page-apps-w7l6ah` (this repo has no `main`, so the workflow
would never fire without the second trigger).

**Known issue:** pushes stopped triggering that workflow after run 7 on 2026-08-04 — later
commits sat unpublished while the live site kept serving run 7's build. If the site goes stale
again, the durable fix is to stop depending on Actions: **Settings → Pages → Source → Deploy
from a branch**, pointed at the default branch and `/ (root)`. `index.html` is already at the
root and `.nojekyll` is committed, so GitHub's built-in builder publishes on every push.

## Adding a new app

Copy any `<article class="card">` block in `index.html` into whichever `.grid` it belongs to
(Games or Apps), change the `--accent` colour, the `data-tags` (`game`, `tool`, `pwa` — kept as
metadata, no longer used for filtering), the copy, and the two links (give the Source link an `aria-label`). Bump the count in that
section's `<h2 class="sect">`. To feature it, add `card--wide` and a `tag--new`, and
take both off the previous featured card. If you want bespoke artwork, add a matching `.a-yourapp` block in
the artwork section of the stylesheet — otherwise the accent gradient alone still looks fine.
