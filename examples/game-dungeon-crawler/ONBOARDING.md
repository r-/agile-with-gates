# ONBOARDING.md
Project: Rune Depths – Dungeon Crawler
Owner: Sam L / Game Lead
Last updated: 2026-02-10

## 1) What is this project?
Rune Depths is a turn-based dungeon crawler where the player explores procedurally generated floors, fights enemies, collects loot, and tries to defeat the boss on floor 5 — all in a 10–15 minute session. Built as a web game (HTML5 Canvas + vanilla JS).

- Game design doc: `GDD.md`

## 2) Current status
- **Phase:** Building MVP
- **Milestone:** MS-01 — Playable MVP with 5 floors, 3 enemy types, loot, boss fight, permadeath
- **Sprint:** 01 — Core Grid & Movement (generation + player movement + enemy spawning) (see `/sprints/`)
- **Biggest open risk:** BSP generation might produce unplayable layouts on small grids

## 3) Team & roles
| Name | Role | Responsible for |
|------|------|----------------|
| Sam L | Game Lead | GDD, scope decisions, game balance |
| Avery R | Dev | Game loop, generation, combat system |
| Morgan P | Art / Audio | Sprites, SFX (post-MVP) |

## 4) Quick setup
### Prerequisites
- Any modern browser (Chrome, Firefox, or Safari)
- A text editor (VS Code recommended)
- (Optional) Node.js if you want a local server with hot reload

### Get running
```bash
# Clone the repo
git clone <repo-url>
cd rune-depths

# Run locally — no build step needed:
# Option A: double-click index.html
# Option B: use a local server
npx -y serve .
```

### Verify it works
- Open `http://localhost:3000` (or index.html directly)
- You should see the title screen
- Press Start — a procedurally generated floor appears
- Arrow keys move the player tile by tile
- Enemies should be visible on the grid

## 5) Project structure
```
rune-depths/
├── docs/
│   ├── GDD.md              # Game design — what & why
│   ├── RESEARCH.md          # Generation algorithms, combat formula research
│   ├── TDD.md               # Architecture, modules, test plan
│   ├── BACKLOG.md            # Prioritized work items
│   ├── ONBOARDING.md         # You are here
│   └── sprints/
│       └── SPRINT_01.md
├── index.html                # Entry point — canvas + HUD container
├── style.css                 # Layout + HUD styles
├── main.js                   # Game loop + state machine
├── floorGenerator.js         # BSP procedural floor generation
├── entityManager.js          # Entity registry (player, enemies, items)
├── combatSystem.js           # Turn-based combat resolution
├── renderer.js               # Canvas drawing (tiles, entities)
├── hud.js                    # DOM-based HUD (HP, floor, inventory)
└── inputHandler.js           # Keyboard input mapping
```

## 6) Key documents (reading order)
1. **This file** — you are here
2. **GDD.md** — understand the game (core loop, mechanics, content plan, game feel targets)
3. **TDD.md** — understand the architecture (modules, data flow, combat formula)
4. **BACKLOG.md** — see what's been done, what's next (BL-001 through BL-008)
5. **SPRINT_01.md** — see the current sprint scope and demo checklist

## 7) Conventions & rules
### Branching / version control
- `main` branch = always playable
- Feature branches: `feature/BL-XXX-short-description`
- Commit messages: `BL-XXX: short description` (e.g. `BL-004: add turn-based combat`)

### Code style
- Vanilla JavaScript (ES6+), no engine or framework
- camelCase for variables and functions, PascalCase for module/class names
- No external dependencies — everything runs in the browser
- Keep game logic separate from rendering (modules don't import renderer)

### Game-specific conventions
- All positions use `{ x, y }` grid coordinates (not pixel coordinates)
- Renderer converts grid → pixel using `TILE_SIZE` constant
- Entities have `{ id, type, pos, stats }` — no inheritance, plain objects
- Combat formula: `damage = attacker.atk - defender.def + rand(0..2)` (min 0)

### Documentation
- Gameplay decisions → GDD.md
- Technical decisions → TDD.md (section 9)
- Research → RESEARCH.md
- Tasks → BACKLOG.md
- Sprint work → /sprints/

### Definition of Done (project-level)
- Feature works in Chrome and Firefox
- No console errors
- Game runs at 60 FPS on a mid-range laptop
- Gameplay change is playtest-verified (even if just by the dev)

## 8) How to contribute
1. Check `BACKLOG.md` — find an unassigned P1 or P2 item
2. Create a feature branch: `feature/BL-XXX-title`
3. Implement the feature and check every box in the item's DoD
4. Playtest your change — does it feel right? Does it break existing gameplay?
5. Test in Chrome + Firefox
6. Push + open a PR against `main`
7. Demo the feature (screen recording is fine)

## 9) Useful links
- Repo: `<repo-url>`
- BSP Generation reference: https://roguebasin.com/index.php/Basic_BSP_Dungeon_generation
- Desktop Dungeons (inspiration): https://www.desktopdungeons.net/
- Live version: not yet deployed (planned for after Sprint 03)

## 10) FAQ / gotchas
- **Q: The floor looks weird / has dead ends — is that a bug?**
  A: Maybe. BSP should always generate connected rooms. If you find an unreachable area, it's a generation bug — file it as a BUG item in BACKLOG. The connectivity check in `floorGenerator.js` should catch these.

- **Q: Can I use a game engine (Phaser, Unity)?**
  A: Not for MVP. We chose vanilla Canvas to keep setup simple and learn the fundamentals. If the project grows to MS-02, we'll revisit (tracked in LATER section of BACKLOG).

- **Q: How do I tweak game balance (enemy stats, loot rates)?**
  A: All balance constants are in `main.js` at the top (ENEMY_STATS, LOOT_TABLE, FLOOR_SCALING). Change there and playtest. If you find better values, update GDD.md section 6 (Content plan) too.

- **Q: What controls does the player have?**
  A: Arrow keys = move, Space = pick up item, E = use item, I = toggle inventory, R = restart (on game over). See `inputHandler.js` for the full key map.
