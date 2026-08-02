# 🌺 Interactive Spider Lily — Web Version

An interactive 3D procedural Spider Lily (*Lycoris radiata*) experience built with **Three.js**, **MediaPipe Hand Tracking**, and **anime.js**.

The vibe? A sleek, high-contrast **monochrome webcam backdrop** with a vibrant, glowing crimson 3D flower blooming right over your hands in real time.

---

## 🌟 Key Features & Upgrades

* **Noir Monochrome Backdrop**: Fullscreen live webcam feed stylized in high-contrast black & white CSS grayscale (`filter: grayscale(100%) contrast(110%)`), making the colorful 3D plant pop.
* **TouchDesigner-Inspired Tracking**: Minimalist white pinch-distance lines and tracking dots (powered by MediaPipe Vision) replace clunky wireframe hand skeletons for an elegant, non-intrusive HUD overlay.
* **Dual-Hand Interactive Choreography**:
  * **Left Hand Pinch**: Controls the growth of the procedural branching plant skeleton.
  * **Right Hand Pinch**: Scrubs the staged **anime.js timeline** (tight bud → petals lift → arch & curl back → stamens extend → full bloom → settle).
* **Vibrant Emissive Shaders & Glow**: High-intensity red/crimson shaders (`emissive: 0xff0033`, `emissiveIntensity: 1.5`) paired with native CSS drop-shadow bloom filters so the flowers radiate over the camera feed.

---

## 🚀 Quickstart — How to Run

1. Navigate to the project folder:
   ```bash
   cd spiderlily/spiderlily-web
   ```

2. Start a local static HTTP server:
   ```bash
   python -m http.server 8642
   ```

3. Open your browser to:
   ```text
   http://localhost:8642
   ```
   *(Tested on Chrome, Brave, and Safari. Make sure to allow webcam permissions when prompted!)*

---

## 🎮 Keyboard Controls

| Key | Action |
|---|---|
| `D` | Toggle Debug Mode (auto-cycle bloom) vs. Live Hand Tracking |
| `1` / `2` / `3` | Pin bloom pose at Bud (`1`), Arching (`2`), or Full Bloom (`3`) in debug mode |
| `0` | Resume normal auto-cycle (debug mode) |
| `H` | Hide / Show HUD text overlay |
| `Mouse Drag` | Orbit 3D camera |
| `Mouse Scroll` | Zoom 3D camera in/out |
| `Right Drag` | Pan 3D camera |

---

## 🎛️ Live Console Tweaking (`PARAMS`)

All simulation and rendering parameters are centrally defined in the `PARAMS` object in `index.html` and exposed globally via `window.PARAMS`. You can tweak values live right from your browser's Developer Console:

```js
// Examples:
window.PARAMS.stamens.count = 24;          // Change stamen filament density (applies on reload)
window.PARAMS.interaction.swapHands = true; // Flip left/right hand pinch assignments
window.PARAMS.debug.bloomCycleSeconds = 5;  // Speed up debug bloom cycle
```

---

## 🛠️ Architecture

1. **`index.html`**: Self-contained single-page web app containing CSS layout, imports, MediaPipe vision pipeline, Three.js 3D scene, and anime.js timeline choreography.
2. **Procedural Geometry**: Custom tube geometries for tapered branching stalks, dynamically updated petal meshes (recurve + wave ripple), and curved filament tubes for stamens with golden anthers.
3. **Webcam & Overlay Pipeline**: HTML5 video element (grayscale filtered) at `z-index: 0`, 3D WebGL canvas with transparent background at `z-index: 1`, 2D pinch-tracking overlay at `z-index: 2`, and HUD overlay at `z-index: 3`.

Enjoy growing and blooming your spider lily! 🌺
