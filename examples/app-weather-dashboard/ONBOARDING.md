# ONBOARDING.md
Project: SkyLens – Weather Dashboard
Owner: Alex M / Product Lead
Last updated: 2026-02-10

## 1) What is this project?
SkyLens is a minimal weather dashboard that shows current conditions, a 5-day forecast, and clothing suggestions — all in a single view, no clutter. Built for people who just want to know "What's it like outside, and what should I wear?"

- Product doc: `PRD.md`

## 2) Current status
- **Phase:** Building MVP
- **Milestone:** MS-01 — Deliver a testable MVP with current weather + forecast + clothing suggestion
- **Sprint:** 01 — Core Weather View (search + current + forecast) (see `/sprints/`)
- **Biggest open risk:** WeatherAPI.com free tier rate limits during heavy testing

## 3) Team & roles
| Name | Role | Responsible for |
|------|------|----------------|
| Alex M | Product Lead | PRD, scope decisions, user testing |
| Jordan K | Dev | Front-end implementation, API integration |
| Riley T | Design | Visual mockups, UX feedback |

## 4) Quick setup
### Prerequisites
- Any modern browser (Chrome, Firefox, or Safari)
- A text editor (VS Code recommended)
- A free API key from [WeatherAPI.com](https://www.weatherapi.com/) (sign up → copy key)

### Get running
```bash
# Clone the repo
git clone <repo-url>
cd skylens

# Add your API key
# Open src/weatherService.js and replace YOUR_API_KEY with your actual key

# Run locally — no build step needed, just open the file:
# Option A: double-click index.html
# Option B: use a local server
npx -y serve .
```

### Verify it works
- Open `http://localhost:3000` (or index.html directly)
- Type "Stockholm" in the search box
- You should see: current temperature + weather icon + 5-day forecast cards

## 5) Project structure
```
skylens/
├── docs/
│   ├── PRD.md             # What & why
│   ├── RESEARCH.md        # API comparison, spike results
│   ├── TDD.md             # Architecture, modules, test plan
│   ├── BACKLOG.md          # Prioritized work items
│   ├── ONBOARDING.md       # You are here
│   └── sprints/
│       └── SPRINT_01.md
├── index.html              # Single-page entry point
├── style.css               # All styles
├── app.js                  # Main entry — wires modules together
├── weatherService.js       # API calls + localStorage caching
├── clothingAdvisor.js      # Rule-based clothing suggestions
└── uiRenderer.js           # DOM updates
```

## 6) Key documents (reading order)
1. **This file** — you are here
2. **PRD.md** — understand the problem (weather app for quick checks), goals, and MVP scope
3. **TDD.md** — understand the architecture (4 modules, no back-end, localStorage caching)
4. **BACKLOG.md** — see what's been done, what's next (BL-001 through BL-008)
5. **SPRINT_01.md** — see the current sprint scope and demo checklist

## 7) Conventions & rules
### Branching / version control
- `main` branch = always working
- Feature branches: `feature/BL-XXX-short-description`
- Commit messages: `BL-XXX: short description` (e.g. `BL-002: add current weather card`)

### Code style
- Vanilla JavaScript (ES6+), no framework
- camelCase for variables and functions
- No build tools — plain files served statically
- Keep functions small (< 30 lines)

### Documentation
- Product decisions → PRD.md
- Technical decisions → TDD.md (section 9)
- API research → RESEARCH.md
- Tasks → BACKLOG.md
- Sprint work → /sprints/

### Definition of Done (project-level)
- Feature works in Chrome and Firefox
- No console errors
- Page loads in < 2 s
- Code is readable (comments on non-obvious logic)

## 8) How to contribute
1. Check `BACKLOG.md` — find an unassigned P1 or P2 item
2. Create a feature branch: `feature/BL-XXX-title`
3. Implement the feature and check every box in the item's DoD
4. Test in Chrome + Firefox
5. Push + open a PR against `main`
6. Demo the feature to the team

## 9) Useful links
- Repo: `<repo-url>`
- WeatherAPI.com docs: https://www.weatherapi.com/docs/
- Live version: not yet deployed (planned for after Sprint 02)

## 10) FAQ / gotchas
- **Q: I get "API key invalid" errors — what's wrong?**
  A: Make sure you replaced `YOUR_API_KEY` in `weatherService.js` with your actual key from WeatherAPI.com. The free tier takes a few minutes to activate after sign-up.

- **Q: Can I use npm / a bundler?**
  A: Not for MVP. We're keeping it simple with plain files. If the project grows beyond MS-01, we'll revisit (tracked in LATER section of BACKLOG).

- **Q: Where do I put new research or links I find?**
  A: In `RESEARCH.md` under "Sources & notes". If a finding changes scope or tech decisions, update PRD or TDD accordingly.
