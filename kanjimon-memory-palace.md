You are an excellent and obedient game designer. Replicate the environment exactly as I have instructed you to do so.

## Project Title: **Kanjimon!**     

### 1️⃣ **Core Concept**

Design a self-contained **retro 2D pixel-art game**, inspired by the aesthetic of early Pokémon (Game Boy Color era). 
The player explores a vibrant pixel world that resembles a carefully constructed memory palace and captures **wild Kanji** by correctly identifying their English meanings.

📦 **Technical requirement:** 
1. Entire game in a single HTML file with embedded CSS + JavaScript (no external libraries). 
2. Uses `<canvas>` 2D rendering context.
3. **Canvas dimensions:** 960x640 pixels (30 tiles wide x 32px, 20 tiles high x 32px).
4. **TILE_SIZE:** 32 pixels.
5. **Game loop:** 60 FPS using `requestAnimationFrame`.
6. **Animation timing:** Kanji bob every 500ms.
7. Follow the exact grid layout specified.

###  2️⃣ **Visuals & Aesthetics**

� **Overall style:**

- High-fidelity 8-bit pixel art, colorful and nostalgic.
- Mimic Pokémon’s top-down overworld with crisp, bright, and charming tiles.
- Text uses **"Press Start 2P"** font everywhere for authentic retro flavor (embedded via Google Fonts or base64 in CSS).

👤 **Player character:**
- Sprite is described by `renderPlayer` in section 5️⃣ 

🌳 **Environment:**

- **Tile map:** 30×20 grid.
- Tile map contains just the elemments of the game, such as the tiles and sprites.
- Each tile type is described in section 5️⃣ by corresponding functions.
- **Tile types:**
  - `0`: `renderGrass`
  - `1`: `renderPath`
  - `2`: `renderTree`
  - `3`: `renderWater`
  - `4`: `renderBuilding`
  - `F`: `renderFire`
  - `M`: `renderMountain`
  - `R`: `renderRiceField`
  - `P1`: `renderPerson` (static player sprite)


👾 **Wild Kanji sprites:**

- 16×16 pixel, blocky grey background, mysterious black Kanji.
- Each Kanji has a subtle 2-pixel vertical bobbing animation to look as if floating or pulsing.
- Kanji can only be found on grass tiles. They can never be superimposed on top of path, trees, or water.
- Every Kanji has a specific location -- this is a crucial feature of the memory palace.
  
🌌 **Battle screen:**

