# GDD.md
Project: Rune Depths – Dungeon Crawler
Owner: Sam L / Game Lead
Status: active
Last updated: 2026-02-08

## 1) Summary
- What we're building: A turn-based dungeon crawler where the player explores procedurally generated floors, fights enemies, collects loot, and tries to reach the deepest level.
- Genre / platform: 2D top-down turn-based roguelite, PC (web build for MVP)
- For who: Players who enjoy quick-session roguelites with simple mechanics and strategic depth.
- Why now: We want a small-scope game to practice the full dev cycle — from GDD to release.
- Success looks like:
  - A playable 5-floor dungeon with 3 enemy types and a boss
  - Average play session 10–15 minutes
  - 5 playtesters complete a full run and give feedback

## 2) Problem & players
### Problem statement
Many roguelites require long time commitments and complex builds. We want a pick-up-and-play dungeon crawler that delivers satisfying exploration and combat in short sessions.

### Target players
- Primary: Casual gamers who like roguelites but have limited time (15 min sessions)
- Secondary: Students learning game development who want a clear reference project

### Context / play scenarios
- Lunch break gaming: play a full run in 10–15 minutes
- Commute play: clear progress in a short session (web version on laptop)
- "One more run" loop: death feels fair and restart is instant

## 3) Core gameplay
### Core loop
1. Enter floor → 2. Explore rooms (move tile by tile) → 3. Fight enemies (turn-based) → 4. Collect loot / heal → 5. Find stairs → go deeper → repeat

### Key mechanics
- **Turn-based movement**: Player moves one tile per turn. Enemies move after the player.
- **Simple combat**: Attack, defend, or use item. Damage = ATK − DEF with randomness.
- **Loot drops**: Enemies and chests drop health potions, weapons (+ATK), shields (+DEF).
- **Permadeath**: When HP = 0, the run ends. Start from floor 1.

### Progression
- Each floor is harder (more enemies, higher stats)
- Loot scales with floor depth
- Boss on floor 5 — beating the boss = winning

### Win / lose conditions
- Win: Defeat the floor 5 boss
- Lose: HP reaches 0 on any floor

## 4) Goals & non-goals
### Goals
- G1: Deliver a fun 10–15 minute roguelite run with clear risk/reward choices
- G2: Procedurally generate floor layouts so each run feels different
- G3: Make combat feel snappy — no unnecessary animations or delays

### Non-goals
- NG1: No persistent meta-progression (unlocks between runs) in MVP
- NG2: No multiplayer or online features
- NG3: No story or dialogue — pure gameplay
- NG4: No mobile touch controls

## 5) Scope (MVP)
### MVP: must-have
- Procedural floor generation (5 floors, grid-based)
- Player movement (arrow keys, turn-based)
- 3 enemy types with different stats (slime, skeleton, ghost)
- Turn-based combat (attack / defend / use item)
- Loot: health potions, swords (+ATK), shields (+DEF)
- Boss fight on floor 5
- Permadeath + instant restart
- Simple HUD: HP bar, floor number, inventory (3 slots)

### Should-have (if time)
- Minimap of explored areas
- Sound effects for attacks, pickups, and stairs
- Floor transition animation

### Could-have (nice to have)
- Multiple player classes (warrior, rogue, mage)
- Leaderboard (best floor reached, fastest run)
- Pixel art tileset (vs colored rectangles in MVP)

## 6) Content plan (MVP)
- Levels / maps: 5 procedurally generated floors (7×7 to 10×10 grid)
- Enemies / obstacles: 3 types (slime: low ATK/DEF, skeleton: balanced, ghost: high ATK/low DEF) + 1 boss
- Items / power-ups: Health potion (+20 HP), Iron Sword (+3 ATK), Wooden Shield (+2 DEF), Hero Blade (+5 ATK, boss-floor only)
- Audio: MVP uses browser beeps or no audio — SFX in should-have

## 7) Requirements (acceptance-level)
- R1: Floors are randomly generated each run
  Acceptance: Play 3 runs → no two floors have identical layouts

- R2: Combat resolves correctly
  Acceptance: ATK 10 vs DEF 5 → damage = 5 (±1 randomness). Player can die. Enemies can die.

- R3: Permadeath works
  Acceptance: Player dies → "Game Over" screen → click "Restart" → new run from floor 1

- R4: Boss is beatable
  Acceptance: A careful player with loot from floors 1–4 can defeat the boss in 3–5 turns

## 8) UX / flows (lightweight)
- Main flow: Title screen → Start → Floor 1 → … → Floor 5 boss → Win screen / Game Over → Restart
- Edge cases:
  - Player has full inventory and walks over loot → "Inventory full" message, item stays
  - Player tries to move into a wall → nothing happens (no turn consumed)
- Notes / constraints:
  - Keyboard-only controls for MVP (arrow keys + E for interact + I for inventory)

## 9) Game feel targets
- Turns should resolve instantly — no slow animations
- Camera follows player (centered)
- Enemy deaths: simple flash + disappear
- Damage numbers: pop above target for 0.5 s
- Inspiration: Brogue, Desktop Dungeons, Into the Breach (snappy, clear feedback)

## 10) Success metrics
- Metric: Playtest completion rate — Target: 4 of 5 testers complete a full run
- Metric: "Fun" rating — Target: avg 7/10 in post-play survey
- Metric: Average session length — Target: 10–15 minutes

## 11) Risks & assumptions
- Risk: Procedural generation creates unwinnable floors (e.g. blocked paths) — Mitigation: validate floor connectivity during generation
- Risk: Combat is too simple / boring — Mitigation: playtest early and add an item or enemy type if needed
- Assumption: Turn-based is enough for engagement (no real-time needed) — How to validate: playtest by sprint 2

## 12) Decisions (product-level)
- [2026-01-20] Web build (HTML/JS Canvas) for MVP — Why: easiest distribution for playtesting — Impact: no native features
- [2026-01-25] Permadeath only, no meta-progression — Why: keep MVP scope small — Impact: replayability relies on generation variety
- [2026-02-05] 5 floors, not 10 — Why: 10 floors made sessions too long (25+ min) — Impact: need to tune loot/difficulty for shorter run

## 13) Links
- Research: `RESEARCH.md`
- Technical design: `TDD.md`
- Plan: `BACKLOG.md` + `/sprints/`
