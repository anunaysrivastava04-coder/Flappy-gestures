# Project Brain / Architecture Notes

## Purpose

A single-page browser game in which a bird moves vertically according to a tracked hand's position. Pipes move horizontally; the game checks collisions and increments the score when a pipe is passed.

## Main source structure

- HTML contains the welcome screen, menu, level selection, settings, shop, about/contact screens, pause/game-over UI, game canvas, and camera HUD.
- CSS contains the pixel/retro theme, responsive rules, screen overlays, buttons, and camera panel styles.
- A JavaScript module contains game state, configuration, drawing/update functions, settings, inputs, audio, and MediaPipe initialization.

## Runtime flow

1. Resize the 800×600 game canvas display to fit the viewport while preserving aspect ratio.
2. Start the animation loop with `requestAnimationFrame`.
3. Dynamically load MediaPipe Tasks Vision and its hand-landmarker model.
4. Request webcam access using `getUserMedia`.
5. For each new video frame, detect one hand and read landmark 9's Y coordinate.
6. Map the normalized Y coordinate using the selected sensitivity range and set `game.bird.targetY` when the game is playing.
7. Update bird movement, pipe positions, scoring, difficulty scaling, and AABB collision checks.
8. Draw the background, pipes, ground, and bird to the canvas.
9. Save supported preferences and best score in `localStorage`.

## Representative code: movement mapping

This is a source-derived excerpt showing the app's core hand-to-game mapping:

```js
const handY = landmarks[9].y;

let comfortTop = 0.2;
let comfortBottom = 0.8;

if (STATE.sensitivity === "low") {
  comfortTop = 0.05;
  comfortBottom = 0.95;
} else if (STATE.sensitivity === "high") {
  comfortTop = 0.35;
  comfortBottom = 0.65;
}

let mappedY = (handY - comfortTop) / (comfortBottom - comfortTop);
mappedY = Math.max(0, Math.min(1, mappedY));

if (STATE.screen === "playing") {
  game.bird.targetY = mappedY * CONFIG.height;
}
```

## Representative code: collision rectangle

```js
checkAABB(rect1, rect2) {
  return (
    rect1.x < rect2.x + rect2.w &&
    rect1.x + rect1.w > rect2.x &&
    rect1.y < rect2.y + rect2.h &&
    rect1.y + rect1.h > rect2.y
  );
}
```

## Persistence keys used by the source

- `flappyBest`
- `flappyDiff`
- `flappySens`
- `flappySkel`
- `flappyFPS`
- `flappySkin`
- `flappyBg`

## Known source-level caveats

- The Space key handler checks `STATE.screen === "menu-screen"`, while the menu flow assigns `"menu"` to `STATE.screen`; that shortcut may not start the game as intended.
- The settings screen uses `STATE.gameActive` to decide where to return; test settings navigation in both menu and in-game flows.
- The supplied source has no automated tests, build configuration, dependency manifest, or explicit license declaration.
- Sensitivity controls adjust the hand-coordinate mapping; they do not change the MediaPipe model's detection threshold.