- Background: solid dark gray (#333 or similar).
- Kanji Color: #F43D37
- Centered enlarged Kanji sprite (5× scale).
- Pixel-art style input box
- 3 buttons: "Capture!", "Hint", "Flee" (styled to match retro UI).
- Hint text is in #F43D37. Hint should be below the "Capture!", "Hint", "Flee" buttons.
- After each Kanji is captured user gets 1 point. 

🖋 **UI text & labels:**

- All text (including “Kanji Captured: X/10”, messages, buttons) uses **Press Start 2P** font.
- White or light-colored text on dark backgrounds for readability.
- “Kanji Captured: X/10” is located on the top left outside of the Tile map.
- There's a toggle to show/hide the Kanji -- outside of the tile map on the top right -- same level as the Kanji counter
  
###  3️⃣ **Game Mechanics & Flow** 
#### 🚶 **State 1: OVERWORLD**

- Player moves tile-by-tile via arrow keys.
- Collision (same tile as a Kanji) triggers BATTLE state.

#### ⚔ **State 2: BATTLE**

- Enlarged Kanji sprite floats center stage.
- **Input Handling:**
  - Arrow keys are disabled during BATTLE state.
  - Input validation: trim whitespace, convert to lowercase.
  - Accept variations for meanings (e.g., "tree" and "wood" for 木).
  - Pressing Enter key submits the answer.
- On correct entry → capture message, Kanji removed from map, return to OVERWORLD.
- On incorrect entry → error message, try again.
- There's a `hint` button that a user can press to see what the meaning is.
- If the Kanji is captured correctly, make sure to account for its allotted points only once.
- User pressing repetively `Enter` should result in counting the captured kanji only once -- make sure to manage state appropriately.

#### 🏆 **State 3: GAME_OVER**

- Trigger: once all 10 Kanji are captured.
- Display: `"You're a Kanji Master! You've captured them all!"`
- Centered “Play Again” button reloads page.

### **Game State Management:**
```javascript
// Explicit state enum
const GameState = {
  OVERWORLD: 'overworld',
  BATTLE: 'battle',
  GAME_OVER: 'game_over'
};

// State transition rules
// - OVERWORLD → BATTLE: player.x === kanji.x && player.y === kanji.y
// - BATTLE → OVERWORLD: correct answer submitted
// - OVERWORLD → GAME_OVER: capturedCount === 10
```

### 4️⃣ **Game Data**

Your list of 10 **JLPT N5 Kanji** with primary meanings — placed randomly on grass at start:

```
一: one        
二: two      
三: three         
人: person      
火: fire
水: water      
木: tree (accept wood)    
山: mountain   
川: river
田: rice field   
```
**Kanji Placement:**
- Kanji characters in `mapData` (e.g., `一`, `二`, `三`, `人`, `火`, `水`, `木`, `山`, `川`, `田`) represent their initial fixed positions. These should be replaced with a generic grass tile (`0`) after initialization, and the Kanji objects themselves should be stored in a separate array with their coordinates.

### 5️⃣ **Exact Game Environment Description**

✅ The world is compact (fits in a single screen or scrolls minimally), but feels vibrant and alive, just like classic Pokémon starting routes.
✅ The map design is indicated below. Place the Kanji in the exact positions instructed.

// Map data (0=renderGrass, 1=renderPath, 2=renderTree, 3=renderWater, F=renderFire, SC=renderMountainSnowcap, R=renderRiceField, P1=renderPerson, U=renderPerson (user's sprite)) 
```
this.mapData = [
[0,0,2,0,2,2,0,0,2,2,2,0,0,0,0,0,0,0,3,3,3,0,0,0,0,2,2,2,2,2],
[0,0,'一',0,'二',0,0,1,0,'三',0,2,2,2,2,0,0,0,0,3,0,0,0,0,0,1,1,0,0,0],
[0,0,2,2,2,2,2,1,0,0,2,1,1,1,2,0,0,0,0,1,0,0,0,0,0,U,1,0,0,0],
[0,0,2,1,1,1,2,1,0,0,2,1,2,2,2,0,0,0,0,1,0,0,0,0,0,0,1,1,0,0],
[0,0,2,1,3,1,2,1,0,0,0,1,0,0,0,0,0,0,0,1,0,3,3,3,3,2,2,1,0,0],
[0,0,2,3,3,1,2,1,1,1,1,1,1,1,1,1,1,1,1,1,1,3,3,3,3,2,2,1,1,0],
[0,0,2,2,2,1,1,1,0,0,0,0,1,0,0,0,0,0,0,0,0,3,3,3,3,2,2,0,1,0],
[0,0,2,0,0,1,2,1,0,2,2,2,1,2,2,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0],
[0,0,2,1,1,1,2,1,0,2,1,1,1,2,2,0,0,0,0,0,'P1',0,0,0,0,0,0,0,1,0],
[0,0,2,1,0,1,2,1,0,2,2,2,2,2,2,0,0,0,0,0,'人',0,0,0,0,0,0,0,1,0],
[0,0,2,1,0,2,2,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
[0,0,2,1,0,2,2,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,'R','R',0,0,0],
[0,0,2,1,1,1,2,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,'田','R',0,0,0],
[0,0,2,2,2,0,2,1,2,2,2,0,0,0,0,0,0,0,0,0,'M',0,0,0,0,'R','R',0,0,0],
[0,0,3,3,2,0,2,1,2,2,2,0,0,0,0,0,0,0,0,'山',0,0,0,0,2,2,2,2,2,2],
[0,0,3,3,3,3,3,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
[0,0,0,'水',3,3,3,1,2,2,2,2,2,2,2,2,2,0,0,0,0,0,0,3,2,2,2,2,2,2],
[0,0,0,0,2,2,2,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,3,3,3,3,3,3,3],
[0,0,0,0,2,2,2,1,0,0,0,2,0,0,0,0,0,0,0,'F',0,0,0,0,0,0,0,0,'川',0],
[0,0,0,0,0,0,0,0,0,0,0,'木',0,0,0,0,0,0,'火',0,0,0,0,0,0,0,0,0,0,0]
];
```

### **Quick Reference:**
```
| Element | Position | Size | Notes |
|---------|----------|------|-------|
| Score | (10,10) | 12px | "Kanji Captured: X/10" |
| Toggle | (860,10) | 80x30 | Show/hide Kanji |
| Battle Kanji | Center | 5x scale | #F43D37 color |
| Input | Below Kanji | 200x30 | Centered |
| Buttons | Below Input | 80x40 | 10px spacing |
```
**Animations:** Kanji bob 2px (sin wave), Player legs alternate every 250ms, Fire flickers randomly.
**Movement:** Arrow keys, tile-by-tile, boundary checks, no overlapping.

### **Color Palette Standardization:**
```javascript
const COLORS = {
  grass: { base: '#4a9d4a', dark: '#3d8b3d', light: '#5eb85e' },
  water: { base: '#4682b4', highlight: '#87ceeb' },
  tree: { trunk: '#8b4513', canopy: '#228b22', highlight: '#32cd32', shadow: '#006400' },
  building: { wall: '#a0522d', roofBase: '#8b4513', roofPeak: '#654321', shadow: '#8b4513', windowDoor: '#2f1f0f' },
  mountain: { base: '#808080', snowcap: '#FFFFFF' },
  riceField: { base: '#6B8E23', dark: '#556B2F', highlight: '#7CFC00' },
  player: { cap: '#ff0000', capVisor: '#cc0000', skin: '#ffdbac', shirt: '#4169e1', pants: '#2f4f4f', shoes: '#000000' },
  kanji: { background: '#cccccc', text: '#000000', battleColor: '#F43D37' },
  ui: { background: '#333333', text: '#FFFFFF', button: { background: '#808080', text: '#FFFFFF' } },
  global: { background: '#1a1a2e' },
  path: { base: '#8B4513', highlight: '#A0522D' }
};
```

#gameCanvas {
    display: block;
    background: #4a9d4a;
}

