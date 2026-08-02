# Spiderlily 🌸

An interactive, high-contrast 3D digital art piece featuring a procedural **Spider Lily (*Lycoris radiata*)** that grows and blooms in real-time driven by your hands.

Using your webcam and MediaPipe machine learning hand tracking, you can organically cultivate, open, and sculpt the crimson flower using subtle hand gestures—all set against a stylized, high-contrast monochrome background feed.

Available in two distinct builds:

* **Web Version (`spiderlily-web/`):** A self-contained Three.js + MediaPipe web application running live in any modern browser.
* **TouchDesigner Version (`InteractiveFlower.43.toe`):** The original installation piece built natively for TouchDesigner.

---

## 🎨 What is this project?

This project is a personal exploration into organic procedural systems, real-time computer vision, and human-computer interaction.

The red spider lily (*higanbana*) is famous in anime and lore for its striking, almost mystical silhouette—a radial cluster of curling crimson petals and long, elegant stamens. This project recreates its lifecycle algorithmically, giving you direct, physical control over its growth and bloom.

---

## ⚡ What's New in the Latest Build?

* **Noir Camera Backdrop:** Live webcam video stream styled in sleek, high-contrast black & white CSS grayscale, letting the bright red 3D flower pop dramatically on screen.
* **Minimalist Gesture Tracking:** Clean, TouchDesigner-inspired white tracking dots and pinch-indicator lines replacing bulky hand skeletons.
* **Direct WebGL Canvas Transparency:** Multi-pass composition setup ensuring zero-alpha canvas rendering behind the emissive 3D flower.

---

## ⚙️ How It Works

### 1. Gesture System (MediaPipe)

The system captures video frames from your webcam and runs the MediaPipe Hand Landmarker model to track key joint coordinates in 3D space:

* **Left Hand (Pinch/Spread):** Controls the structural growth of the plant stalk from a small bud to a full branching stem.
* **Right Hand (Pinch/Spread):** Drives the actual blooming process of the flower heads.
* *Note: MediaPipe detects handedness accurately even if you cross your hands.*

### 2. Growth & Bloom Choreography

* **Procedural Branching:** The stem is generated dynamically using a recursive branching algorithm to create tapered 3D cylinders.
* **Timeline Scrubbing (Anime.js):** Instead of a simple scale-up, blooming is driven by a staged keyframe timeline:
1. *Tight Bud* (Petals tightly wrapped)
2. *Lift & Separate* (Petals open upward)
3. *Arch & Recurve* (Petals arch outward and backward)
4. *Stamen Extension* (Filaments sweep out and upward)
5. *Full Bloom* (Anthers tilt into final posture)



Your right-hand pinch distance acts as an interactive scrubber for this timeline, letting you step forward and backward through the bloom fluidly.

### 3. Rendering & Emissive Glow

* **Dynamic Mesh Geometry:** Petals are built frame-by-frame using trigonometric functions to calculate recurve bends and edge ripples.
* **Emissive Crimson Shaders:** Custom material styling with high-intensity emissive channels and targeted drop-shadow blending so the spider lily glows vividly over the black & white camera feed.

---

## 🚀 Running the Web Version (Recommended)

The Web version is completely self-contained in `spiderlily-web/index.html` with external libraries loaded via CDNs.

### Getting Started

1. Serve the repository locally (a local server is required for webcam and MediaPipe security permissions):
```bash
cd spiderlily-web
python -m http.server 8642

```


2. Open **`http://localhost:8642`** in a WebGL-compatible browser (*Chrome, Brave, or Safari recommended*).
3. Grant camera permissions when prompted.

---

## 🎛️ Controls & Shortcuts

| Input | Action |
| --- | --- |
| **Left Hand Pinch Out / Spread** | Grow the stem and branch structure |
| **Right Hand Pinch Out / Spread** | Scrub the bloom timeline (open/close flowers) |
| **Mouse Left Drag** | Orbit 3D camera |
| **Mouse Right Drag** | Pan 3D camera |
| **Mouse Scroll** | Zoom camera in / out |
| **`D` Key** | Toggle Debug Mode (auto-blooming cycle without hand tracking) |
| **`1` / `2` / `3` Keys** | Pin bloom state to *Bud*, *Arching*, or *Full Bloom* (Debug mode) |
| **`0` Key** | Resume normal debug auto-cycle |
| **`H` Key** | Toggle HUD overlay and text visibility |

---

## 💻 Live Console Tweaking (`PARAMS`)

All simulation parameters are exposed globally via `window.PARAMS` in your browser console:

```javascript
// Example console tweaks:
window.PARAMS.stamens.count = 24;            // Change stamen density
window.PARAMS.interaction.swapHands = true;  // Flip left/right hand controls
window.PARAMS.debug.bloomCycleSeconds = 5;   // Speed up debug cycle

```

---

## 🛠️ Running the TouchDesigner Version

For the native GPU node-network build:

1. Install [TouchDesigner](https://derivative.ca/) (Free non-commercial license works).
2. Download `MediaPipe.tox` from [torinmb/mediapipe-touchdesigner](https://github.com/torinmb/mediapipe-touchdesigner).
3. Place `MediaPipe.tox` inside the `toxes/` directory alongside the other `.tox` assets.
4. Launch `InteractiveFlower.43.toe` in TouchDesigner and hit play.

---

## 📚 References & Inspiration

* Stem branching geometry inspired by procedural L-system tutorials.
* MediaPipe TouchDesigner integration plugin by Torin Blankensmith.
