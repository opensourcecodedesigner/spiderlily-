# Spiderlily 🌸

An interactive digital art piece featuring a procedural **Spider Lily** (Lycoris radiata) that grows and blooms in real-time in response to your hands. By using your webcam and machine learning hand tracking, you can organically cultivate and open the flower with natural gestures.

It is available in two versions:
1. **Web Version (`spiderlily-web/`)**: A self-contained Three.js + MediaPipe web application that runs directly in any modern browser.
2. **TouchDesigner Version (`InteractiveFlower.43.toe`)**: The original interactive installation piece built for TouchDesigner.

---

## 🎨 What is this project?

This project is an exploration of organic growth and human-computer interaction. The red spider lily (*Lycoris radiata* or *higanbana*) is famous for its striking shape—an umbel of radial, curling petals and long, elegant stamens. This project recreates its lifecycle procedurally, allowing a user to steer its growth and bloom.

---

## ⚙️ How it Works

The interaction follows a simple gesture system mapped to your hands:

### 1. Hand Tracking (MediaPipe)
The system uses a webcam to capture video frames and runs the **MediaPipe Hand Landmarker** model. It tracks the 3D coordinates of your hands, identifying the handedness (left vs. right) and calculating the distance between the tips of your **Thumb** and **Index** finger (pinch distance).

*   **Left Hand:** Grows the plant from a small bud at the base to a full stalk.
*   **Right Hand:** Drives the blooming process of the flower heads.
*   *Note:* The mapping holds even if you cross your hands because MediaPipe distinguishes left and right hands.

### 2. Growth & Blooming Choreography
*   **Procedural Growth:** The stem is built recursively using a branching algorithm (similar to an L-system), rendering solid, tapered cylinders.
*   **Choreographed Blooming:** The bloom isn't just a simple scale-up. It is driven by a staged **Anime.js timeline** that controls the flower state through 5 key poses:
    1.  **Tight Bud:** Petals are curled tightly inward.
    2.  **Lift & Separate:** Petals begin to lift upward.
    3.  **Arch & Recurve:** Petals arch outward and curl backward (recurve).
    4.  **Stamen Extension:** Filament stems grow out and sweep upwards at the tip (declinate posture).
    5.  **Full Bloom & Settle:** Anthers tilt, and the flower reaches its fully open state.
    
    Your right-hand pinch distance acts as a scrubber for this timeline, allowing you to manually step through the blooming process forward and backward.

### 3. Rendering & Aesthetics
*   **Geometry:** The petals are dynamic 3D ribbons generated frame-by-frame using mathematical functions for the recurve and edge ripples. The stamens are declinate curves ending in rotating anthers.
*   **Coloring:** Vertex colors are dynamically calculated to paint a pale pink throat, a midrib highlight, and rich crimson edges/tips.
*   **Bloom Glow:** A post-processing `UnrealBloomPass` is applied to create a vibrant, dream-like emissive glow.

---

## 🚀 Running the Web Version (Recommended)

The Web Version is completely self-contained in `spiderlily-web/index.html` and pulls libraries (Three.js, MediaPipe, Anime.js) from CDNs.

### Getting Started

1.  **Serve the files locally** (a server is required to allow webcam and MediaPipe to run under secure context rules):
    ```bash
    cd spiderlily/spiderlily-web
    python3 -m http.server 8642
    ```
    *(Alternatively, any local development server like `npx serve` or Live Server will work.)*
2.  Open **`http://localhost:8642`** in a WebGL-compatible browser (Chrome or Safari recommended).
3.  **Allow camera access** when prompted.

### Interactive Controls

*   **Left Hand (Pinch Out / Spread):** Grow the plant.
*   **Right Hand (Pinch Out / Spread):** Bloom the flower.
*   **Mouse Drag & Scroll:** Orbit, pan, and zoom the camera.
*   **Keyboard Shortcuts:**
    *   `D`: Toggle **Debug Mode** (auto-blooming cycle, no camera/hands needed).
    *   `1`, `2`, `3`: Pin the bloom state to bud, arching, or full bloom (in Debug Mode).
    *   `0`: Resume the automatic debug cycle.
    *   `H`: Toggle visibility of the HUD and webcam overlay.

---

## 🎛️ Running the TouchDesigner Version

The TouchDesigner version uses native GPU pipelines and a dedicated TouchDesigner network.

### Open it

1. Install **TouchDesigner** (free non-commercial license) from
   [derivative.ca](https://derivative.ca/download).
2. Get the **MediaPipe engine** (see below) into the `toxes/` folder.
3. Double-click **`InteractiveFlower.43.toe`**, or launch TouchDesigner and use
   **File → Open** to select it.
4. Press the play/perform controls to run it; a connected webcam drives the hand
   tracking.

### MediaPipe dependency

The TouchDesigner version needs **everything in the `toxes/` folder**. The tracking
toxes come with the repo; the one you have to add is the large **MediaPipe.tox**
engine:

Download **[MediaPipe.tox](https://github.com/cupidbity/spiderlily/releases/download/assets/MediaPipe.tox)**
and put it in the **`toxes/`** folder alongside the others. Once all the toxes are
in `toxes/`, the hand tracking will work.

`MediaPipe.tox` is the free **MediaPipe for TouchDesigner** plugin:
https://github.com/torinmb/mediapipe-touchdesigner

---

## Which one should I run?

- Want to try it instantly in a browser with just a webcam? → **Web version.**
- Want the full TouchDesigner piece to edit or perform? → **TouchDesigner version.**

---

## 📚 References & Inspiration
*   Original video/tutorial reference for building procedural stems: [YouTube Tutorial](https://www.youtube.com/watch?v=KGALeCnTTbg&t=32s).
*   MediaPipe plugin for TouchDesigner by Torin Blankensmith: [mediapipe-touchdesigner](https://github.com/torinmb/mediapipe-touchdesigner).

