# Contour Target (Vision Therapy)

A single black ring on a warm white field, controlled from the keyboard, with no visible UI. Built for a TV or monitor driven from a PC over HDMI, or opened directly in a smart-TV browser.

Live: `https://<username>.github.io/contour-target/`

## What it is for

A peripheral contour target for strabismus vision therapy, after Greenwald, *Effective Strabismus Therapy*, Ch 5 step 9 (p.24) and the home version (p.25). The patient wears high plus "fog" lenses and red-green glasses, holds a red-green lustre in the central field, and a deliberately defocused ring sits in the periphery. Over sessions the fog and the ring's blur are reduced and the viewing distance increased, until lustre holds with a sharp ring at any distance.

Design consequences:

- The ring is the only contour on screen. No text, controls, cursor or borders.
- The ring is meant to appear double. Nothing on the page tries to help alignment.
- The user is fogged and cannot read the screen. Settings are set before the session (URL preset) and adjusted blind (keyboard steps).
- The background is warm white, not bright, and adjustable.

## Keyboard

| Key | Action |
|---|---|
| `C` or `Space` | Toggle ring visible / hidden |
| `↑` / `↓` or `+` / `-` | Ring diameter ± 0.025 (0.05–0.95 of shorter screen side) |
| `←` / `→` | Blur − / + 2 px (0–80) |
| `[` / `]` | Stroke width − / + 0.01 (0.01–0.5 of diameter) |
| `F` | Toggle flash mode (background alternates white / black) |
| `,` / `.` | Flash rate − / + 0.25 Hz (0.25–12) |
| `B` | Cycle background: pure white → warm → warmer → dim grey |
| `R` | Reset to defaults |
| `Enter` | Toggle fullscreen |
| `S` | Save current settings into the URL (bookmark or text it to a phone) |

Arrow keys and `Enter` are all a TV remote reliably sends, so size, blur and fullscreen are all reachable from a D-pad. Play/Pause often maps to `Space`, which toggles the ring.

## Defaults

Diameter 0.75, stroke 0.10, blur 0, background `#fff8f0`, ring visible, flash off at 1 Hz.

## Presets via URL

Settings are read from the hash on load:

```
https://<username>.github.io/contour-target/#d=0.75&s=0.10&blur=12&bg=fff8f0&ring=1&flash=0&hz=1
```

| Key | Meaning |
|---|---|
| `d` | Diameter as a fraction of the shorter screen side |
| `s` | Stroke width as a fraction of diameter |
| `blur` | Gaussian blur in px |
| `bg` | Background hex, no `#` |
| `ring` | `1` visible, `0` hidden |
| `flash` | `1` on, `0` off |
| `hz` | Flash rate |

Malformed or missing keys fall back to defaults. The last state is also kept in `localStorage`; a hash in the URL overrides it.

## Session usage

1. Fog lenses and red-green glasses on. Start at nose-to-screen distance with the default ring size; add blur to taste (the fog will blur it anyway).
2. Hold lustre in the centre. The ring will appear as two blurred rings offset vertically. That is expected; do not try to make them one.
3. Progress across sessions in this order: distance out with fog constant → fog down in 2 D steps → ring blur down → ring smaller and sharper. Go back one step whenever lustre is lost.
4. Flash mode (`F`) is a stabiliser if the lustre swirls (p.22).

## Technical notes

- One file, `index.html`, inline CSS and JS. No build step, no dependencies, no network requests after load.
- Ring is an inline SVG `<circle>` with `fill="none"`, so it scales and blurs cleanly. Blur is applied to the ring only; the background stays uniform.
- Written in ES5 for old TV browsers (Samsung Tizen, LG webOS, Hisense VIDAA): no optional chaining, `keyCode` fallback, vendor-prefixed fullscreen, feature-detected Wake Lock.
- Fullscreen may be ignored by some TV browsers; their own chrome usually auto-hides after a few seconds.

## Deployment

Repo root contains `index.html` and this file. GitHub → Settings → Pages → Deploy from a branch → `main` / root. Pushes redeploy automatically within about a minute.

## Out of scope

Textured or rope rings, stereo pairs, alignment aids, fixation dots and prism simulation belong to a later (vectogram) phase and are deliberately absent.
