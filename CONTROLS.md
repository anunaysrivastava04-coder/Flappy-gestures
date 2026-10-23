# Controls

| Input / setting | Behavior in the supplied code |
|---|---|
| W or Arrow Up | Decreases the bird's target Y by 50 while playing |
| S or Arrow Down | Increases the bird's target Y by 50 while playing |
| Touch / drag on canvas | Maps touch's vertical position to the bird's target Y while playing |
| Esc | Pauses while playing; resumes while paused; closes settings; exits some screens to the menu |
| On-screen PLAY / level buttons | Starts game flow and selects Easy, Normal, or Hard |
| Pause / Resume | Pauses or resumes the game loop state |
| Sensitivity Low / Med / High | Changes the vertical hand-coordinate mapping range |
| Show Skeleton On / Off | Enables or disables drawing the green hand landmark overlay |
| FPS 30 / 60 / 120 | Changes the game-loop FPS cap |
| Bird skins | Selects one of 15 color themes |
| Backgrounds | Selects Normal, City, Hills, or Village |

Hand movement controls the bird's target vertical position while a hand is detected and the game is playing. The source reads landmark index 9's normalized Y coordinate.

**Note:** The source contains a Space-key shortcut, but the menu-state condition does not match the state value used by the current menu flow. Use on-screen controls to start.
