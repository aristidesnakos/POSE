## Project Title: **Kanjimon!** 
### 1️⃣ **Core Concept**

Design a self-contained **retro 2D pixel-art game**, inspired by the aesthetic of early Pokémon (Game Boy Color era). The player explores a vibrant pixel world and captures **wild Kanji** by correctly identifying their English meanings. 

Goal: **capture all 25 Kanji** scattered across the world.

📦 **Technical requirement:** 
➡ Entire game in a single HTML file with embedded CSS + JavaScript (no external libraries). 
➡ Uses `<canvas>` 2D rendering context.
###  2️⃣ **Visuals & Aesthetics**

🎨 **Overall style:**

- High-fidelity 8-bit pixel art, colorful and nostalgic.
- Mimic Pokémon’s top-down overworld with crisp, bright, and charming tiles.
- Text uses **"Press Start 2P"** font everywhere for authentic retro flavor (embedded via Google Fonts or base64 in CSS).

👤 **Player character:**

- 16×16 pixel sprite representing a **human-like figure wearing a cap** (think: simplified Pokémon trainer).
- Palette: bright blue for the cap, simple shirt + pants contrast.
- Sprite whose legs move when walking.

🌳 **Environment:**

- **Tile map:** 30×15 grid.
- Tile types:
    - `grass`: Green pixel texture, speckled to feel alive.
    - `path`: Light brown / beige tiles with subtle dirt variation.
    - `trees`: Pixelated trees (8-bit style) bordering the map — chunky, round, classic RPG look, with deep green canopies and brown trunks.
    - `water`: Streaked bodies of water resembling a lake with light waves
- Each tile type is described in section 5️⃣

👾 **Wild Kanji sprites:**

- 16×16 pixel, blocky grey background, mysterious black Kanji — Unown-inspired.
- Each Kanji has a subtle 2-pixel vertical bobbing animation to look as if floating or pulsing.
- Each Kanji moves left or right at random, but is at least 1 pixel away from the nearest kanji.

🌌 **Battle screen:**

