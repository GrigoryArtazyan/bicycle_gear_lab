# 2×12 Gear Lab

An interactive lab for a 2×12 road drivetrain. Watch where the chain sits on every gear, see why cross-chaining wears the drivetrain, then ride a short course and get scored on cadence and chain line.

The app is one static page. GitHub Pages can host it with no build step. Fonts load from Google Fonts; everything else is in `index.html`.

## Play

After GitHub Pages is enabled, play it at [grigoryartazyan.github.io/bicycle_gear_lab](https://grigoryartazyan.github.io/bicycle_gear_lab/).

Locally, open `index.html` in a browser. That is the same page GitHub Pages will serve.

## What you can do

**Learn** shows the drivetrain before you ride it.

- A top view of chain line from the chainrings to the cassette. Sideways angles are exaggerated so a bad line is obvious.
- A side view of the chain running. Drag the cadence slider, or pause the animation.
- A readout for the selected gear: ratio, metres per pedal turn, speed at the current cadence, and chain angle.
- All 24 gears on one scale. Dots that stack vertically are nearly the same ratio on different rings, which is why the red gears are almost always avoidable.
- Tap a cog, a chainring, or a ladder dot to select that gear.

**Ride** is a short course, about 3.3 km, with ten sections from flat to a 10% grade.

- Keep cadence in the green band, 80–95 rpm.
- Stay out of red chain-line gears.
- Shift before the road changes. A front shift under a hard load costs points.
- The coach strip names a sensible gear for the section you are on and the one coming up. Turn it off with **Coach hints**.
- At the finish you get a letter grade, a score, and a best score saved in this browser.

The setup strip at the top switches crankset, cassette, and tire. The choice is remembered in this browser. Defaults match a Shimano 105 style 12-speed: 50/34, 11–34, 700×28c.

| Crankset | Cassette | Tire |
| --- | --- | --- |
| 50/34 or 52/36 | 11–34 or 11–30 | 700×25c, 700×28c, 700×32c |

## Controls

Arrow keys work on both tabs, unless focus is in a dropdown or slider.

| Action | Button | Key |
| --- | --- | --- |
| Easier rear gear (bigger cog) | Easier | `←` |
| Harder rear gear (smaller cog) | Harder | `→` |
| Small chainring | Small ring | `↓` |
| Big chainring | Big ring | `↑` |

On the ride, a front shift takes a moment to complete, the way a real front derailleur does. Rear shifts are immediate.

## How the ride is scored

Time in the 80–95 rpm band scores the most. 70–105 rpm still scores, at a lower rate. A red chain line drains the score. An amber line drains it more slowly. A front shift on a steep grade, or while cadence is under 60 rpm, costs 40 points and is called out on screen.

The letter grade comes from how much of the ride you spent in the target band, in an acceptable cadence, and cross-chained.

## Deploy to GitHub Pages

The workflow in `.github/workflows/pages.yml` publishes `index.html` on every push to `main` or `master`. It also runs when you start it by hand from the Actions tab.

1. The code lives in [GrigoryArtazyan/bicycle_gear_lab](https://github.com/GrigoryArtazyan/bicycle_gear_lab).
2. In that repository, open **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to **GitHub Actions**.
4. Open the **Actions** tab and wait for **Deploy GitHub Pages** to finish. The job summary includes the live URL.

The first run can take a minute. Later pushes update the same URL.

The workflow copies only `index.html` and `.nojekyll` into the published site. This README and the workflow file stay in the repository and are not part of the live page. `.nojekyll` tells GitHub not to run Jekyll if you ever switch Pages to “deploy from a branch” instead of Actions.

There is no install step. The lab is plain HTML, CSS, and JavaScript inside `index.html`. Fonts load from Google Fonts in the browser.

## Project layout

| File | Role |
| --- | --- |
| `index.html` | The whole lab: layout, drawings, ride simulation |
| `.github/workflows/pages.yml` | Publishes the page to GitHub Pages |
| `.nojekyll` | Skips Jekyll processing on branch deploys |
| `.gitignore` | Keeps local site output and Finder files out of git |

## Model notes

Chain-line zones use approximate 12-speed road geometry: a 43.5 mm chainline, 3 mm cog spacing, and a 410 mm chainstay. Green is fine to ride. Amber means the chain is at a visible angle, all right for a short stretch. Red is cross-chained: more noise, more wear, and a higher chance of dropping the chain. Modern drivetrains tolerate more angle than older ones, so treat the colours as habits, not a shop manual.

Speed uses the selected tire’s rollout. The ride assumes an 82 kg rider-and-bike, a steady effort, rolling resistance, and air drag, then picks a gear that lands near 87 rpm without a red chain line. It is a teaching model, not a power-meter file.
