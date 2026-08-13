# Echo Runner 3D 👻

A true 3D top-down arcade runner on a massive rotating disc where your past movements become your enemies.

## 🎮 Play
Open `index.html` in any modern browser. No server required.

## ✨ Concept
You run on a glowing 3D disc that rotates beneath you. You can steer left and right across different lanes and jump over 3D obstacles. Every 5 seconds, a ghost of your exact position and lane is dropped on the track. Since the track rotates, ghosts come back around every lap. The longer you survive, the more your past haunts you.

## 🕹️ Controls
| Input | Action |
|---|---|
| `A` / `D` or `⬅` / `➡` | Steer Left / Right (switch lanes) |
| `SPACE` | Jump |
| `TAP Left/Right Side` | Steer (Mobile) |
| `TAP Top 30%` | Jump (Mobile) |

## 🧠 Strategy
- **Lap 1:** Learn where the static red crystal spikes are.
- **Lap 2-3:** First ghosts appear — start placing them in safe zones by steering to empty lanes before the timer hits 0.
- **Lap 4+:** The track is a minefield of your own decisions.

## 🏗️ Tech Stack
- **Three.js (r128)** — 3D WebGL game engine
- **Web Audio API** — procedural sound (no external audio files)
- **Vanilla JS** — game logic
- **CrazyGames SDK v3** — ads and gameplay tracking

## 🚀 CrazyGames Ready
- ✅ SDK v3 fully integrated
- ✅ Muted by default (autoplay policy)
- ✅ Audio pauses on tab switch
- ✅ Midgame ad on retry
- ✅ Single `index.html` deployment (< 1MB)
- ✅ Mobile touch support

## 📁 Files
| File | Purpose |
|---|---|
| `index.html` | Entire game |
| `concept.md` | Game design document |
| `implementation.md` | Technical reference |
| `README.md` | This file |

---
*Created by S0HAM03*
