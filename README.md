# Flappy Gesture

Flappy Gesture is a browser-based, retro-style Flappy Bird-inspired game. The uploaded source uses a webcam and MediaPipe Hand Landmarker to move the bird vertically based on the detected hand position. It also supports keyboard movement and touch dragging.

> **Source-grounded note:** This documentation describes what is present in the supplied `index.html`. It does not claim that every control has been tested on every browser or device.


# 🎮 Visit Flappy Gestures

Play the live game here:

## 👉 [VISIT THE GAME](https://flappygestures.netlify.app/)

**Live Game URL:** https://flappygestures.netlify.app/

Click the link above to open Flappy Gestures and start playing. Follow the on-screen instructions to play the game.

---

Developed project: Flappy Gestures  
Platform: Web  
Live Demo: https://flappygestures.netlify.app/




## Features

- Real-time single-hand landmark detection using MediaPipe Tasks Vision.
- Webcam preview with a tracking status label.
- Bird vertical movement based on hand position.
- Keyboard controls: **W / S** or **Arrow Up / Arrow Down**.
- Touch dragging on the game canvas for mobile/tablet use.
- Easy, Normal, and Hard difficulty settings.
- Score, best-score display, and local best-score storage.
- Fifteen selectable bird skins and four selectable backgrounds.
- Settings for tracking sensitivity, skeleton overlay, and FPS cap (30 / 60 / 120).
- Retro pixel-art style drawn on an HTML canvas.
- Synthesized score and collision sounds through Tone.js.
- Pause, resume, restart, settings, and return-to-menu screens.
- Persistent settings stored in browser `localStorage`.

## Run locally

1. Download or clone this repository.
2. Serve it from `localhost` or deploy it to an HTTPS host.
3. Open `index.html` in a modern browser.
4. Allow camera access when prompted.
5. Click **ENTER**, choose **PLAY GAME**, and select a difficulty.
6. Hold one hand in view of the webcam and move it up or down to guide the bird.

Camera access is controlled by the browser. If camera access is blocked, the game displays a camera/AI error status. A browser's camera APIs generally require a secure context such as HTTPS or localhost.

### Optional local server

If Python is installed, open a terminal in the project folder and run:

```bash
python -m http.server 8000
```

Then visit `http://localhost:8000` in your browser. Stop the server with `Ctrl+C`.

## Controls

| Input | Action |
|---|---|
| W or Arrow Up | Move the bird target upward |
| S or Arrow Down | Move the bird target downward |
| Touch / drag | Move the bird target to the touched vertical position |
| Esc | Pause/resume or return from supported screens |
| On-screen buttons | Start, pause, resume, restart, open settings, or exit |

The Space key handler is present in the source, but its menu-state check does not match the state value assigned by the current menu flow; use the on-screen buttons to start the game.

## How hand tracking works

The source dynamically imports MediaPipe Tasks Vision, creates a `HandLandmarker` in video mode with `numHands: 1`, reads landmark 9's vertical coordinate, maps it through a sensitivity range, and updates the bird's target Y coordinate while the game is running.

```js
const { HandLandmarker, FilesetResolver } = await import(
  "https://cdn.jsdelivr.net/npm/@mediapipe/tasks-vision@0.10.3"
);

const vision = await FilesetResolver.forVisionTasks(
  "https://cdn.jsdelivr.net/npm/@mediapipe/tasks-vision@0.10.3/wasm"
);

handLandmarker = await HandLandmarker.createFromOptions(vision, {
  baseOptions: {
    modelAssetPath:
      "https://storage.googleapis.com/mediapipe-models/hand_landmarker/hand_landmarker/float16/1/hand_landmarker.task",
    delegate: "GPU"
  },
  runningMode: "VIDEO",
  numHands: 1
});
```

This snippet is taken from the uploaded app's implementation. The app uses external URLs for MediaPipe, its model, Tailwind CSS, Google Fonts, and Tone.js, so internet access is needed to load those resources.

## Technology stack

- HTML5
- CSS
- JavaScript (ES modules)
- HTML Canvas 2D API
- MediaPipe Tasks Vision — hand landmark detection
- Tailwind CSS CDN — utility styling
- Tone.js — synthesized sound effects
- Google Fonts — Press Start 2P
- Browser APIs: `getUserMedia`, `requestAnimationFrame`, and `localStorage`

No `package.json` or build step is included in the supplied source. The main app is a single HTML file.

## Project files

- `index.html` — the supplied game source
- `README.md` — project overview and instructions
- `DESCRIPTION.md` — short repository description
- `FEATURES.md` — feature inventory
- `USES.md` — intended uses
- `LANGUAGES.md` — languages used
- `LIBRARIES.md` — external libraries and browser APIs
- `CONTROLS.md` — control reference
- `brain.md` — architecture and implementation notes
- `LICENSE_GUIDANCE.md` — licensing status and guidance
- `.gitignore` — common local/generated files to exclude

## GitHub upload steps

### Browser method

1. Sign in to [GitHub](https://github.com/).
2. Select **+ → New repository**.
3. Choose a repository name, for example `flappy-gesture`.
4. Add a short description and choose Public or Private.
5. Create the repository.
6. Select **Add file → Upload files**.
7. Upload `index.html` and the Markdown documentation files from this folder.
8. Enter a commit message such as `Add Flappy Gesture game and documentation`.
9. Select **Commit changes**.

### Git command-line method

Install Git, open a terminal inside this folder, and replace the placeholders below:

```bash
git init
git add .
git commit -m "Add Flappy Gesture game and documentation"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/flappy-gesture.git
git push -u origin main
```

If the remote repository already contains commits (for example, a README created on GitHub), clone that repository first or follow Git's instructions to reconcile histories rather than blindly reinitializing it.

### Optional GitHub Pages deployment

1. Open the repository's **Settings**.
2. Open **Pages**.
3. Under the build/deployment section, select deployment from a branch if available.
4. Select the `main` branch and `/ (root)` folder, then save.
5. Wait for GitHub Pages to publish, then open the URL it provides.

Camera permissions depend on the deployed origin and browser; use the HTTPS GitHub Pages URL. Test webcam permission and CDN/model loading after deployment.

## Privacy and troubleshooting

- The page requests camera access through `navigator.mediaDevices.getUserMedia`.
- The source uses the camera stream for in-browser hand landmark detection. Review the external MediaPipe/CDN resources and browser permissions before use.
- If the camera does not start, check browser permissions and use localhost or HTTPS.
- If AI initialization fails, check internet access and the browser console for loading/model errors.
- If the hand is not detected, ensure it is visible and well-lit, then check the camera HUD status.
- The skeleton overlay can be toggled in settings.
- The selected difficulty, sensitivity, skeleton setting, FPS cap, bird skin, background, and best score are saved in `localStorage`.

## License

No license is specified in the supplied source. See `LICENSE_GUIDANCE.md`. Do not assume the project is MIT-licensed unless the copyright holder deliberately chooses that license.
