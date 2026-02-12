# RESEARCH.md
Project: Rune Depths – Dungeon Crawler
Owner: Sam L / Game Lead
Last updated: 2026-01-28

## 1) Purpose
This is the **research scratchpad**: links + notes + comparisons + spike results.
Conclusions should be copied into:
- `GDD.md` (gameplay scope/decisions)
- `TDD.md` (technical choices/design)

## 2) Questions we're answering
- Q1: What procedural generation algorithm works best for small grid-based dungeons?
- Q2: How should turn-based combat feel in a web-based game (JS + Canvas)?
- Q3: How do similar roguelites balance loot and difficulty across floors?

## 3) What we found (copy-ready)
- BSP (Binary Space Partitioning) generates clean room-and-corridor layouts on small grids → Impacts: TDD (generation module) → Evidence: §6 source #1
- Simple ATK − DEF + random(0..2) formula keeps combat snappy and predictable → Impacts: GDD (R2 acceptance) → Evidence: §5 spike #1
- Desktop Dungeons scales enemy HP by floor × 1.5 and ATK by floor × 1.2 — feels fair for short runs → Impacts: GDD (balance tuning) → Evidence: §6 source #3

## 4) Options (only if needed)
### A) BSP dungeon generation
- Pros: guarantees connected rooms, no isolated areas, clean corridors
- Cons: rooms can feel rectangular and repetitive
- Risks: need to validate min room size on small grids (7×7)

### B) Drunkard's Walk (random walk)
- Pros: organic cave-like layouts, simple to implement
- Cons: no guaranteed room structure, hard to place items/enemies meaningfully
- Risks: might create too-open layouts without tactical cover

**Recommendation:** A (BSP) — room structure gives better item/enemy placement and corridor chokepoints add tactics.

## 5) Spikes / experiments (only if done)
- Spike: Combat formula prototype — Goal: test ATK−DEF+rand(0..2) in 50 simulated fights — Result: player wins ~70 % of balanced fights, feels fair — Next: implement in combat module
- Spike: BSP on 7×7 grid — Goal: test if BSP works on small grids — Result: minimum 2 rooms + 1 corridor at 7×7, works fine at 10×10 — Next: use 8×8 as minimum floor size

## 6) Sources & notes
- BSP Dungeon Generation tutorial — https://roguebasin.com/index.php/Basic_BSP_Dungeon_generation
  - Clear algorithm, works well for grid-based games
  - Can enforce min/max room sizes
- Procedural Content Generation Wiki — https://pcg.wikidot.com/pcg-algorithm:dungeon-generation
  - Good comparison of BSP vs cellular automata vs random walk
- Desktop Dungeons postmortem — https://www.gamedeveloper.com/design/desktop-dungeons
  - Scaling formula: enemy HP = base × (1 + 0.5 × floor), ATK = base × (1 + 0.2 × floor)
  - Short runs (10–15 min) work when each decision matters

## 7) Open questions / next steps
- How many items per floor feels right? → Next: playtest in sprint 2 (start with 2–3 per floor)
- Should rooms have "themes" (enemy-heavy, loot-heavy, empty)? → Next: consider for should-have after MVP
