# Libraries, Dependencies, and Browser APIs

The supplied app loads these external resources:

| Resource | How the source uses it |
|---|---|
| Tailwind CSS CDN (`https://cdn.tailwindcss.com`) | Utility classes for UI layout and styling |
| Google Fonts — `Press Start 2P` | Retro 8-bit typography |
| Tone.js 14.8.49 CDN | Synthesized score and collision sounds |
| `@mediapipe/tasks-vision` 0.10.3 from jsDelivr | `HandLandmarker` and `FilesetResolver` for hand landmarks |
| MediaPipe hand-landmarker model from Google Cloud Storage | Model used by the hand tracking task |

## Browser APIs

- `navigator.mediaDevices.getUserMedia()` — requests webcam access.
- `HTMLCanvasElement` / Canvas 2D context — draws game graphics and hand landmarks.
- `requestAnimationFrame()` — schedules game and camera prediction loops.
- `localStorage` — stores settings and best score.
- `performance.now()` — supplies a timestamp for video detection.

## Dependency notes

- These resources are loaded from remote URLs; an internet connection is required for first-party app resources to load.
- No package manager manifest or local dependency bundle is included in the supplied source.
- The MediaPipe model and GPU delegate availability may vary by browser/device. If model or GPU initialization fails, the source shows an AI error status.
