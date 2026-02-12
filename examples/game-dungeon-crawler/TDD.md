# TDD.md
Project: Rune Depths – Dungeon Crawler
Owner: Sam L / Game Lead
Status: active
Last updated: 2026-02-05
Related milestone: MS-01 (MVP)

## 1) Summary
- What this builds (from GDD): A turn-based dungeon crawler with procedural generation, grid movement, combat, loot, and a boss fight.
- Technical approach in one sentence: HTML5 Canvas with vanilla JS — a game loop processes turns, BSP generates floors, and a simple ECS-like pattern manages entities (player, enemies, items).
- Key constraints: Web-only (no native), keyboard controls, no external game engine, 60 FPS render target.

## 2) Architecture (big picture)
### Modules / boundaries
- **Game** — responsibility: game loop, state machine (title / playing / gameover / win) — API: `start()`, `restart()`
- **FloorGenerator** — responsibility: BSP-based procedural floor creation — API: `generate(width, height, floor) → FloorData`
- **EntityManager** — responsibility: create/destroy/query entities (player, enemies, items) — API: `spawn(type, pos)`, `getAt(pos)`, `remove(id)`
- **CombatSystem** — responsibility: resolve attacks — API: `resolve(attacker, defender) → CombatResult`
- **InputHandler** — responsibility: capture arrow keys + action keys — API: `onInput(callback)`
- **Renderer** — responsibility: draw floor, entities, HUD to canvas — API: `draw(state)`
- **HUD** — responsibility: render HP bar, floor number, inventory overlay — API: `update(playerState)`

### Data ownership
- Game owns global state (current floor, game phase)
- EntityManager owns all entity instances
- FloorGenerator produces FloorData (tiles + spawn points) but doesn't own it after creation
- No entity stores reference to another entity — queries go through EntityManager

### Event / flow (if relevant)
- InputHandler captures key → Game processes turn → EntityManager moves player → if enemy at target: CombatSystem resolves → if stairs: FloorGenerator generates next floor → Renderer draws

## 3) Core components
- Component: FloorGenerator — Purpose: create grid-based floors with rooms, corridors, enemy spawn points, item spawns, and staircase
- Component: CombatSystem — Purpose: resolve attack/defend actions using ATK − DEF + rand(0..2) formula
- Component: EntityManager — Purpose: central registry of all game entities with position queries
- Component: Renderer — Purpose: tile-based canvas rendering (floor tiles, entities, fog of war optional)
- Component: HUD — Purpose: DOM-based overlay for HP, floor number, inventory

## 4) Public contracts
- Contract: `FloorGenerator.generate(width, height, floorNum)`
  - Input: grid dimensions + floor number (for difficulty scaling)
  - Output: `{ tiles: 2D array, spawnPoints: { player, enemies[], items[], stairs } }`

- Contract: `CombatSystem.resolve(attacker, defender)`
  - Input: two entities with `{ atk, def, hp }` stats
  - Output: `{ damage, defenderHP, defeated: bool }`

- Contract: `EntityManager.spawn(type, pos)`
  - Input: entity type string + `{ x, y }` position
  - Output: entity ID

## 5) Key scenarios
### Scenario A: Player moves and explores
1. Player presses → (right arrow)
2. Game checks target tile — is it walkable? Yes → move player
3. Enemies take their turn (simple AI: move toward player if within 3 tiles, else idle)
4. Renderer redraws floor with new positions

### Scenario B: Player attacks enemy
1. Player moves into enemy tile → triggers combat
2. CombatSystem.resolve(player, enemy) → damage = player.atk − enemy.def + rand(0..2)
3. Enemy HP reduced — if 0: enemy defeated, loot dropped
4. If enemy survives: enemy retaliates on their turn

### Scenario C: Player finds stairs
1. Player steps on stairs tile
2. Game increments floor counter
3. If floor > 5: boss defeated screen (win)
4. Else: FloorGenerator.generate() for next floor → EntityManager clears + respawns

### Scenario D: Player dies
1. Enemy attack reduces player HP to 0
2. Game state → "gameover"
3. Renderer shows Game Over screen + score (floors cleared)
4. Player presses "R" → Game.restart()

## 6) Risks & mitigations
- Risk: BSP generates disconnected rooms on small grids — Mitigation: connectivity check after generation, regenerate if isolated rooms exist
- Risk: Canvas rendering too slow with many entities — Mitigation: max 15 entities per floor, only redraw changed tiles
- Risk: Turn-based loop feels laggy — Mitigation: all turns resolve in same frame, no await/animation blocking game loop

## 7) Testing plan (minimal)
- Unit: FloorGenerator connectivity (no isolated rooms), CombatSystem damage formula (edge cases: 0 DEF, equal ATK/DEF), EntityManager spawn/remove/query
- Integration: full turn sequence (input → move → combat → loot → render call)
- E2E: manual playthrough — reach floor 5 and defeat boss
- Smoke test:
  1. Open index.html
  2. Press Start — floor 1 generates, player visible
  3. Move around — enemies visible and react
  4. Attack an enemy — damage numbers appear, enemy can die
  5. Find stairs — next floor loads

## 8) Performance / constraints (if needed)
- Target: 60 FPS render, instant turn resolution
- Canvas size: 640×640 px (scales with CSS)
- Max entities per floor: 15 (player + enemies + items)
- No external dependencies — vanilla JS only

## 9) Decisions (technical)
- [2026-01-22] Canvas over DOM for game rendering — Why: tile-based drawing is faster and simpler on canvas — Impact: HUD stays DOM-based for easy text
- [2026-01-28] BSP over random walk for generation — Why: better room structure for item/enemy placement — Impact: slightly more complex generation code
- [2026-02-05] No ECS library — simple objects with type/stats/pos — Why: keep it minimal for MVP — Impact: refactor to proper ECS if scope grows

## 10) Optional splits (only if TDD gets too big)
- `DESIGN.md` — could document tile sizes, color palette, and HUD layout if the team grows
- `ART_BIBLE.md` — not needed for MVP (colored rectangles)

## 11) Links
- Game design: `GDD.md`
- Research notes: `RESEARCH.md`
- Plan: `BACKLOG.md` + `/sprints/`