### **Render Functions Reference:**
```javascript
// All functions use simple fillRect patterns with TILE_SIZE=32

renderGrass(x, y) {
    this.ctx.fillStyle = COLORS.grass.base;
    this.ctx.fillRect(x, y, 32, 32);
    // Add random texture spots
}

renderPath(x, y) {
    this.ctx.fillStyle = COLORS.path.base;
    this.ctx.fillRect(x, y, 32, 32);
    // Add texture variation
}

renderTree(x, y) {
    // Base grass tile
    this.renderGrass(x, y);
    // Trunk
    this.ctx.fillStyle = COLORS.tree.trunk;
    this.ctx.fillRect(x + 12, y + 20, 8, 12);
    // Canopy shadow
    this.ctx.fillStyle = COLORS.tree.shadow;
    this.ctx.beginPath();
    this.ctx.ellipse(x + 16, y + 15, 16, 12, 0, 0, 2 * Math.PI);
    this.ctx.fill();
    // Canopy main
    this.ctx.fillStyle = COLORS.tree.canopy;
    this.ctx.beginPath();
    this.ctx.ellipse(x + 16, y + 12, 15, 11, 0, 0, 2 * Math.PI);
    this.ctx.fill();
    // Canopy highlight
    this.ctx.fillStyle = COLORS.tree.highlight;
    this.ctx.beginPath();
    this.ctx.ellipse(x + 18, y + 8, 8, 6, 0, 0, 2 * Math.PI);
    this.ctx.fill();
}

renderWater(x, y) {
    this.ctx.fillStyle = COLORS.water.base;
    this.ctx.fillRect(x, y, this.TILE_SIZE, this.TILE_SIZE);
    // Wave lines
    this.ctx.fillStyle = COLORS.water.highlight;
    const waveOffset = Math.sin(this.lastTime / 500 + x) * 2;
    this.ctx.fillRect(x, y + 10 + waveOffset, this.TILE_SIZE, 3);
    this.ctx.fillRect(x, y + 25 - waveOffset, this.TILE_SIZE, 3);
}

renderPlayer() {
    const x = this.player.x * 32, y = this.player.y * 32;
    // Red cap, skin face, blue shirt, dark pants
    // Animation: alternate leg positions based on animFrame
}

renderMountain(x, y) {
      // Gray base of the triangle
      this.ctx.fillStyle = '#808080'; // Gray color
      this.ctx.beginPath();
      this.ctx.moveTo(x, y + this.TILE_SIZE); // Bottom-left
      this.ctx.lineTo(x + this.TILE_SIZE, y + this.TILE_SIZE); // Bottom-right
      this.ctx.lineTo(x + this.TILE_SIZE / 2, y); // Top-center
      this.ctx.closePath();
      this.ctx.fill();

      // White snowcap (top half of the triangle)
      this.ctx.fillStyle = '#FFFFFF'; // White color
      this.ctx.beginPath();
      this.ctx.moveTo(x + this.TILE_SIZE * 0.25, y + this.TILE_SIZE * 0.5); // Left point of snowcap
      this.ctx.lineTo(x + this.TILE_SIZE * 0.75, y + this.TILE_SIZE * 0.5); // Right point of snowcap
      this.ctx.lineTo(x + this.TILE_SIZE / 2, y); // Top-center
      this.ctx.closePath();
      this.ctx.fill();
    }

// Rice Field, Fire, Person: Similar simple patterns
```


### 6️⃣ **Coding Rules**
- Count each successful kanji submission only once.
- Character moves one tile at a time.
- renderPerson is essentially a static version of the renderPlayer function, but with a blue cap.
- Replicate the environment exactly as I have instructed you to do so.
- All of the Kanji must be rendered.
- Ensure the hint font is #F43D37.
- Also ensure the Kanji counter and toggle are outside of the game area box and above to the left and right, respectively.

The application itself has the following background style:
```
body {
    background: #1a1a2e;
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    font-family: 'Press Start 2P', monospace;
    color: white;
}
```
