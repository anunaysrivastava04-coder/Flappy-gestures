# Features (from the supplied source)

- Webcam preview and real-time hand landmark detection using MediaPipe Tasks Vision.
- One-hand tracking in video mode; landmark 9's vertical coordinate drives bird movement.
- Configurable tracking sensitivity: Low, Medium/Normal, and High.
- Optional green hand-skeleton overlay.
- Keyboard controls using W/S and the arrow keys.
- Touch start/move handling for direct vertical dragging on touch devices.
- Easy, Normal, and Hard difficulty settings.
- Scoring when pipes are passed; best score persisted in `localStorage`.
- Fifteen bird-skin color themes.
- Four backgrounds: Normal, City, Hills, and Village.
- FPS cap setting: 30, 60, or 120.
- Canvas-based retro graphics and animated bird movement.
- Tone.js synthesized sounds for scoring and collisions.
- Menu, level selection, pause, settings, shop, about, contact, and game-over screens.
- Responsive layout rules for smaller screens.

## Source limitations / accuracy notes

- Hand tracking uses a single landmark-based vertical position; the code does not implement a collection of distinct hand gestures such as pinch, fist, or thumbs-up.
- The app's source is a single HTML file with external CDN imports; no build system or `package.json` is supplied.
- The Space-key handler is present, but its check for the menu state does not match the actual state value assigned when the menu opens. The on-screen buttons are the reliable way to start.
- A "shop" interface allows choosing skins and backgrounds; the shown source does not implement an in-game currency or purchase economy.
