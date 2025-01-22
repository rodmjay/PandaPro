# PandaGame Requirements Document

## Overview
PandaGame is a turn-based, grid-based strategy game where players manage plants to strategically create space, trigger upgrades, and progress through levels. Players take precise actions to place or destroy plants while managing voids and leveraging snapping and triggered collapses for maximum efficiency.

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
   - **Effect**:
     - If the plant is part of a **2x2 block**, all **four cells** in the block are reset to `0` (empty), clearing the entire area.
     - If the plant is not part of a 2x2 block, only the selected cell is reset to `0`.
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
  ```
  Before Large Snap:
  1 | 1
  1 | 1
  After Large Snap:
  2 | 2
  2 | 2
  ```

### Small Snapping
- **Effect**: Only the **last planted cell** in the 2x2 block upgrades to the next higher number. The other three cells reset to `0`.
- **Example**:
  ```
  Before Small Snap:
  1 | 1
  1 | 1
  (Last planted cell: bottom-right)
  After Small Snap:
  0 | 0
  0 | 2
  ```

---

## Triggered Collapses
A **triggered collapse** occurs when snapping creates a chain reaction, potentially forming larger-than-2x2 blocks.

### Resolving Larger Blocks
1. **Break Into Sub-Blocks**:
   - Larger blocks are divided into distinct **2x2 sub-blocks**.
   - Sub-blocks are resolved based on **priority rules**:
     - **Top-Left Priority**: Start from the top-left and resolve left-to-right, top-to-bottom.

2. **Cascading**:
   - If resolving a larger block creates new valid 2x2 blocks, these are processed recursively.
   - Cascading continues until no further 2x2 blocks are formed.

### Voids in Collapses
- Voids prevent snapping within larger blocks, splitting them into smaller, resolvable parts.
- **Example**:
  ```
  Before Collapse with Voids:
  1 | 1 | 1
  1 | V | 1
  1 | 1 | 1

  After Collapse:
  2 | 2 | 1
  2 | V | 1
  1 | 1 | 1
  ```

---

## Configurable Gameplay Settings

### Snapping Configuration
1. **Snapping Type**:
   - Large Snapping (all four cells upgrade).
   - Small Snapping (only the last planted cell upgrades).
2. **Cascading Depth**:
   - Limit the maximum depth of cascades (e.g., 3).
3. **Trigger Rules**:
   - Always enabled or condition-based (e.g., score thresholds).

### Grid Setup
1. **Grid Size**:
   - Default: 8x8.
   - Adjustable for advanced levels (e.g., 10x10).
2. **Initial Layout**:
   - Define starting plants, voids, and blocked cells.

### Voids
1. **Static Voids**:
   - Fixed void positions that never change.
2. **Dynamic Voids**:
   - Voids can move or expand based on game events.

### Scoring
1. **Snapping Rewards**:
   - Large Snap: Higher points for upgrading all cells.
   - Small Snap: Bonus for strategic placement.
2. **Cascading Bonuses**:
   - Exponential score increases for deeper cascades.
3. **Destruction Penalty**:
   - Deduct points for destroying plants.

---

## Visual Feedback
1. **Highlight Snapping Areas**:
   - Glow effects for Large and Small Snapping.
2. **Cascade Animation**:
   - Ripple effects to indicate triggered collapses.
3. **Voids**:
   - Unique sprites for voids to differentiate them from other cells.

---

## Level Design Flexibility
1. **Dynamic Challenges**:
   - Time limits, move limits, or special goals (e.g., clear X voids).
2. **Snapping as a Tool**:
   - Use Large or Small Snapping selectively to adjust difficulty.
3. **Progression**:
   - Early levels: Small Snapping, minimal voids.
   - Advanced levels: Large Snapping, dynamic voids, tighter space.

