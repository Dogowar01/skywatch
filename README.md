# Sky

**What's that bright thing in the sky tonight?**

A plain-language stargazing app for complete beginners, from Signal9. Open it,
give it a rough location, and it names the Moon, the visible planets and the
brightest stars above you right now — in ordinary words ("Look south-east,
about a third of the way up — that's Jupiter"), on a sky-dome chart, and on a
beginner-friendly horizon strip. Tap anything for a short, friendly story.

**Live:** https://dogowar01.github.io/skywatch/

## Features

- Sun, Moon (with phase), Mercury–Saturn, and 21 of the brightest stars —
  positions computed entirely on-device with low-precision Meeus/Schlyter formulas
- Two views: a **3D sky dome** you can drag to spin and tilt (rim = horizon,
  top = straight up, compass ring turns with you) and a **horizon strip**
  ("look SE, about 30° up")
- Plain-language blurbs, no jargon, no engagement mechanics
- **Constellation figures** — faint stick-figures for the Southern Cross,
  the Pointers, Orion, Scorpius, the Big Dipper and Cassiopeia (toggleable)
- **Later tonight** — what's still below the horizon but rising before dawn,
  with rise times and directions
- **"Worth a look" callouts** when the Moon or a planet sits close to
  something else bright
- **Rise & set times** for every object, sunset / first-dark / sunrise for
  your location, and next full/new Moon dates on the Moon's card
- Time scrubber — see what's up at 9pm before you head out
- Stars drawn in their real colours (orange Betelgeuse, blue-white Rigel) and
  gently twinkling — planets shine steady, just like the real sky
- A lightweight **"I spotted it"** log — tick off what you've found
- **GPS auto-locate** — finds you on first open and quietly refreshes each
  time the app opens (optional, off-switch in settings); manual entry and
  city presets as fallback
- **Settings panel** — location controls, auto-GPS toggle, night vision,
  spotted-log reset
- Red **night-vision mode** for use in the dark (swaps the photo backdrop for
  pure low-glare red)
- Knows whether it's actually dark enough to see anything, and says so
- Milky Way photo backdrop, dimmed hard so the app stays readable outdoors

## Tech

Single-file HTML PWA. No backend, no build step, no external scripts, no keys.
Vanilla JS, canvas charts, localStorage only, versioned service worker for full
offline use. Static deploy on GitHub Pages. iPhone-first.

---

Signal9 Apps · built with Claude Code
