# Peony: Generative 3D Animation 🌸

An interactive, mathematical generative art piece running entirely in the browser. This project renders a 3D peony flower that continuously cycles through phases of growth, interactive blooming, and wilting. 

It utilizes a custom 3D rendering engine built on top of the 2D HTML Canvas and the p5.js library, featuring dynamic visual state transitions and post-processing glitch effects.

## ✨ Features

* **Continuous Lifecycle States:** The animation operates on a state machine (`growing` ➔ `interactive` ➔ `wilting` ➔ `waiting`), calculating delta-time to ensure smooth, framerate-independent physics.
* **Multi-Modal Rendering:** The visual style automatically transitions between three distinct computational aesthetics:
  * **Solid Mode:** Clean, geometric pixel clusters.
  * **Dot Mode:** Soft, circular particle-style rendering.
  * **ASCII Mode:** Real-time text rendering where pixel brightness is mapped to character density.
* **Interactive Physics:** The camera perspective eases smoothly toward the user's mouse position, and the flower head calculates slight physical displacement based on interactive "wind."
* **Algorithmic Glitch Engine:** A custom post-processing effect that randomly slices the canvas, applying chromatic aberration (color splitting) and horizontal displacement to contrast the organic flower with digital artifacts.

## 🛠 Tech Stack

* **HTML5 / CSS3:** Zero-dependency layout with a custom CSS-animated loading sequence.
* **Vanilla JavaScript:** Core logic, state management, and math functions.
* **p5.js:** Utilized for rendering geometry, matrix calculations, and managing the draw loop.

## 🧠 How It Works (Under the Hood)

This project avoids standard WebGL libraries in favor of a highly custom computational approach:

1. **Custom 3D Projection:** The flower is mathematically modeled using 3D coordinates (x, y, z). The `rot3D()` function manually calculates the sine and cosine rotation matrices to project these 3D points onto a flat 2D screen using perspective focal length division.
2. **Painter's Algorithm:** To handle depth sorting without a Z-buffer, the petals are pushed into an array with their calculated depth (`rz`) and sorted from back to front before rendering.
3. **The Buffer Pipeline:** The geometry is *not* drawn directly to the screen. 
   * First, the 3D flower is drawn to an invisible, offline graphics buffer.
   * Next, `loadPixels()` reads the raw RGBA data from that buffer.
   * Finally, a grid system iterates over those pixels, calculates their perceived brightness (`r*0.299 + g*0.587 + b*0.114`), and draws the final ASCII character, dot, or solid shape to the main screen.

## 🚀 Running the Project

Because the entire application is bundled into a single file with no external dependencies, installation is incredibly simple:

1. Clone or download this repository.
2. Open `index.html` directly in any modern web browser.
3. *Alternatively*, serve it via GitHub Pages for a live web link.

## 🎮 Controls

* **Mouse Move:** Rotate the viewing angle and influence the flower.
* **Mouse Click:** Manually trigger a digital glitch slice.
* **Key `G`:** Trigger the glitch effect.
* **Key `F`:** Toggle fullscreen mode.
