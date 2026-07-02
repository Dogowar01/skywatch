# Sky — Build Brief

**Signal9 Apps** · single-file HTML PWA · Claude Code handoff

---

## What it is

A plain-language "what's that bright thing in the sky tonight?" app for complete
beginners. Given your location and the current time, it names the Moon, the visible
planets, and a handful of the brightest stars, tells you in ordinary words where to
look, and shows it on a simple visual sky chart.

**Audience:** total non-astronomers — someone who walks outside, sees a bright dot, and
wants to know what it is. NOT astrophotographers or aurora chasers (that's Astro Planner
/ Aurora Watch — deliberately a different, much broader crowd).

**Non-negotiables:** no backend, no build step, no external scripts or CDNs (all vanilla
JS inline), offline after first load, keyless, localStorage only, installable PWA with a
versioned service worker, static deploy to GitHub Pages. iPhone-first.

---

## Core idea

Open the app → it works out what's up right now for your latitude/longitude → shows a
ranked plain-language list of visible objects AND a visual chart. Tap any object (in the
list or on the chart) for a short, friendly blurb. That's the whole loop.

No accounts, no settings to wade through, no jargon on the surface. "Look southeast,
about a third of the way up — that's Jupiter, the brightest planet."

---

## The astronomy engine

Reuse the existing Tamar Light sun/moon engine as the base, with **one addition:**

- **Planet positions** — add low-precision planetary formulas (Meeus-style / low-accuracy
  VSOP). Keyless, offline, no data files, a few hundred lines. Accuracy target: good
  enough to say "Saturn is low in the southwest" — arcminute precision is not needed.
- Compute, for the current time + observer lat/lng, the **alt-az** (altitude above
  horizon + azimuth compass bearing) of: Sun, Moon, Mercury, Venus, Mars, Jupiter,
  Saturn.
- **Bright stars:** embed a tiny inline catalogue of ~15–25 of the brightest/most
  recognisable stars (Sirius, Canopus, Arcturus, Vega, Capella, Rigel, Betelgeuse,
  Aldebaran, Antares, Spica, etc.) with RA/Dec + magnitude, and compute their alt-az the
  same way. Keep it small — this is orientation, not a full star atlas.
- An object is "up" if its altitude > ~0° (with a small buffer). Rank the visible list by
  brightness (magnitude), Moon and bright planets first.
- Use the Sun's altitude to know if it's actually dark enough to see things, and say so
  ("The sky isn't dark yet — check back after sunset").

---

## Visual modes (two, toggle between them)

### Mode A — Sky Dome (hero view)
A canvas sky-dome, same plotting muscle as Parked's radar:
- Circular dome: **horizon = outer edge, zenith = centre.**
- Compass directions **N / E / S / W** marked around the rim.
- Each visible object drawn as a dot at its correct alt-az: azimuth sets the angle around
  the circle, altitude sets the distance from centre (edge = horizon, centre = straight
  up). Dot size/brightness scaled by magnitude; the Moon shows its phase as a little
  lit-fraction glyph.
- Labels on the brighter objects; tap any dot → blurb card.
- Everything computed locally, redraws live as time passes.

### Mode B — Horizon Strip (beginner mode)
A low, wide band — the truest fit for "what's that bright thing?":
- A horizon line with compass bearings along the bottom (NE, E, SE, S, SW…).
- Objects pinned along it at their azimuth, raised by their altitude, with rough
  altitude guides (e.g. dashed lines at 30° and 60°).
- Reads like: "Look SE, about 30° up → Jupiter." Easiest possible mental model for
  someone who's never held a star chart.

Toggle between A and B; remember the last-used mode in localStorage.

### Explicitly NOT building: compass point-and-find AR
Tilt (altitude) is reliable in a PWA, but heading (`webkitCompassHeading`) is the same
flaky behaviour that bit Astro Planner — so a live "aim your phone at the sky" mode would
be unreliable and is **out of scope**. (Optional future: ship behind an "experimental"
toggle with an honest "approximate" warning. Not in v1.)

---

## Plain-language blurbs

Each object gets a short, warm, jargon-free card on tap:
- What it is ("Jupiter — the biggest planet, and usually the brightest point of light
  after Venus").
- Where to look, in words ("low in the southeast, about a third of the way up").
- One nice hook ("through binoculars you can sometimes spot its four largest moons").
- Moon also shows phase name + % illuminated.
App-authored text, no live data, no engagement mechanics. Calm and factual.

---

## Location & time

- **Geolocation API** for lat/lng (you know this well). If denied, let the user pick a
  location manually or type a rough one; fall back gracefully.
- Default to **now**, but allow scrubbing time forward/back a few hours ("what will be up
  at 9pm?") with a simple slider — the chart and list update live.
- All timezone/sidereal-time math done locally.

---

## Data model

- **localStorage** — saved location(s), last-used visual mode, and (optional) a "seen"
  log if you want a lightweight "objects I've spotted" tick-list. Keep v1 minimal; the
  spotted-log is optional.
- No IndexedDB needed unless you add the spotted-log with notes.

---

## Aesthetic

Signal9 night-sky register (lean on the Scriptorium / Oracle / Tamar Light lineage):
- Deep low-glare background, warm off-white type, restrained accent (brass/amber or a
  cool star-white) for the objects.
- Optional **red-tint night-vision mode** (you've built this before) — genuinely useful
  here since people use it in the dark. Worth including.
- Big, legible labels; generous space; no clutter. The dome and strip should feel calm
  and readable outdoors at night, not busy.
- Spectral serif for headings/blurbs, clean sans for the alt-az numbers.

---

## PWA / technical

- Single `index.html`, all JS/CSS inline. **Zero external dependencies** (no CDN — the
  old pinning-bug lesson).
- `manifest.json` for installability; dark theme colour.
- **Versioned service worker** caching the shell for full offline use (bump the version
  string each deploy — Oracle pattern).
- All astronomy is pure math; nothing hits the network at runtime.

---

## Explicitly out of scope (v1)

Compass AR / point-and-find · deep-sky objects, constellations as line-figures, full star
catalogues · satellite/ISS passes (that's the shelved Overhead / CORS problem — don't) ·
notifications/alerts · sharing. Note constellations and a spotted-log as easy v2
candidates.

---

## Definition of done

Walk outside, open Sky, and within a second see "Jupiter — low in the southeast" both
named in plain words and shown as a dot on the dome; tap it, get a friendly explanation;
flip to the horizon strip and it still makes sense; switch on night-vision mode; scrub to
9pm to see what's coming. Works offline, installed, no jargon, no accounts. A beginner
looks up and knows what they're seeing. That's the app.
