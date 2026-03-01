# Agile with Gates - Document Templates

A lightweight, copy-and-use template kit for running product development with the **agile-with-gates** method — combining sprint-based delivery with clear decision points (gates) to keep projects on track.

These templates work for **apps, games, services, and any product** you want to take from idea to launch.

---

## Why this exists

Most project documentation is either too heavy (100-page specs nobody reads) or too informal (sticky notes that vanish after standup). This kit sits in the sweet spot:

- **Structured enough** to keep everyone aligned on _what_, _why_, and _how_
- **Lightweight enough** to actually maintain throughout the project
- **Gate-driven** so you stop, check, and decide before committing more time

The underlying philosophy: **steps are the map, sprints are the engine, gates are the brakes.**

---

## The process at a glance

```
Problem → Concept → Research → MVP Scope → Design → Build/Test → Release → Launch → Improve
```

| Step | What you do | Key document | Gate? |
|------|------------|--------------|-------|
| 1. Problem & users | Define the problem and who has it | PRD / GDD | — |
| 2. Concept | Describe the solution + list assumptions | PRD / GDD | **Gate A** ✓ |
| 3. Research | Reduce uncertainty (compare, spike, test) | RESEARCH | — |
| 4. MVP scope | Define must/should/could + non-goals | PRD / GDD + BACKLOG | **Gate B** ✓ |
| 5. Design | UX flows + system architecture + test strategy | TDD | — |
| 6. Build & test | Sprint-based delivery with demo + retro | /sprints/ | — |
| 7. Release | Smoke test → user testing | Sprint doc | **Gate C** ✓ |
| 8. Launch | Ship to real users, collect data | BACKLOG (updated) | — |
| 9. Improve | Prioritize next iteration from feedback | BACKLOG + /sprints/ | — |

### Gates (decision points)

Gates protect you from scope creep and bad assumptions:

- **Gate A** — _Ready to research?_ Problem is clear, concept can be pitched in 30 seconds, assumptions are written down.
- **Gate B** — _Ready to build?_ MVP scope is defined and bounded, P1 items have clear DoD, risks have a plan.
- **Gate C** — _Ready to launch?_ MVP acceptance is met, core flow is stable, success metrics are defined.

At each gate: **go / adjust / stop.**

---

## Testing workflow (fast teams)

This template kit supports two common testing styles. Pick one per project (or per milestone) and be consistent.

### Style A — Continuous verification (classic TDD)
- tests are written early
- tests are run frequently during implementation
- failures are fixed immediately

### Style B — Batch verification (fast iteration)
For very fast teams, it can be more efficient to:
- **plan tests at the start**
- **implement quickly**
- run a focused **Test Phase** near the end of the sprint (or at the milestone gate)

If you use batch verification, define a **Test Phase Gate** in each sprint doc:

**Test Phase Gate (must be green before closing sprint/milestone)**
- planned tests exist (from sprint tasks)
- full test suite is green (or agreed subset)
- demo/smoke is green
- failures are mapped to tasks and resolved (or explicitly deferred)

---

## Templates included

```
templates/
├── ONBOARDING.md               # New dev? Start here (setup, structure, conventions)
├── PRD.md                      # Product Requirements Document (apps, services)
├── GDD.md                      # Game Design Document (games)
├── RESEARCH.md                 # Research scratchpad (links, comparisons, spikes)
├── TDD.md                      # Technical Design Document (architecture + test plan)
├── BACKLOG.md                  # Prioritized work items with DoD
└── sprints/
    └── SPRINT_TEMPLATE.md      # Sprint scope, tasks, test phase gate, demo, retro
```

### What goes where

| Information | Document |
|------------|----------|
| New dev setup, structure, conventions | **ONBOARDING.md** |
| Problem, goals, MVP scope, non-goals | **PRD.md** or **GDD.md** |
| Links, comparisons, spike results | **RESEARCH.md** |
| Architecture, modules, contracts, test plan | **TDD.md** |
| Prioritized work items with DoD | **BACKLOG.md** |
| Sprint scope, tasks, demo, retro | **/sprints/SPRINT_NN.md** |

### PRD vs GDD — which one?

- Use **PRD.md** for apps, services, tools, and most products.
- Use **GDD.md** for games — it adds sections for core loop, mechanics, progression, content plan, and game feel.

Both serve the same purpose: define _what_ and _why_. The GDD just speaks the language of game development.

---

## How to use

### 1. Copy the templates

Copy the `templates/` folder into your project root and rename it `docs/` (or keep it as-is — whatever fits your workflow):

