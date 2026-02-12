# BACKLOG.md
Project: SkyLens – Weather Dashboard
Owner: Alex M / Product Lead
Last updated: 2026-02-10

## 1) Current milestone
**Milestone:** MS-01
**Milestone goal:** Deliver a testable MVP — current weather + 5-day forecast + clothing suggestion for any searched city.

**Scope rule:** MVP first. Everything else goes to Later/Icebox.

## 2) Active backlog (prioritized)
> ID format: BL-001, BL-002, ...

### P1 — Must (MVP)
#### BL-001 — City search input
- Milestone: MS-01
- Outcome: User can type a city name and submit the search
- Notes: Debounce input (300 ms). Validate non-empty string.
- DoD:
  - [ ] Input field renders and accepts text
  - [ ] Pressing Enter or clicking Search triggers the flow
  - [ ] Empty input shows validation message

#### BL-002 — Fetch & display current weather
- Milestone: MS-01
- Outcome: Current temperature, condition icon, description, wind, and humidity are displayed
- Notes: Uses WeatherService with WeatherAPI.com
- DoD:
  - [ ] Current weather card renders with correct data for searched city
  - [ ] Loading state shown while fetching
  - [ ] API error shows user-friendly message

#### BL-003 — Fetch & display 5-day forecast
- Milestone: MS-01
- Outcome: Five daily forecast cards with high/low temp and condition icon
- Notes: Data comes from same API call as current weather
- DoD:
  - [ ] 5 forecast cards render with correct day/temp/icon
  - [ ] Cards are responsive (stack on mobile)

#### BL-004 — LocalStorage caching
- Milestone: MS-01
- Outcome: Repeated searches use cached data if fresh (< 10 min)
- Notes: Cache last 5 cities, evict oldest
- DoD:
  - [ ] Second search for same city within 10 min uses cache (no API call)
  - [ ] Stale cache (> 10 min) triggers new fetch
  - [ ] Cache works across page reloads

#### BL-005 — Clothing suggestion
- Milestone: MS-01
- Outcome: A text suggestion appears based on temp + condition
- Notes: Rule-based — see spike in RESEARCH.md
- DoD:
  - [ ] Suggestion text renders below current weather
  - [ ] Cold + rain → "Warm jacket and umbrella"
  - [ ] Warm + clear → "Light clothes, sunglasses"
  - [ ] At least 5 distinct suggestion combos tested

### P2 — Should (if time)
#### BL-010 — Geolocation auto-detect
- Milestone: MS-01
- Outcome: App detects user's city on first load via browser geolocation
- DoD:
  - [ ] On first load, browser prompts for location
  - [ ] If granted, shows weather for detected city
  - [ ] If denied, falls back to default city or empty state

#### BL-011 — Dark / light mode toggle
- Milestone: MS-01
- Outcome: User can switch between dark and light themes
- DoD:
  - [ ] Toggle button in header
  - [ ] Preference saved in localStorage
  - [ ] All elements readable in both modes

### P3 — Could (nice to have)
#### BL-020 — Animated weather backgrounds
- Milestone: MS-02
- Outcome: Background animation matches current condition (rain, sun, snow)
- DoD:
  - [ ] At least 3 condition-specific animations
  - [ ] Animations don't hurt performance (< 2 % CPU)

## 3) Bugs (optional)
> No bugs yet — project has not shipped.

## 4) Tech debt / chores (time-boxed)
#### TD-001 — Set up project structure
- Milestone: MS-01
- Why: Need basic file structure before building features
- DoD:
  - [ ] index.html, style.css, app.js created
  - [ ] Module files created (weatherService.js, clothingAdvisor.js, uiRenderer.js)

## 5) LATER (not now, but planned)
- Unit preference (°C / °F toggle) — reason: need user testing first to confirm demand
- Multi-language support — reason: English-only for MVP

## 6) ICEBOX (ideas / maybe someday)
- Share forecast as shareable image — why interesting: viral potential
- Weekly / monthly trend chart — why interesting: differentiator, but high effort
- Voice search ("Hey SkyLens, weather in Oslo") — why interesting: accessibility + novelty
