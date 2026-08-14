# Echo Runner 🏃⚡

A feature-rich, high-performance **3D Endless Track Runner game** built using **Three.js** and **HTML5 Canvas**. The application is completely self-contained in a single file, requiring no external build tools, asset downloads, or backend servers.

---

## ✨ Features

- **🎮 3D Graphics Engine**: Built with Three.js, featuring dynamic lighting, post-processing unreal bloom, metallic humanoid player rig, and responsive camera controls.
- **🎨 Skin & Theme Shop**: Integrated shop system with starting coin balance, unlockable player skins, and track color themes (Vaporwave, Cyberpunk, Synthwave, Neon).
- **🔊 Web Audio API Sound Synthesizer**: Custom procedural sound synthesis for jumps, coin collections, shop purchases, and game events — zero external `.mp3` or `.wav` dependencies.
- **🏆 Leaderboard System**: Built-in score ranking system tracking high scores, total runs, and coin stats with LocalStorage support and dedicated modal UI.
- **📱 Full Mobile & Desktop Control System**:
  - Glassmorphic on-screen touch control buttons (`▲ IN` / `▼ OUT`).
  - Split-screen side-tap steering (Left = Out, Right = In).
  - Intuitive vertical swipe gestures (Swipe Up = In, Swipe Down = Out).
  - Responsive 2-column mobile & landscape modal layout with top-right `✕` close buttons.
- **🖱️ Smart Input Separation**: Desktop mouse cursor is dedicated to UI interactions (Mute sound, Main Menu, Shop, Leaderboard, Restart) without interfering with player movement controls.
- **⚡ CrazyGames SDK v3 Ready**: Pre-integrated for web game portals and ad networks.

---

## 🕹️ Controls

### Desktop Controls
| Action | Key / Input |
| :--- | :--- |
| **Steer Inward (Towards Center)** | `W` or `▲ Up Arrow` |
| **Steer Outward (Away from Center)** | `S` or `▼ Down Arrow` |
| **UI Interaction** | Mouse Click (Mute, Shop, Play, Menu) |

### Mobile Controls
- **Touch Buttons**: Tap `▲ IN` or `▼ OUT` glassmorphic overlay buttons.
- **Screen Tap**: Tap right half of screen to move Inward, left half to move Outward.
- **Swipe Gestures**: Swipe Up to move Inward, Swipe Down to move Outward.

---

## 🚀 How to Run

1. Simply double-click **`index.html`** or open it in any web browser (Chrome, Firefox, Edge, Safari, Opera, Mobile Chrome/Safari).
2. Click **PLAY** on the main menu to start running!

No node modules, local server setup, or compilation needed.

---

## 🛠️ Technology Stack

- **HTML5 & CSS3** (Vanilla Glassmorphism UI & Flexbox layout)
- **JavaScript ES6+**
- **Three.js** (3D Rendering Engine & Post-Processing Bloom)
- **Web Audio API** (Procedural Audio Synthesis)
- **CrazyGames SDK v3**

---

## 📄 File Structure

- **`index.html`**: The complete single-file standalone web game containing all logic, rendering, styles, audio generators, and embedded textures.
- **`README.md`**: Project documentation and usage guide.
- **`LICENSE`**: MIT License copyright file.

---

## 📜 License

This project is licensed under the [MIT License](file:///d:/Web-Projects/Web-game-06/LICENSE) - Copyright (c) 2026 **S0HAM03**.