```
my-project/
├── docs/
│   ├── ONBOARDING.md   # New dev? Start here
│   ├── PRD.md          # or GDD.md for games
│   ├── RESEARCH.md
│   ├── TDD.md
│   ├── BACKLOG.md
│   └── sprints/
│       └── SPRINT_01.md
├── src/
└── ...
```

### 2. Fill in the templates

Work through them in order:

1. **PRD/GDD** — Start here. Define the problem, users, concept, and scope.
2. **RESEARCH** — Capture your research as you go. Conclusions feed back into PRD/GDD and TDD.
3. **TDD** — Design the technical approach once the scope is clear.
4. **BACKLOG** — Break the MVP into buildable items with clear DoD.
5. **SPRINT_01** — Pick items from the backlog, set a goal, and start building.
6. **ONBOARDING** — Fill this in so the next person who joins can get up to speed fast.

### 3. Use the gates

Before moving to the next phase, check the gate criteria:

- **Gate A** (after concept): Can you pitch it in 30 seconds? Are assumptions written down?
- **Gate B** (after MVP scope): Is the scope bounded? Do P1 items have DoD?
- **Gate C** (before launch): Does the core flow work? Are success metrics defined?

### 4. Repeat sprints

After each sprint:
- Demo what works
- Run a retro (what went well / what was painful / actions)
- Update the backlog
- Create the next sprint document

---

## Examples

Two fully filled-in examples are included to show how the templates look in practice:

### 📱 App example: Weather Dashboard

A single-page weather app with search, 5-day forecast, and clothing suggestions.

→ [`examples/app-weather-dashboard/`](examples/app-weather-dashboard/)

Uses: **PRD.md** · RESEARCH.md · TDD.md · BACKLOG.md · ONBOARDING.md · Sprint 01

### 🎮 Game example: Dungeon Crawler

A turn-based roguelite with procedural floors, combat, loot, and a boss fight.

→ [`examples/game-dungeon-crawler/`](examples/game-dungeon-crawler/)

Uses: **GDD.md** · RESEARCH.md · TDD.md · BACKLOG.md · ONBOARDING.md · Sprint 01

---

## Key concepts

| Term | Meaning |
|------|---------|
| **Agile-with-gates** | Sprints for delivery + gates for decision-making |
| **MVP** | Minimum Viable Product — smallest version you can test with real users |
| **Scope** | What's included in a delivery (and what's explicitly _not_) |
| **Non-goals** | Things you deliberately won't build now — prevents scope creep |
| **Sprint** | A short work period: pick scope → build → test → demo → retro |
| **Gate** | A checkpoint: go / adjust / stop based on what you've learned |
| **DoD** | Definition of Done — checklist that defines when an item is _complete_ |
| **Milestone** | A delivery target (often 1–2 sprints for fast teams) |
| **P1 / P2 / P3** | Priority: Must / Should / Could |
| **Spike** | A time-boxed experiment to reduce uncertainty |
| **Demo** | Showing what actually works in a runnable build |
| **Retro** | Short reflection: what worked, what was hard, what to improve |
| **Test Phase** | A focused verification block near the end of sprint/milestone (batch verification style) |

---

## Common mistakes

| Mistake | Fix |
|---------|-----|
| PRD becomes a novel | Keep it scannable. Put research in RESEARCH.md |
| Sprint without demo | If you can't show it, it's not done |
| Scope creeps silently | Write non-goals. Review at gates |
| DoD is vague | Make every check testable: "user can X" not "X works" |
| Skipping retro | Even 5 minutes of reflection improves the next sprint |
| Batch testing becomes chaos | Use a Test Phase Gate + map failures back to sprint tasks |

---

## Waterfall vs Agile (and why we combine them)

**Waterfall** plans phases in sequence (requirements → design → build → test). It works when requirements are stable but risks discovering problems late.

**Agile** delivers in small increments with early feedback. You learn faster and can change direction.

**Agile-with-gates** combines both:
- The **steps** give you a clear map (problem → MVP → launch)
- **Sprints** are the engine (small deliveries + early feedback)
- **Gates** are decision points (go / adjust / stop) that prevent scope creep and bad bets

---

## Optional documents

If your project grows, you can split the TDD into:

| Document | Purpose |
|----------|---------|
| **DESIGN.md** | UI/UX flows, wireframes, interaction design, game feel |
| **ART_BIBLE.md** | Visual style rules: colors, typography, icons, VFX consistency |

**Rule of thumb:** Keep TDD.md technical. Move experience design to DESIGN.md and visual rules to ART_BIBLE.md only when needed.

---

## License

These templates are free to use, modify, and share. Attribution to r- is appreciated but not required.



