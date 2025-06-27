## Project Title: **Kanjimon!**

### 1️⃣ **Core Concept**

Design a self-contained **retro 2D pixel-art game**, inspired by the visuals and vibe of early Pokémon (Game Boy Color era). The player explores a vibrant pixel world and captures **wild Kanji** by correctly identifying their English meanings. The goal: **capture all 25 target Kanji** scattered across the world.

📦 **Technical requirement:**
➡ Entire game in a single HTML file with embedded CSS + JavaScript (no external libraries).
➡ Uses `<canvas>` 2D rendering context.

---

### 2️⃣ **Visuals & Aesthetics**

🎨 **Overall style:**

* High-fidelity 8-bit pixel art, colorful and nostalgic.
* Mimic Pokémon’s classic Game Boy-style pixel art with that distinctive green monochrome palette and detailed tile patterns.
* Text uses **"Press Start 2P"** font everywhere for authentic retro flavor (embedded via Google Fonts or base64 in CSS).

👤 **Player character:**

* 20×20 pixel sprite representing a **human-like figure wearing a cap** (think: simplified Pokémon trainer).
* Palette: red for the cap, simple white shirt + pants contrast.
* Simple single-frame sprite with horizontal flip on left/right movement.

🌳 **Environment:**

* **Tile map:** 40×30 grid.
* Tile types:

  * `grass`: Noisy green pixel texture, speckled to feel alive.
  * `path`: Light brown / beige tiles with subtle dirt variation.
  * `trees`: Pixelated trees (8-bit style) sprinkled throughout the map to create a forest like environment — trees are chunky, round, classic RPG look, with deep green canopies and brown trunks.
* The map feels like a small, self-contained park or nature preserve, with a tic tac toe style path and grassy clearings.
* Occasional pixelated **flowers** (decorative only) for extra charm.

👾 **Wild Kanji sprites:**

* 16×16 pixel, blocky, mysterious black Kanji with abstract forms — Unown-inspired.
* Each Kanji has a subtle 2-pixel vertical bobbing animation to look as if floating or pulsing.
* Kanji are limited in grassy clearnings. 

🌌 **Battle screen:**

* Background: solid dark gray (#333 or similar).
* Centered enlarged Kanji sprite (5× scale).
* Pixel-art style input box + "Capture!" button below (styled to match retro UI).

🖋 **UI text & labels:**

* All text (including “Kanji Captured: X/25”, messages, buttons) uses **Press Start 2P** font.
* Light-colored text on dark backgrounds for readability.

---

### 3️⃣ **Game Mechanics & Flow**

#### 🚶 **State 1: OVERWORLD**

* Top Left overlay: `"Kanji Captured: X/25"` in Press Start 2P.
* Player moves tile-by-tile via arrow keys.
* Wild Kanji wander grass tiles randomly (1 tile move per second).
* Collision (same tile as a Kanji) triggers BATTLE state.

---

#### ⚔ **State 2: BATTLE**

* Enlarged Kanji sprite floats center stage.
* Below: retro-style input box + “Capture!” button.
* On correct entry → capture message, Kanji removed from map, return to OVERWORLD.
* On incorrect entry → error message, try again.

---

#### 🏆 **State 3: GAME\_OVER**

* Trigger: all 25 Kanji captured.
* Display: `"You're a Kanji Master! You've captured them all!"`
* Centered “Play Again” button reloads page.

---

### 4️⃣ **Game Data**

Your list of 25 **JLPT N5 Kanji** with primary meanings — placed randomly on grass at start:

```
一: one      二: two      三: three
四: four    五: five     六: six
七: seven   八: eight    九: nine
十: ten     人: person   日: sun (accept day)
月: moon (accept month) 火: fire
水: water   木: tree (accept wood)
金: gold (accept money) 土: earth (accept soil)
山: mountain 川: river
田: rice field 口: mouth
目: eye     手: hand     心: heart
```

---

### 5️⃣ **Exact Environment Description**

Imagine:
✅ A small, lush, pixel-art nature reserve — ringed with **pixelated trees** that form natural borders.
✅ A tic tac toe style grid of dirt interspersed with grassy fields, creating exploration zones.
✅ **Grass tiles** are filled with tiny pixel flecks, giving texture and life.
✅ One tree is exactly in the center.
✅ Decorative **flowers** or tiny rocks add visual richness.
✅ The world is compact (fits in a single screen or scrolls minimally), but feels vibrant and alive, just like classic Pokémon starting routes.
