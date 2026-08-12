# Echo Runner — Technical Implementation

## Architecture

Single-file HTML5 game (`index.html`). No build step, no bundler.

### Dependencies (CDN — NOT bundled into ZIP)
| Library | Version | Purpose |
|---|---|---|
| Phaser 3 | 3.88.2 | Game engine (rendering, input, scenes) |
| Space Mono | Google Fonts | UI typography |
| CrazyGames SDK | v3 | Ad integration, gameplay events |

---

## Coordinate System

The track is a circle whose **center is below the visible screen**.

```
Screen: 960 × 540 px
Track Radius (TR): 500 px
Circle Centre (CX, CY): (480, 840)  ← 300px below screen bottom
Track Surface Y (TSY): CY - TR = 340

Visible arc: approx ±53° from player = ~29% of circle ✓
```

The player is **always fixed** at `(CX, TSY)` = `(480, 340)`.
Instead of the player moving, the **world rotates** (worldAngle increases each frame).

### Angular Conventions
- Screen angle 0° = right, 90° = down (standard CSS/Canvas convention)
- Player is always at screen angle **-π/2** (top of circle)
- An obstacle at circle-angle `α` has screen position:
  ```
  screenAngle = α - worldAngle
  x = CX + TR * cos(screenAngle)
  y = CY + TR * sin(screenAngle)
  ```
- Obstacle "reaches" player when `screenAngle = -π/2`, i.e. `worldAngle = α + π/2`

### Relative Angle (collision test)
```javascript
// Static obstacle
relAngle = (α - worldAngle + π/2) mod 2π   → normalize to [-π, π]

// Ghost (deployed when worldAngle = ghostWA)
// Ghost's circle-angle: θ_ghost = ghostWA - π/2
relAngle = (ghostWA - worldAngle) mod 2π    → normalize to [-π, π]

Collision fires when |relAngle| < COL_A (0.037 rad ≈ 2.1°)
```

---

## Scene Graph

```
BootScene   → 1s loading screen, CrazyGames SDK init
MenuScene   → Title + animated demo track
GameScene   → Main gameplay loop
DeadScene   → Score display, retry/menu
```

---

## GameScene — Graphics Layers

| Depth | Object | Content |
|---|---|---|
| 0 | gBG | Background fill, stars, horizon glow |
| 1 | gTrack | Planet body (fillCircle), surface arcs, glow |
| 2 | gGhost | Ghost orbs (translucent, pulsing) |
| 3 | gObs | Spike obstacles |
| 4 | gPl | Player orb + trail |
| 5 | gOver | Danger flash, death overlay |
| 9 | gBar | Ghost timer bar |
| 10 | Texts | Score, lap, speed, ghost warning |

---

## Ghost System

```javascript
// Deployment (every GHOST_INT ms):
this.ghosts.push(this.worldAngle);  // store worldAngle at time of placement

// Rendering ghost idx i (deployed at ghostWA):
const sa = (ghostWA - Math.PI / 2) - this.worldAngle;
const gx = CX + TR * Math.cos(sa);
const gy = CY + TR * Math.sin(sa);

// Collision test:
let rel = (ghostWA - this.worldAngle) % (2 * Math.PI);
if (rel > Math.PI) rel -= 2 * Math.PI;
if (Math.abs(rel) < COL_A && this.jOff < PR * 2.5) → die()
```

---

## Jump Physics

Simple Euler integration, no Phaser physics engine needed:

```javascript
// On jump input:
this.jVel = -JMP_VEL;   // -420 px/sec (upward)
this.jOff = 1;           // begin airborne

// Each frame:
this.jVel += GRV * dt;   // GRV = 940 px/sec²
this.jOff -= this.jVel * dt;
if (this.jOff <= 0) { this.jOff = 0; this.jVel = 0; land(); }

// Player screen Y:
py = TSY - PR - this.jOff;
```

Max jump height = JMP_VEL² / (2 × GRV) = 176400 / 1880 ≈ **94 px**
Tallest obstacle height = **74 px** → max clearance ~20px at peak (tight but fair)

---

## Audio Engine

All sounds are generated procedurally using the **Web Audio API**.
No external `.mp3` or `.ogg` files required → contributes zero bytes to ZIP.

| Event | Sound |
|---|---|
| Jump | Sine wave: 360 Hz → 840 Hz sweep, 140ms |
| Land | Triangle wave: 210 Hz → 55 Hz decay, 90ms |
| Ghost deployed | 3-voice ascending chord (200, 280, 380 Hz) |
| Death | Bass sweep + white noise burst |
| Milestone | Major triad (523, 659, 784 Hz) |
| BGM | Continuous 3-voice ambient drone (55, 82, 110 Hz) with LFO tremolo |

Audio is **muted by default** (CrazyGames requirement). Toggle with 🔊 button.

---

## CrazyGames SDK Integration

| SDK Call | When |
|---|---|
| `sdkGameLoadingStart()` | BootScene.create() |
| `sdkGameLoadingStop()` | After init, before MenuScene |
| `gameplayStart()` | GameScene.create() |
| `gameplayStop()` | GameScene.die() |
| `requestAd('midgame')` | After death delay, before DeadScene |

Audio is automatically suspended on `document.visibilitychange` (tab switch).

---

## Performance Notes

- All rendering uses Phaser 3 `Graphics` objects cleared and redrawn each frame
- `fillCircle` for planet body: efficient because most of the disc is off-screen (clipped by renderer)
- Obstacle visibility check: skip rendering if `oy > GH + 20` (below screen) or `oy < TSY - h - 40`
- Ghost/obstacle danger calculation: O(n) scan each frame, acceptable for n < 20
- Stars: 200 static points with pre-computed twinkle parameters

---

## Deployment

```bash
# Single file ZIP for CrazyGames:
Compress-Archive -Path index.html -DestinationPath echo-runner.zip -Force
```

ZIP contains only `index.html`.
All dependencies load from CDN (no offline support required by CrazyGames).
