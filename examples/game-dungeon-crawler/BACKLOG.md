# BACKLOG.md
Project: Rune Depths – Dungeon Crawler
Owner: Sam L / Game Lead
Last updated: 2026-02-08

## 1) Current milestone
**Milestone:** MS-01
**Milestone goal:** Deliver a playable MVP — 5 floors, 3 enemy types, boss fight, loot, permadeath.

**Scope rule:** MVP first. Everything else goes to Later/Icebox.

## 2) Active backlog (prioritized)
> ID format: BL-001, BL-002, ...

### P1 — Must (MVP)
#### BL-001 — Floor generation (BSP)
- Milestone: MS-01
- Outcome: Each floor is a grid with rooms, corridors, and guaranteed connectivity
- Notes: BSP algorithm. Min floor size 8×8, max 10×10. Floor size grows with depth.
- DoD:
  - [ ] Generates connected rooms + corridors
  - [ ] No isolated (unreachable) areas
  - [ ] Stairs placed in a room far from the player spawn
  - [ ] 3 runs produce 3 different layouts

#### BL-002 — Player movement (turn-based)
- Milestone: MS-01
- Outcome: Player moves one tile per arrow key press. Walls block movement.
- Notes: Movement consumes a turn. Enemies act after.
- DoD:
  - [ ] Arrow keys move player on the grid
  - [ ] Wall tiles block movement (no turn consumed)
  - [ ] Camera centers on player

#### BL-003 — Enemy spawning & AI
- Milestone: MS-01
- Outcome: Enemies spawn on each floor and move toward the player
- Notes: 3 types: slime (weak), skeleton (balanced), ghost (glass cannon). Simple AI: chase if within 3 tiles.
- DoD:
  - [ ] 2–5 enemies per floor (scales with floor number)
  - [ ] Enemies move toward player if within 3 tiles, else idle
  - [ ] Each type has distinct stats (ATK/DEF/HP)

#### BL-004 — Turn-based combat
- Milestone: MS-01
- Outcome: Walking into an enemy triggers combat. ATK − DEF + rand(0..2) damage.
- Notes: Player attacks by moving into enemy. Enemy retaliates on their turn.
- DoD:
  - [ ] Moving into enemy deals damage
  - [ ] Damage number pops up briefly
  - [ ] Enemy at 0 HP is removed + may drop loot
  - [ ] Player at 0 HP triggers Game Over

#### BL-005 — Loot & inventory
- Milestone: MS-01
- Outcome: Enemies/chests drop items. Player has 3 inventory slots.
- Notes: Items: health potion (+20 HP), sword (+ATK), shield (+DEF). Press E to use/equip.
- DoD:
  - [ ] Items appear on floor after enemy death
  - [ ] Walking over item + space picks it up (if inventory not full)
  - [ ] Health potion heals immediately when used
  - [ ] Weapon/shield modifies player stats while equipped

#### BL-006 — HUD (HP, floor, inventory)
- Milestone: MS-01
- Outcome: Player can see their HP, current floor, and inventory at all times
- Notes: DOM-based overlay on canvas
- DoD:
  - [ ] HP bar updates on damage/heal
  - [ ] Floor number updates on descent
  - [ ] Inventory slots show item icons/text

#### BL-007 — Boss fight (floor 5)
- Milestone: MS-01
- Outcome: Floor 5 has a boss enemy with higher stats. Defeating it wins the game.
- Notes: Boss = larger entity, 3× normal HP, unique attack pattern (hits harder)
- DoD:
  - [ ] Boss spawns on floor 5 (only)
  - [ ] Boss has visually distinct appearance
  - [ ] Defeating boss shows "You Win" screen
  - [ ] Boss is beatable with good loot from floors 1–4

#### BL-008 — Game Over & restart
- Milestone: MS-01
- Outcome: Dying shows Game Over screen. Player can restart instantly.
- Notes: Show floors cleared as score
- DoD:
  - [ ] Game Over screen appears on death
  - [ ] Shows "Floors cleared: X"
  - [ ] Press R or click Restart → new run from floor 1

### P2 — Should (if time)
#### BL-010 — Minimap
- Milestone: MS-01
- Outcome: Small minimap in corner showing explored tiles
- DoD:
  - [ ] Minimap renders in top-right corner
  - [ ] Only shows visited tiles
  - [ ] Updates on each move

#### BL-011 — Sound effects
- Milestone: MS-01
- Outcome: Audio feedback for attacks, pickups, stairs, and death
- DoD:
  - [ ] Attack: hit sound
  - [ ] Item pickup: chime
  - [ ] Stairs: descend sound
  - [ ] Death: game over jingle

### P3 — Could (nice to have)
#### BL-020 — Player classes
- Milestone: MS-02
- Outcome: Choose warrior (high DEF), rogue (high ATK), or mage (ranged)
- DoD:
  - [ ] Class select screen before run
  - [ ] Each class has distinct starting stats
  - [ ] Mage has 2-tile attack range

#### BL-021 — Pixel art tileset
- Milestone: MS-02
- Outcome: Replace colored rectangles with pixel art tiles and sprites
- DoD:
  - [ ] Tileset for floor, wall, stairs
  - [ ] Sprites for player, 3 enemies, boss
  - [ ] Item icons

## 3) Bugs (optional)
> No bugs yet — project has not shipped.

## 4) Tech debt / chores (time-boxed)
#### TD-001 — Set up project structure
- Milestone: MS-01
- Why: Need canvas, modules, and basic game loop before features
- DoD:
  - [ ] index.html + style.css + main.js created
  - [ ] Module files created (floorGenerator.js, combatSystem.js, entityManager.js, renderer.js, hud.js)
  - [ ] Canvas renders a colored background

#### TD-002 — Add basic state machine
- Milestone: MS-01
- Why: Need title/playing/gameover states before gameplay
- DoD:
  - [ ] Game states: title, playing, gameover, win
  - [ ] Transitions work (title → playing → gameover/win → title)

## 5) LATER (not now, but planned)
- Meta-progression (unlock items between runs) — reason: adds replayability, but MVP must prove core loop first
- Floor themes (cave, crypt, dungeon) — reason: visual variety, but gameplay first
- Fog of war — reason: adds exploration tension, but complicates MVP rendering

## 6) ICEBOX (ideas / maybe someday)
- Online leaderboard (fastest clear time) — why interesting: competition drives replays
- Daily challenge (seeded run) — why interesting: shared experience, community
- Co-op mode (two players, split keyboard) — why interesting: couch co-op is fun but doubles scope
