# 🎮 Minecraft-Inspired 3D Web Game

A fully playable, browser-based voxel game inspired by Minecraft, built with **Three.js** — no external assets required.

## ✨ Features
- **Procedural terrain generation** (Simplex noise) with 7 biomes: plains, forest, mountain, desert, snow tundra, swamp, cave
- **Chunk-based infinite world** (16×16 chunks, seamless loading/unloading)
- **First-person controller**: WASD + Space jump, Shift sprint, Ctrl crouch-slide
- **Building system**: 18+ block types, place/remove with mouse, undo/redo (50 actions), save/load
- **Mining & tools** with tiered durability (wooden → diamond)
- **Crafting table** with 3×3 grid and recipes for tools/blocks/potions
- **Mobs**: passive (cow, pig, sheep, chicken) + hostile (zombie, skeleton, creeper) with AI pathfinding & night spawning
- **Survival**: health hearts, hunger bar, day/night cycle (24 min), weather (rain/thunder)
- **Inventory UI**: 9-slot hotbar + 27-slot chest, drag-and-drop, crafting GUI
- **Achievement system** tracking milestones
- **Modding framework** via JSON config files for custom blocks/mobs
- **Mini-game mode**: Parkour course generator
- **Unique mechanic: Elemental Affinity** — placing blocks of matching biome type grants temporary buffs
- **Windows Desktop shortcut** instructions included below

## 📁 Project Structure
```
minecraft-3d-webgame/
├── index.html              # Entry point / HTML shell
├── package.json            # npm dependencies (three.js only)
├── src/
│   ├── main.js             # Bootstrap & game loop
│   ├── core/
│   │   ├── Engine.js       # Renderer, scene, camera, lighting
│   │   ├── GameLoop.js     # Fixed-timestep update + render
│   │   ├── InputManager.js # Keyboard/mouse/touch input
│   │   └── SaveSystem.js    # localStorage world persistence
│   ├── world/
│   │   ├── Noise.js        # Simplex noise implementation
│   │   ├── Biome.js         # 7 biomes with palettes & vegetation
│   │   ├── ChunkManager.js  # 16×16 chunk load/unload system
│   │   ├── TerrainGenerator.js# Height + cave generation (diamond noise)
│   │   └── BlockRegistry.js # All block definitions (18+)
│   ├── player/
│   │   ├── Player.js        # FPS controller, physics, collision
│   │   ├── Inventory.js     # Hotbar + chest inventory, drag/drop
│   │   └── SurvivalStats.js # Health, hunger, XP, temperature
│   ├── systems/
│   │   ├── CraftingSystem.js# 3×3 grid + recipe book
│   │   ├── MobSpawner.js    # Night spawning by biome/time
│   │   ├── MobAI.js         # Pathfinding, attack patterns, breeding
│   │   ├── WeatherSystem.js # Rain/thunder/clear
│   │   ├── DayNightCycle.js # 24-min cycle with lighting lerp
│   │   └── AchievementTracker.js# Milestone detection & toasts
│   ├── ui/
│   │   ├── HUD.js           # Health/hunger/XP bars, crosshair, tooltip
│   │   ├── InventoryUI.js    # Hotbar + chest GUI (DOM overlay)
│   │   └── CraftingGUI.js    # 3×3 crafting table UI
│   └── modding/
│       └── ModLoader.js     # JSON config for custom blocks/mobs
├── mods/
│   ├── example_blocks.json  # Sample mod: new block definitions
│   └── example_mobs.json    # Sample mod: new mob definitions
└── tools/
    └── create-desktop-shortcut.html  # Windows desktop shortcut helper
```

## 🚀 Installation & Running

### Option A — Local dev server (recommended)
```bash
cd minecraft-3d-webgame
npm install
npx http-server . -p 8080
# Open http://localhost:8080 in your browser
```

### Option B — Python HTTP server
```bash
python3 -m http.server 8080
```

### Option C — Windows Desktop Shortcut (Easy Access)
To make this game easily accessible from your **Windows desktop**:
1. Run the dev server: `npm install && npx http-server . -p 8080`
2. Right-click on an empty area of your desktop → **New → Shortcut**
3. In "Location", paste: `http://localhost:8080`
4. Give it a name like `Minecraft Web Game` and click Finish
5. Optionally, set the icon to a custom one

> **Note**: The server must be running for the shortcut to work.
> You can run it as a background process or use `npm start` in a terminal window.

## 🎮 Controls
| Key | Action |
|-----|--------|
| W A S D | Move |
| Mouse | Look around |
| Space | Jump |
| Shift | Sprint |
| Ctrl | Crouch / Slide |
| Left Click (hold) | Break block |
| Right Click | Place block |
| E | Toggle inventory |
| Q | Open crafting table |
| 1-9 | Select hotbar slot |
| R | Undo, T | Redo |
| F5 | Save world |
| F6 | Load world |
| P | Parkour mini-game mode |
| Esc | Pause / Menu |

## 🧪 Modding Framework
Place JSON files in the `mods/` directory to add custom blocks and mobs:

### Custom Block Example (`mods/my_block.json`)
```json
{
  "id": "my_wood",
  "name": "Mystery Wood",
  "color": [0.6, 0.4, 0.2],
  "hardness": 3,
  "tool": "axe",
  "drops": [{"item": "mystery_planks", "count": 1}],
  "biomeAffinity": ["forest"]
}
```

### Custom Mob Example (`mods/my_mob.json`)
```json
{
  "id": "my_creature",
  "name": "Mystery Creature",
  "type": "passive",
  "color": [0.8, 0.6, 0.1],
  "speed": 2.5,
  "health": 10,
  "spawnBiomes": ["plains", "forest"],
  "breedItem": "wheat"
}
```

## ⚠️ Known Limitations
- No multiplayer (would require a separate backend server)
- Textures are procedurally generated (colored faces, not full texture maps) — keeps bundle size tiny
- Mob AI is simplified state-machine pathfinding (not full A* on large maps)
- Mobile touch controls are basic (virtual joystick + tap-to-place)
- Performance: ~60 FPS on mid-range hardware with 12×12 chunks visible; adjust via `CHUNK_RADIUS` in Engine.js

## 🏆 Unique Mechanics
1. **Elemental Affinity**: Placing a block whose material matches the current biome grants a temporary buff (e.g., placing snow in tundra = cold resistance, placing sand in desert = heat resistance). Buffs last 30 seconds.
2. **Parkour Mini-Game Mode**: Press `P` to generate a procedurally-built parkour course above your position — timed jumps over gaps with increasing difficulty tiers.
3. **Achievement Toasts**: Unlocking milestones (first block placed, first mob killed, full inventory, survived 1 day, etc.) shows an animated toast notification.

## 📝 License
MIT — see LICENSE file.