# Echo Runner 👻

A circular-track arcade runner where your past movements become your enemies.

## 🎮 Play
Open `index.html` in any modern browser. No server required.

## ✨ Concept
You run automatically around a circular planet. The view shows only the bottom 20-30% of the track — like running on a planet's surface. Every 5 seconds, a ghost of your exact position is permanently placed on the track. Ghosts come back around every lap. The longer you survive, the more your past haunts you.

## 🕹️ Controls
| Input | Action |
|---|---|
| `SPACE` | Jump |
| `↑` / `W` | Jump |
| `TAP` / `CLICK` | Jump |

## 🧠 Strategy
- **Lap 1:** Learn where the 8 static obstacles are
- **Lap 2-3:** First ghosts appear — start placing them in safe zones
- **Lap 4+:** The track is a minefield of your own decisions

## 🏗️ Tech Stack
- **Phaser 3** — game engine
- **Web Audio API** — procedural sound (no external audio files)
- **Vanilla JS** — game logic
- **CrazyGames SDK v3** — ads and gameplay tracking

## 🚀 CrazyGames Ready
- ✅ SDK v3 fully integrated
- ✅ Muted by default (autoplay policy)
- ✅ Audio pauses on tab switch
- ✅ Midgame ad on retry
- ✅ Single `index.html` deployment
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
