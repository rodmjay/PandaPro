# PandaGame Gameplay Mechanics

## Overview
PandaGame is a turn-based grid-based strategy game where players manage plants to strategically create space and upgrade plants through snapping and triggered collapses. The game supports dynamic levels with customizable mechanics for snapping, collapsing, and void interactions.

---

## Game Board
- **Grid Size**: 8x8 by default.
- **Base Cells**:
  - Cells start as `0` (empty).
  - Numbers (`1`, `2`, `3`, etc.) represent plants at different growth stages.
  - Voids are obstacles where plants cannot be placed.

---

## Player Actions
1. **Place a Plant**:
   - Place the **next plant** (visible at the top middle) into any single **empty cell** (`0`).
   - Plants cannot overwrite existing plants or be placed on voids.

2. **Destroy a Plant**:
   - Remove an existing plant from the grid.
   - The destroyed plant’s cell resets to `0` (empty), freeing up space.
   - **Rules**:
     - Players can destroy only one plant per turn.
     - Destruction may have penalties (e.g., score deduction).

3. **Turn Structure**:
   - Players must take exactly one action per turn:
     - Place the next plant, OR
     - Destroy one existing plant.

---

## Snapping Mechanics
Snapping resolves when a valid **2x2 block** of the same number is formed. Two snapping types determine the outcome:

### Large Snapping
- **Effect**: All four cells in the 2x2 block upgrade to the next higher number.
- **Example**:
