# Echo Runner 3D — Technical Implementation

## Architecture

Single-file HTML5 game (`index.html`). No build step, no bundler.

### Dependencies (CDN — NOT bundled into ZIP)
| Library | Version | Purpose |
|---|---|---|
| Three.js | r128 | WebGL 3D Game engine (rendering, physics, scene graph) |
| Space Mono | Google Fonts | UI typography |
| CrazyGames SDK | v3 | Ad integration, gameplay events |

---

## 3D Coordinate System & Scene Graph

The game takes place on a massive rotating 3D disc (cylinder).

```
Track Radius: 150 units
Disc Group Position: (0, 0, 0)
Player Z-Position (fixed running track): Z = 75
Camera Position: (0, 35, 100) looking at (0, 0, 45)
```

### The Rotating World
Instead of moving the player forward, a `THREE.Group` containing the disc track (`discGroup`) rotates continuously around the Y-axis (`rotation.y`).

### Player Steering
The player meshes exist in **World Space**.
- **Left/Right Movement**: Changes the player's `X` coordinate from `-40` to `40`.
- **Jumping**: Changes the player's `Y` coordinate with basic Euler gravity.
- **Forward**: The player's `Z` coordinate is locked at `75`.

### Ghost Attachment Math
When a ghost is deployed:
1. We clone the player's current world position.
2. We convert that world position into the local coordinate space of the rotating `discGroup` using `discGroup.worldToLocal(worldPos)`.
3. The ghost is added as a child of `discGroup`.
4. As `discGroup` rotates, the ghost automatically orbits perfectly back to the player's location on subsequent laps!

---

## GameScene — Visual Layers & Lighting

| Light/Material | Purpose |
|---|---|
| AmbientLight | Provides base visibility (dark slate blue) |
| DirectionalLight | Casts real-time PCF soft shadows from player & obstacles onto the disc |
| PointLight | A warm light attached to the player to illuminate the track dynamically |
| Player Material | Emissive gold `MeshStandardMaterial` |
| Obstacle Material | Emissive red `MeshStandardMaterial` on a `ConeGeometry` |
| Ghost Material | Transparent, emissive cyan `MeshStandardMaterial` |
| Trail Particles | Additive blending point cloud following the player |

---

## Jump Physics

Simple Euler integration in the render loop:

```javascript
// On jump input:
vy = JUMP_V; // 45 units/sec

// Each frame:
vy += GRAVITY * dt;   // -120 units/sec²
py += vy * dt;
if (py <= P_RADIUS) { 
  py = P_RADIUS; 
  vy = 0; 
  SFX.land(); 
}
```

---

## Audio Engine

All sounds are generated procedurally using the **Web Audio API**.
No external `.mp3` or `.ogg` files required → contributes zero bytes to ZIP.

| Event | Sound |
|---|---|
| Jump | Sine wave: 360 Hz → 840 Hz sweep |
| Land | Triangle wave: 150 Hz → 50 Hz decay |
| Ghost deployed | 3-voice ascending chord (200, 300, 450 Hz) |
| Death | Square wave sweep 100Hz → 10Hz |
| BGM | Continuous 3-voice ambient drone (55, 82, 110 Hz) with LFO tremolo |

Audio is **muted by default** (CrazyGames requirement). Toggle with 🔊 button.

---

## Collision Detection
Performed via distance checking in the XZ plane, plus a Y height check:
```javascript
const dx = pWorld.x - mWorld.x;
const dz = pWorld.z - mWorld.z;
const distSq = dx*dx + dz*dz;
if (distSq < (radius*radius) && pWorld.y < mWorld.y + heightCheck) {
  die();
}
```

---

## CrazyGames SDK Integration
Integrated exactly as required: `sdkGameLoadingStart`, `sdkGameLoadingStop`, `gameplayStart`, `gameplayStop`, and mid-game ads on death retries.
