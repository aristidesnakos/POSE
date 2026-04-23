# Flappy Bird Clone

## Metadata
- **Category**: html-games
- **Complexity**: Medium (200-800 LOC)
- **Output Type**: Single HTML file
- **Key Skills Tested**: Canvas 2D rendering, physics simulation, procedural generation, game loop, collision detection, game state management
- **Dependencies**: None (single HTML file with embedded CSS + JS)

## Prompt

> Build a fully playable Flappy Bird clone as a single self-contained HTML file with embedded CSS and JavaScript. No external libraries or images — all visuals must be drawn with Canvas 2D API calls.
>
> ### Game Specifications
>
> **Canvas:**
> - Size: 480×640 pixels (portrait orientation, centered on the page)
> - Sky gradient background: `#1a1a4e` (top) → `#3b5998` (bottom) — use `createLinearGradient`
> - Scrolling ground strip at the bottom: 60px tall, color `#8B4513` with a lighter `#a0522d` top edge
>
> **Bird:**
> - Draw as a circle (radius 15px) in yellow `#FFD700` with a small orange beak triangle pointing right, and a black dot eye
> - Position: fixed X at 120px, Y controlled by physics
> - Physics:
>   - Gravity: `0.4` pixels per frame added to vertical velocity each frame
>   - Flap: sets vertical velocity to `-8` (upward)
>   - Terminal velocity: cap downward velocity at `10`
> - The bird rotates to match its velocity (nose down when falling, nose up just after flap) — use `ctx.rotate(Math.atan2(vy, 6) * 0.5)` as the rotation formula
>
> **Pipes:**
> - Color: `#228B22` (green) with a slightly lighter `#2ecc40` cap (the wider end piece)
> - Pipe width: 60px
> - Gap between top and bottom pipe: 160px (vertical)
> - Pipes scroll left at 2.5 pixels per frame
> - New pipe spawned every 220 frames at a random gap position (gap center between 180px and 400px from the top, leaving room for the 60px ground strip)
> - Pipes are removed when they scroll off the left edge
> - Cap (end piece): 10px wider on each side, 20px tall
>
> **Scoring:**
> - +1 point when the bird passes the center of a pipe pair
> - Score displayed in large white text at the top center of the canvas (font size 36px, shadow for readability)
> - Best score persists in `localStorage`
>
> **Collision detection:**
> - Bird hits top/bottom pipe rectangle (accounting for caps) → game over
> - Bird hits the ground (y + radius ≥ canvas height − 60) → game over
> - Bird flies above the canvas top (y − radius ≤ 0) → game over
>
> **Game states:**
> - `IDLE`: Canvas shows the bird hovering (gentle sine-wave bob), game title "Flappy Clone" and "Tap / Space to start" message. Bird gently bobs using `Math.sin(Date.now() / 300) * 5`.
> - `PLAYING`: Active game loop
> - `DEAD`: "Game Over" text + score + best score + "Tap / Space to restart" — shown over a semi-transparent dark overlay
>
> **Controls:**
> - Space bar → flap
> - Mouse click / touch on canvas → flap
> - In IDLE: any of the above starts the game
> - In DEAD: any of the above restarts after a 500ms delay (prevent accidental instant restart)
>
> **Stars (background detail):**
> - On game start, generate 40 random small white dots (radius 1-2px) at random positions in the sky area
> - Stars stay static (don't scroll) to give a sense of depth
>
> **Sound (optional — no external files):**
> - Use the Web Audio API to generate short beep tones:
>   - Flap: 50ms sine wave at 880Hz
>   - Score: 80ms sine wave at 1046Hz
>   - Death: 200ms sawtooth wave descending from 440Hz to 220Hz
> - Sound should only play after the first user interaction (to satisfy browser autoplay policy)
>
> **Visual style (page wrapper):**
> - Page background: `#0a0a0f`
> - Canvas centered with `box-shadow: 0 0 40px rgba(59,89,152,0.5)`
> - Score and best score shown below canvas as text, white, monospace

## Reference Materials

None — text-only prompt. All specifications are self-contained.

## Evaluation Checklist

- [ ] Opens in a browser without errors
- [ ] Canvas renders at 480×640 with sky gradient and ground
- [ ] Bird is drawn using Canvas API (circle + beak + eye) — no external images
- [ ] Bird falls due to gravity and jumps on Space / click
- [ ] Bird rotates to match velocity direction
- [ ] Green pipes spawn from the right and scroll left
- [ ] Gap between pipes is consistent and large enough to be passable
- [ ] Score increments correctly when passing through a pipe gap
- [ ] Collision with pipes or ground triggers game over
- [ ] Game over overlay displays score and best score
- [ ] Game restarts cleanly after game over
- [ ] Best score persists across page refreshes (localStorage)
- [ ] Idle screen shows title and instruction before first game
- [ ] Stars visible in the background

## Notes for Evaluators

**Flappy Bird is a strong benchmark for physics-based game generation.** It requires correctly implementing gravity, collision rectangles, procedural pipe spawning, and multi-state game management — all in one shot.

**Common failure modes**:
- Gravity and flap velocity tuning is off — bird falls too fast or floats too slowly (check the specified constants)
- Pipe collision boxes are imprecise — bird dies when visually clear of pipes (or passes through them)
- Score is incremented multiple times per pipe (not just once at the center crossing)
- Game restart doesn't reset pipes and score to initial state
- Bird rotation is missing or always points in one direction
- Idle bob animation uses `setInterval` instead of being tied to `requestAnimationFrame` loop
- Web Audio API sounds may be skipped — that's acceptable as they're marked optional

**What "close enough" means**: If the bird flaps, pipes scroll, and you can actually play a round — that's a solid pass. The visual polish (rotation, star background, sound) is evaluated separately. A working game with basic shapes and correct physics is the core competency test.