- Background: solid dark gray (#333 or similar).
- Kanji Color: #F43D37
- Centered enlarged Kanji sprite (5× scale).
- Pixel-art style input box
- 3 buttons: "Capture!", "Hint", "Flee" (styled to match retro UI).
- After each Kanji is capture user gets 1 point. 

🖋 **UI text & labels:**

- All text (including “Kanji Captured: X/25”, messages, buttons) uses **Press Start 2P** font.
- White or light-colored text on dark backgrounds for readability.
###  3️⃣ **Game Mechanics & Flow** 
#### 🚶 **State 1: OVERWORLD**

- Outside of the game on the top overlay: `"Kanji Captured: X/25"` in Press Start 2P.
- Player moves tile-by-tile via arrow keys.
- Wild Kanji wander grass tiles randomly (1 tile move per second).
- Collision (same tile as a Kanji) triggers BATTLE state.
#### ⚔ **State 2: BATTLE**

- Enlarged Kanji sprite floats center stage.
- On correct entry → capture message, Kanji removed from map, return to OVERWORLD.
- On incorrect entry → error message, try again.
- There's a `hint` button that a user can press to see what the meaning is.
- If the Kanji is captured correctly, make sure to account for its allotted points only once.
#### 🏆 **State 3: GAME\_OVER**

- Trigger: once all 25 Kanji are captured.
- Display: `"You're a Kanji Master! You've captured them all!"`
- Centered “Play Again” button reloads page.
### 4️⃣ **Game Data**

Your list of 25 **JLPT N5 Kanji** with primary meanings — placed randomly on grass at start:

```
一: one        二: two      三: three
四: four       五: five     六: six
七: seven      八: eight    九: nine
十: ten        人: person   日: sun (accept day)
月: moon (accept month)     火: fire
水: water      木: tree (accept wood)
金: gold (accept money)     土: earth (accept soil)
山: mountain   川: river
田: rice field 口: mouth
目: eye        手: hand     心: heart
```
### 5️⃣ **Exact Environment Description**

✅ There's a toggle to show/hide the Kanji -- outside of the map on the top right -- same level as the Kanji counter
✅ The world is compact (fits in a single screen or scrolls minimally), but feels vibrant and alive, just like classic Pokémon starting routes.
✅ Map tile layout is provided below.

```
// Map data (0=grass, 1=path, 2=tree, 3=water, 4=building/structure) 
this.mapData = [
[0,0,2,2,2,2,0,0,0,0,0,0,0,0,0,0,0,0,3,3,3,0,0,0,0,0,0,0,0,0,2,2,2,2,2,2,0,0,0,0],
[0,0,0,0,0,0,0,1,0,0,2,2,2,2,2,0,0,0,0,3,0,0,0,0,0,0,0,0,0,0,1,1,4,0,0,2,2,0,0,0],
[0,0,2,2,2,2,2,1,0,0,2,1,1,1,2,0,0,0,0,1,0,0,0,0,0,0,0,0,0,0,1,4,4,4,0,0,2,0,0,0],
[0,0,2,1,1,1,2,1,0,0,2,1,2,2,2,0,0,0,0,1,0,0,0,0,0,0,0,0,0,0,1,1,1,1,1,2,2,0,0,0],
[0,0,2,1,3,1,2,1,0,0,0,1,0,0,0,0,0,0,0,1,0,3,3,3,3,2,2,0,0,1,1,0,0,0,2,2,0,0,0,0],
[0,0,2,3,3,1,2,1,1,1,1,1,1,1,1,1,1,1,1,1,1,3,3,3,3,2,2,0,1,1,0,0,0,0,0,0,0,0,0,0],
[0,0,2,2,2,1,1,1,0,0,0,0,1,0,0,0,0,0,0,0,0,3,3,3,3,2,2,0,1,0,0,0,0,0,0,0,0,0,0,0],
[0,0,2,0,0,1,2,1,0,2,2,2,1,2,2,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,0,0,0,0,0,0,0,0,0],
[0,0,2,1,1,1,2,1,0,2,1,1,1,2,2,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,2,2,2,2,2,2,0,0,0,0],
[0,0,2,1,0,1,2,1,0,2,2,2,2,2,2,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,2,3,3,3,3,2,2,2,2,0],
[0,0,2,1,0,2,2,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,3,3,3,3,2,1,1,2,0],
[0,0,2,1,0,2,2,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2,2,2,2,2,2,2,1,0,0],
[0,0,2,1,1,1,2,1,0,0,0,0,0,4,4,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,1,1,0,0],
[0,0,2,2,2,0,2,1,2,2,2,0,4,4,4,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,0,0],
[0,0,3,3,2,0,2,1,2,2,2,0,4,4,4,4,0,0,0,0,0,0,0,0,2,2,2,2,2,2,2,2,2,2,2,1,3,3,3,3],
[0,0,3,3,3,3,3,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,3],
[0,0,0,0,3,3,3,1,2,2,2,2,2,2,2,2,2,0,0,0,0,0,0,0,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,3],
[0,0,0,0,2,2,2,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,3,3,3,3],
[0,0,0,0,2,2,2,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,3,3,3,3],
[0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,3,3,3,3]
];
```

```
            renderTree(x, y) {
                // Tree trunk
                this.ctx.fillStyle = '#8b4513';
                this.ctx.fillRect(x + 12, y + 20, 8, 12);
                
                // Tree canopy
                this.ctx.fillStyle = '#228b22';
                this.ctx.fillRect(x + 4, y + 4, 24, 20);
                
                // Canopy highlights
                this.ctx.fillStyle = '#32cd32';
                this.ctx.fillRect(x + 6, y + 6, 4, 4);
                this.ctx.fillRect(x + 18, y + 8, 6, 4);
                
                // Canopy shadows
                this.ctx.fillStyle = '#006400';
                this.ctx.fillRect(x + 20, y + 16, 6, 6);
                this.ctx.fillRect(x + 8, y + 18, 4, 4);
            }

            renderGrass(x, y) {
                // Base grass color
                this.ctx.fillStyle = '#4a9d4a';
                this.ctx.fillRect(x, y, this.TILE_SIZE, this.TILE_SIZE);
                
                // Add texture with random dark spots
                this.ctx.fillStyle = '#3d8b3d';
                for (let i = 0; i < 8; i++) {
                    const px = x + (i * 4) % this.TILE_SIZE;
                    const py = y + Math.floor(i / 8) * 4;
                    if (Math.random() > 0.6) {
                        this.ctx.fillRect(px, py, 2, 2);
                    }
                }
                
                // Lighter spots
                this.ctx.fillStyle = '#5eb85e';
                for (let i = 0; i < 6; i++) {
                    const px = x + (i * 5) % this.TILE_SIZE;
                    const py = y + Math.floor(i / 6) * 5;
                    if (Math.random() > 0.7) {
                        this.ctx.fillRect(px, py, 1, 1);
                    }
                }
            }

            renderBuilding(x, y) {
                const TILE_SIZE = 64; // Adjust as needed
                
                // Base building structure - main walls
                this.ctx.fillStyle = '#a0522d'; // Light brown wall color
                this.ctx.fillRect(x, y + 16, TILE_SIZE, TILE_SIZE - 16); // Main building body
                
                // Roof base
                this.ctx.fillStyle = '#8b4513'; // Medium brown for roof
                this.ctx.fillRect(x - 8, y, TILE_SIZE + 16, 24); // Extended roof base
                
                // Roof peak/ridge
                this.ctx.fillStyle = '#654321'; // Dark brown for roof peak
                this.ctx.fillRect(x - 4, y, TILE_SIZE + 8, 8); // Roof ridge
                
                // Building outline/shadow
                this.ctx.fillStyle = '#8b4513'; // Medium brown for shadows
                this.ctx.fillRect(x + TILE_SIZE - 4, y + 20, 4, TILE_SIZE - 20); // Right shadow
                this.ctx.fillRect(x, y + TILE_SIZE - 4, TILE_SIZE, 4); //Bottom shadow
                
                // Windows - upper floor
                this.ctx.fillStyle = '#2f1f0f'; // Dark brown for windows
                this.ctx.fillRect(x + 12, y + 24, 8, 8); // Left upper window
                this.ctx.fillRect(x + 28, y + 24, 8, 8); // Middle upper window  
                this.ctx.fillRect(x + 44, y + 24, 8, 8); // Right upper window
                
                // Windows - lower floor
                this.ctx.fillRect(x + 8, y + 40, 8, 8); // Left lower window
                this.ctx.fillRect(x + 24, y + 40, 8, 8); // Right lower window
                
                // Door
                this.ctx.fillStyle = '#2f1f0f'; // Same dark brown for door
                this.ctx.fillRect(x + 40, y + 36, 12, 16); // Door opening
                
                // Roof tiles/texture lines
                this.ctx.fillStyle = '#654321';
                this.ctx.fillRect(x - 2, y + 8, TILE_SIZE + 4, 2); //Roof line 1
                this.ctx.fillRect(x, y + 16, TILE_SIZE, 2); //Roof line 2
            }

           renderWater(x, y) {
 	`	this.ctx.fillStyle = '#4682b4';
		this.ctx.fillRect(x, y, this.TILE_SIZE, this.TILE_SIZE);
              
		// Water effects
		this.ctx.fillStyle = '#87ceeb';
              
		for (let i = 0; i < 3; i++) {
			this.ctx.fillRect(x + i * 8, y + 4, 6, 2);
			this.ctx.fillRect(x + i * 8 + 2, y + 16, 4, 2);
			this.ctx.fillRect(x + i * 8 + 4, y + 26, 6, 2);
			}
		}

           renderPlayer() {
		const x = this.player.x * this.TILE_SIZE;
            	const y = this.player.y * this.TILE_SIZE;
            
            	// Black outlines first (draw behind everything)
            	this.ctx.fillStyle = '#000000';
            
            	// Head outline
            	this.ctx.fillRect(x + 5, y + 3, 22, 18);
            	// Body outline  
            	this.ctx.fillRect(x + 7, y + 19, 18, 10);
            	// Leg outlines
		if (this.player.animFrame % 2 === 0) {
			this.ctx.fillRect(x + 9, y + 28, 6, 4); // Left leg
	                this.ctx.fillRect(x + 17, y + 28, 6, 4); // Right leg
		} else {
	                this.ctx.fillRect(x + 7, y + 28, 6, 4); // Left leg  
	                this.ctx.fillRect(x + 19, y + 28, 6, 4); // Right leg
            	}	
            
		// Cap (with outline)
		this.ctx.fillStyle = '#ff0000'; // Red cap like Ash
		this.ctx.fillRect(x + 6, y + 4, 20, 8);
            
            	// Cap visor
            	this.ctx.fillStyle = '#cc0000'; // Darker red for visor
            	this.ctx.fillRect(x + 6, y + 10, 20, 3);
            
            	// Face
            	this.ctx.fillStyle = '#ffdbac';
            	this.ctx.fillRect(x + 8, y + 8, 16, 12);
            
            	// Hair (showing under cap)
            	this.ctx.fillStyle = '#8b4513'; // Brown hair
            	this.ctx.fillRect(x + 7, y + 11, 2, 4);
            	this.ctx.fillRect(x + 23, y + 11, 2, 4);
            
            	// Eyes
            	this.ctx.fillStyle = '#000000';
            	this.ctx.fillRect(x + 11, y + 11, 2, 2); // Left eye
            	this.ctx.fillRect(x + 19, y + 11, 2, 2); // Right eye
            
            	// Nose (single pixel)
            	this.ctx.fillStyle = '#000000';
            	this.ctx.fillRect(x + 15, y + 14, 1, 1);
            
            	// Shirt
            	this.ctx.fillStyle = '#4169e1'; // Blue shirt
            	this.ctx.fillRect(x + 8, y + 20, 16, 8);
            
            	// Shirt shading
            	this.ctx.fillStyle = '#1e3a8a'; // Darker blue
            	this.ctx.fillRect(x + 8, y + 26, 16, 2);
            
            	// Arms
            	this.ctx.fillStyle = '#ffdbac'; // Skin tone
            	this.ctx.fillRect(x + 4, y + 22, 4, 6); // Left arm
            	this.ctx.fillRect(x + 24, y + 22, 4, 6); // Right arm
            
            	// Pants
            	this.ctx.fillStyle = '#2f4f4f'; // Dark pants
            	if (this.player.animFrame % 2 === 0) {
                	this.ctx.fillRect(x + 10, y + 29, 5, 3); // Left leg
                	this.ctx.fillRect(x + 18, y + 29, 5, 3); // Right leg
            	} else {
                	this.ctx.fillRect(x + 8, y + 29, 5, 3); // Left leg
                	this.ctx.fillRect(x + 20, y + 29, 5, 3); // Right leg
            	}
            
            	// Shoes
            	this.ctx.fillStyle = '#000000';
            	if (this.player.animFrame % 2 === 0) {
                	this.ctx.fillRect(x + 9, y + 31, 6, 1); // Left shoe
                	this.ctx.fillRect(x + 17, y + 31, 6, 1); // Right shoe
            	} else {
                	this.ctx.fillRect(x + 7, y + 31, 6, 1); // Left shoe
                	this.ctx.fillRect(x + 19, y + 31, 6, 1); // Right shoe
            	}
	}
```

### 6️⃣ **Coding Rules**
- Count each successful kanji submission only once.
- Character moves one tile at a time.
