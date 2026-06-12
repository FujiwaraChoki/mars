# Valles Aurorae — a playable Mars valley at sunrise

A single-file three.js game. No assets, no build step — every texture, mesh,
sound and the fallback score are generated from math at runtime.

![Mars](https://img.shields.io/badge/gravity-3.71%20m%2Fs%C2%B2-orange)

## Run

Open `index.html` in a browser (it loads three.js from a CDN), or serve it:

```sh
python3 -m http.server 8000
# → http://localhost:8000
```

## Play

| Input | Action |
|---|---|
| Click | lock cursor / start |
| WASD + mouse | walk and look |
| Shift | run |
| Space | jump (0.38 g — bound up the canyon walls) |
| **Hold left-click** | rocket thrust toward where you look (60 m/s) |
| **Hold right-click** | ultrafast burn (260 m/s) |
| M | music on/off |
| Esc | release cursor |

**Objective:** follow the trail of 17 glowing energy cores down the valley and
up the flank of Olympus Mons to the summit caldera (~7 km out, ~1,600 m up).
Cores refill your rocket fuel (+35); fuel also regenerates while you stand on
the ground. The fuel bar and distances live in the bottom-right HUD.

## What's procedural (everything)

- **Terrain** — infinite, streamed in 180 m chunks around the player.
  Heights come from a pure `terrainHeight(x, z)` function (fBm value noise +
  ridged multifractal canyon walls + a meandering valley floor), so physics
  and visuals can never disagree, and revisited terrain regenerates
  identically. Normals are analytic, so chunk borders are seamless.
- **Olympus Mons** — a shield-volcano profile with caldera, flank channels
  and basal escarpment, folded into the same height function: it is real,
  walkable ground, with a haze-baked far-distance mesh for the horizon view.
- **Ground material** — a Worley-noise pebble field, packed fines and
  desiccation cracks baked into seamless color / normal / roughness maps at
  startup.
- **Rocks** — noise-displaced, flat-shaded boulders that rest half-buried,
  clustered as talus near the canyon walls. Big ones have cylinder collision:
  they block you, and you can stand on them.
- **Sky** — a GLSL pre-dawn Mars atmosphere: dusty horizon band, near-black
  zenith with stars, and the real Martian quirk of a *blue* scattering halo
  around the rising sun. Bloom, procedural lens flare, drifting dust.
- **Audio** — rocket rumble and pickup chimes from raw Web Audio oscillators,
  plus a synthesized organ score (ticking clock, ostinato, swelling pads).
  If a file named `interstellar.mp3` that you legally own is placed next to
  `index.html`, it plays on loop instead (the file is git-ignored and must
  not be committed).

## License

Code: MIT. Bring your own music.
