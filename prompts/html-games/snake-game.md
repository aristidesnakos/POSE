# Snake Game

## Metadata
- **Category**: html-games
- **Complexity**: Medium (200-800 LOC)
- **Output Type**: Single HTML file
- **Key Skills Tested**: Canvas 2D rendering, game loop, collision detection, keyboard input, score tracking, game state management
- **Dependencies**: None (single HTML file with embedded CSS + JS)

## Prompt

> Build a fully playable Snake game as a single self-contained HTML file with embedded CSS and JavaScript. No external libraries.
>
> ### Game Specifications
>
> **Canvas:**
> - Size: 600×600 pixels
> - Grid: 20×20 cells (each cell is 30×30 pixels)
> - Background: `#0a0a0f` (very dark)
> - Grid lines: subtle `rgba(255,255,255,0.03)` to give a faint grid texture
>
> **Snake:**
> - Body segments fill a cell with 2px padding inset (so 26×26px within a 30×30 cell)
> - Head: `#7c3aed` (purple)
> - Body segments: gradient from `#5b21b6` (near head) to `#2563eb` (near tail) — approximate with linear interpolation per segment
> - Rounded corners on each segment (`borderRadius` equivalent: draw with `roundRect` or simulate with arc)
> - Eyes on the head: two small white dots positioned based on direction of travel
>
> **Food:**
> - A pulsing red circle (`#ef4444`) centered in a random empty cell
> - Pulse animation: scale between 0.7 and 1.0 using a sine wave on each frame
>
> **Game loop:**
> - Target: 10 moves per second (100ms tick interval using `setInterval`)
> - Arrow keys and WASD control direction
> - Snake cannot reverse direction (pressing the opposite direction is ignored)
>
> **Collision:**
> - Wall collision: snake hits canvas edge → game over
> - Self collision: snake head overlaps any body segment → game over
>
> **Scoring:**
> - Eating food: +10 points
> - Snake grows by 1 segment when food is eaten
> - New food spawns in a random empty cell (not on the snake)
> - High score persists in `localStorage` across page refreshes
>
> **UI (outside the canvas):**
> - Title: "🐍 Snake" in large white text above the canvas
> - Score display: "Score: 0" and "Best: 0" side by side, updated in real time
> - Start screen overlaid on the canvas: "Press Space or Enter to start" centered text
> - Game over overlay on the canvas: "Game Over" in large text + final score + "Press Space or Enter to restart"
> - Controls hint below the canvas: "Arrow keys or WASD to move"
>
> **Visual style:**
> - Page background: `#0a0a0f`
> - Canvas has a subtle border: `1px solid rgba(255,255,255,0.1)` and a purple glow `box-shadow: 0 0 30px rgba(124,58,237,0.3)`
> - Score text: white, monospace font
> - Game over overlay background: `rgba(0,0,0,0.7)`, text in white
> - Font: system monospace stack (Consolas, Monaco, monospace)
>
> **Speed increase:**
> - Every 5 foods eaten, tick interval decreases by 5ms (minimum 50ms)
>
> **States:**
> - `IDLE` — waiting to start (shows start overlay)
> - `PLAYING` — active game
> - `GAME_OVER` — shows game over overlay, waiting for restart

## Reference Materials

None — text-only prompt. All specifications are self-contained.

## Evaluation Checklist

- [ ] Opens in a browser without errors
- [ ] Canvas renders at 600×600 pixels with a dark background
- [ ] Snake starts in the center of the grid and moves automatically
- [ ] Arrow keys control the snake's direction (WASD as bonus)
- [ ] Snake cannot reverse direction (opposite key is ignored)
- [ ] Food appears as a pulsing circle in a random cell
- [ ] Eating food increases score by 10 and grows the snake
- [ ] New food spawns in an empty cell (never on the snake body)
- [ ] Wall collision triggers game over
- [ ] Self-collision triggers game over
- [ ] Game over overlay is displayed with final score
- [ ] Game restarts correctly after game over
- [ ] Score and high score are displayed and update in real time
- [ ] High score persists after page refresh (localStorage)
- [ ] Game speed increases as score grows

## Notes for Evaluators

**This is a classic benchmark for frontend code generation.** Snake is simple enough to be achievable in one shot but complex enough to reveal gaps in game loop management, collision detection, and state handling.

**Common failure modes**:
- Snake can reverse direction (opposite key not ignored) — easy-to-miss bug
- Food spawning on top of the snake body
- Self-collision not detected until the head fully occupies a segment (off-by-one)
- Game over not properly resetting all state on restart
- High score in `localStorage` not loading correctly on page refresh
- Speed increase logic missing or broken
- Pulse animation on food implemented as CSS but broken on canvas (must use JS frame animation)

**What "close enough" means**: If the snake moves, eats food, grows, and dies correctly — that's a pass. The visual polish (gradient body, rounded corners, eye direction, pulse animation) is evaluated separately and is expected to be partially implemented. A game that plays correctly but looks plain still demonstrates the core competency.
