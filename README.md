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
- Two views: **Sky dome** (horizon = edge, straight up = centre) and
  **Horizon strip** ("look SE, about 30° up")
- Plain-language blurbs, no jargon, no engagement mechanics
- Time scrubber — see what's up at 9pm before you head out
- Red **night-vision mode** for use in the dark
- Knows whether it's actually dark enough to see anything, and says so

## Tech

Single-file HTML PWA. No backend, no build step, no external scripts, no keys.
Vanilla JS, canvas charts, localStorage only, versioned service worker for full
offline use. Static deploy on GitHub Pages. iPhone-first.

---

Signal9 Apps · built with Claude Code
