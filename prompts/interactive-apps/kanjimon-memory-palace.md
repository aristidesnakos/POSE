# Kanjimon Memory Palace

## Metadata
- **Category**: interactive-apps
- **Complexity**: Complex (800+ LOC)
- **Output Type**: Single HTML file
- **Key Skills Tested**: Canvas 2D rendering, game state management, pixel art generation, educational game design, keyboard input handling
- **Dependencies**: None (single HTML file with embedded CSS + JS, Google Fonts for "Press Start 2P")

## Prompt

> You are an excellent and obedient game designer. Replicate the environment exactly as I have instructed you to do so.
>
> ### Project Title: **Kanjimon!**
>
> #### 1. Core Concept
>
> Design a self-contained retro 2D pixel-art game, inspired by the aesthetic of early Pokemon (Game Boy Color era). The player explores a vibrant pixel world that resembles a carefully constructed memory palace and captures wild Kanji by correctly identifying their English meanings.
>
> Technical requirement:
> 1. Entire game in a single HTML file with embedded CSS + JavaScript (no external libraries).
> 2. Uses `<canvas>` 2D rendering context.
> 3. Canvas dimensions: 960x640 pixels (30 tiles wide x 32px, 20 tiles high x 32px).
> 4. TILE_SIZE: 32 pixels.
> 5. Game loop: 60 FPS using `requestAnimationFrame`.
> 6. Animation timing: Kanji bob every 500ms.
> 7. Follow the exact grid layout specified.
>
> #### 2. Visuals & Aesthetics
>
> **Overall style:**
> - High-fidelity 8-bit pixel art, colorful and nostalgic.
> - Mimic Pokemon's top-down overworld with crisp, bright, and charming tiles.
> - Text uses "Press Start 2P" font everywhere for authentic retro flavor (embedded via Google Fonts or base64 in CSS).
>
> **Player character:**
> - Sprite is described by `renderPlayer` in section 5.
>
> **Environment:**
> - Tile map: 30x20 grid.
> - Tile types: 0=renderGrass, 1=renderPath, 2=renderTree, 3=renderWater, 4=renderBuilding, F=renderFire, M=renderMountain, R=renderRiceField, P1=renderPerson (static NPC)
>
> **Wild Kanji sprites:**
> - 16x16 pixel, blocky grey background, mysterious black Kanji.
> - Each Kanji has a subtle 2-pixel vertical bobbing animation to look as if floating or pulsing.
> - Kanji can only be found on grass tiles.
> - Every Kanji has a specific location — this is a crucial feature of the memory palace.
>
> **Battle screen:**
> - Background: solid dark gray (#333).
> - Kanji Color: #F43D37
> - Centered enlarged Kanji sprite (5x scale).
> - Pixel-art style input box.
> - 3 buttons: "Capture!", "Hint", "Flee" (styled to match retro UI).
> - Hint text is in #F43D37, below the buttons.
> - After each Kanji is captured user gets 1 point.
>
> **UI text & labels:**
> - All text uses Press Start 2P font.
> - "Kanji Captured: X/10" on top left, outside the tile map.
> - Show/hide Kanji toggle on top right, same level as counter.
>
> #### 3. Game Mechanics & Flow
>
> **State 1: OVERWORLD** — Player moves tile-by-tile via arrow keys. Collision with Kanji triggers BATTLE.
>
> **State 2: BATTLE** — Arrow keys disabled. Input validation: trim whitespace, lowercase. Accept meaning variations (e.g., "tree" and "wood" for 木). Enter key submits. Correct = capture + remove from map + return to overworld. Incorrect = error message. Hint button shows meaning. Count each captured kanji only once.
>
> **State 3: GAME_OVER** — All 10 Kanji captured. Display "You're a Kanji Master! You've captured them all!" with "Play Again" button.
>
> **State management:**
> ```javascript
> const GameState = { OVERWORLD: 'overworld', BATTLE: 'battle', GAME_OVER: 'game_over' };
> ```
>
> #### 4. Game Data
>
> 10 JLPT N5 Kanji:
> ```
> 一: one, 二: two, 三: three, 人: person, 火: fire
> 水: water, 木: tree (accept wood), 山: mountain, 川: river, 田: rice field
> ```
>
> Kanji characters in mapData represent their fixed positions. After initialization, replace with grass tiles and store Kanji objects separately with coordinates.
>
> #### 5. Exact Map Layout
>
> ```javascript
> this.mapData = [
> [0,0,2,0,2,2,0,0,2,2,2,0,0,0,0,0,0,0,3,3,3,0,0,0,0,2,2,2,2,2],
> [0,0,'一',0,'二',0,0,1,0,'三',0,2,2,2,2,0,0,0,0,3,0,0,0,0,0,1,1,0,0,0],
> [0,0,2,2,2,2,2,1,0,0,2,1,1,1,2,0,0,0,0,1,0,0,0,0,0,U,1,0,0,0],
> [0,0,2,1,1,1,2,1,0,0,2,1,2,2,2,0,0,0,0,1,0,0,0,0,0,0,1,1,0,0],
> [0,0,2,1,3,1,2,1,0,0,0,1,0,0,0,0,0,0,0,1,0,3,3,3,3,2,2,1,0,0],
> [0,0,2,3,3,1,2,1,1,1,1,1,1,1,1,1,1,1,1,1,1,3,3,3,3,2,2,1,1,0],
> [0,0,2,2,2,1,1,1,0,0,0,0,1,0,0,0,0,0,0,0,0,3,3,3,3,2,2,0,1,0],
> [0,0,2,0,0,1,2,1,0,2,2,2,1,2,2,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0],
> [0,0,2,1,1,1,2,1,0,2,1,1,1,2,2,0,0,0,0,0,'P1',0,0,0,0,0,0,0,1,0],
> [0,0,2,1,0,1,2,1,0,2,2,2,2,2,2,0,0,0,0,0,'人',0,0,0,0,0,0,0,1,0],
> [0,0,2,1,0,2,2,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
> [0,0,2,1,0,2,2,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,'R','R',0,0,0],
> [0,0,2,1,1,1,2,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,'田','R',0,0,0],
> [0,0,2,2,2,0,2,1,2,2,2,0,0,0,0,0,0,0,0,0,'M',0,0,0,0,'R','R',0,0,0],
> [0,0,3,3,2,0,2,1,2,2,2,0,0,0,0,0,0,0,0,'山',0,0,0,0,2,2,2,2,2,2],
> [0,0,3,3,3,3,3,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
> [0,0,0,'水',3,3,3,1,2,2,2,2,2,2,2,2,2,0,0,0,0,0,0,3,2,2,2,2,2,2],
> [0,0,0,0,2,2,2,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,3,3,3,3,3,3,3],
> [0,0,0,0,2,2,2,1,0,0,0,2,0,0,0,0,0,0,0,'F',0,0,0,0,0,0,0,0,'川',0],
> [0,0,0,0,0,0,0,0,0,0,0,'木',0,0,0,0,0,0,'火',0,0,0,0,0,0,0,0,0,0,0]
> ];
> ```
>
> **Color palette:**
> ```javascript
> const COLORS = {
>   grass: { base: '#4a9d4a', dark: '#3d8b3d', light: '#5eb85e' },
>   water: { base: '#4682b4', highlight: '#87ceeb' },
>   tree: { trunk: '#8b4513', canopy: '#228b22', highlight: '#32cd32', shadow: '#006400' },
>   building: { wall: '#a0522d', roofBase: '#8b4513', roofPeak: '#654321', shadow: '#8b4513', windowDoor: '#2f1f0f' },
>   mountain: { base: '#808080', snowcap: '#FFFFFF' },
>   riceField: { base: '#6B8E23', dark: '#556B2F', highlight: '#7CFC00' },
>   player: { cap: '#ff0000', capVisor: '#cc0000', skin: '#ffdbac', shirt: '#4169e1', pants: '#2f4f4f', shoes: '#000000' },
>   kanji: { background: '#cccccc', text: '#000000', battleColor: '#F43D37' },
>   ui: { background: '#333333', text: '#FFFFFF', button: { background: '#808080', text: '#FFFFFF' } },
>   global: { background: '#1a1a2e' },
>   path: { base: '#8B4513', highlight: '#A0522D' }
> };
> ```
>
> **Render functions**: All use simple fillRect patterns with TILE_SIZE=32. Trees have trunk + elliptical canopy. Water has animated wave lines. Mountains are triangles with snowcaps. Player has red cap, skin face, blue shirt, dark pants with leg animation.
>
> **Body style:**
> ```css
> body { background: #1a1a2e; display: flex; justify-content: center; align-items: center; min-height: 100vh; font-family: 'Press Start 2P', monospace; color: white; }
> ```
>
> #### 6. Coding Rules
> - Count each successful kanji submission only once.
> - Character moves one tile at a time.
> - renderPerson is a static version of renderPlayer with a blue cap.
> - Replicate the environment exactly as instructed.
> - All Kanji must be rendered.
> - Hint font color is #F43D37.
> - Kanji counter and toggle are outside the game area box.

## Reference Materials

None — text-only prompt. All specifications are self-contained.

## Evaluation Checklist

- [ ] Opens in a browser without errors
- [ ] Canvas renders at 960x640 pixels
- [ ] Tile map matches the 30x20 grid layout specified
- [ ] All 10 Kanji characters are visible on the map
- [ ] Player moves tile-by-tile with arrow keys
- [ ] Walking into a Kanji triggers battle state
- [ ] Battle screen shows enlarged Kanji with input box and 3 buttons
- [ ] Correct answer captures the Kanji and removes it from the map
- [ ] Incorrect answer shows error message without capturing
- [ ] Hint button reveals the English meaning
- [ ] "Kanji Captured: X/10" counter updates correctly
- [ ] Show/hide toggle works for Kanji visibility
- [ ] Game over screen appears after all 10 Kanji captured
- [ ] Uses Press Start 2P font
- [ ] Color palette matches the specification
- [ ] Kanji bob animation is visible (2px vertical movement)
- [ ] Arrow keys are disabled during battle state
- [ ] Repeated Enter presses don't double-count captures

## Notes for Evaluators

**This is the most complex evaluation in POSE.** A single HTML file producing a complete, playable game with educational content. Expect partial passes — very few models will nail every detail.

**Common failure modes**:
- Map layout will likely be approximate rather than exact — that's acceptable if the general terrain types are correct
- Kanji placement is the hardest part — models often place them randomly instead of at specified coordinates
- Battle state management frequently has bugs (arrow keys not disabled, double-counting captures)
- Press Start 2P font may not load if Google Fonts is unavailable — check if there's a fallback
- Some models will produce a game that runs but looks nothing like the specification

**What "close enough" means**: If it produces a playable game where you can move a character, encounter Kanji, type answers, and win — that's a strong pass even if colors, layout, or animations are imperfect. The core loop (explore, encounter, answer, capture) is what matters most.

**Adaptability**: This prompt can be adapted for Chinese or Korean characters by swapping the Kanji data in section 4.
