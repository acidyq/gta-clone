# Core Architecture & World Generation

Sunset City is a top-down, micro-sandbox game modeled after early Grand Theft Auto titles. It is built entirely as a single-file HTML5 web application (`index.html`), utilizing vanilla JavaScript and the Canvas 2D API without any external dependencies or game engines.

## Core Architecture

The game runs in a classic `requestAnimationFrame` loop and separates its logic into three primary phases:
- **Input Handling**: Capturing keyboard events (WASD, arrows, modifiers).
- **Update (Logic)**: Fixed-step delta-time (`dt`) updates for all entities, collision resolution, and state changes.
- **Render**: Drawing the world grid, entities, particles, UI, and applying visual effects.

Variables are largely kept in the global scope to reduce boilerplate, typical for a micro-prototype.

## World Generation

The game world is generated procedurally upon initialization:
- **Grid System**: The world is structured as a 7x7 grid (`NB=7`) of blocks. Each block is 560x560 pixels (`CELL=560`), separated by 140-pixel wide roads (`ROAD=140`). Total world size is 4060x4060 pixels.
- **Block Types**: 
  - **Buildings**: Contain procedural rectangular structures with varying heights, colors, roof props, and trees.
  - **Parks**: Open areas with grass, trees, and occasionally a pond.
  - **Parking Lots**: Open areas where parked cars are spawned.
- **Collision Data**: World objects like buildings and ponds provide a hit-test function `hitBuilding(x, y, r)` that entities use for circle-vs-rectangle and circle-vs-circle collision resolution.
