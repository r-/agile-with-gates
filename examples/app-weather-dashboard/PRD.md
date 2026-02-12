# PRD.md
Project: SkyLens – Weather Dashboard
Owner: Alex M / Product Lead
Status: active
Last updated: 2026-02-10

## 1) Summary
- What we're building: A minimal weather dashboard that shows current conditions, a 5-day forecast, and clothing suggestions based on the weather.
- For who: People who want a fast, no-clutter weather check before heading out.
- Why now: Existing weather apps are bloated with ads and screens — we want a single-view experience.
- Success looks like:
  - Users get the info they need in under 5 seconds
  - 80 % of test users say it's faster than their current weather app
  - MVP live within 3 sprints

## 2) Problem & users
### Problem statement
Checking the weather today usually means opening a bloated app with ads, multiple taps, and irrelevant data. Users just want: "What's it like outside, and what should I wear?"

### Target users
- Primary: Daily commuters who check weather every morning
- Secondary: Parents deciding what to dress their kids in

### Context / use cases
- Morning routine: glance at the dashboard on desktop/tablet before leaving
- Weekend planning: check the 5-day forecast to decide on outdoor activities
- Travel prep: look up weather in another city

## 3) Goals & non-goals
### Goals
- G1: Display current weather + 5-day forecast for any searched city
- G2: Provide simple clothing suggestions based on temperature and conditions
- G3: Load the full view in under 2 seconds on a 4G connection

### Non-goals
- NG1: No user accounts or saved preferences in MVP
- NG2: No weather alerts or push notifications
- NG3: No hourly breakdown — daily granularity only

## 4) Scope (MVP)
### MVP: must-have
- Search by city name
- Current conditions (temp, icon, description, wind, humidity)
- 5-day daily forecast
- Clothing suggestion based on current temp + rain

### Should-have (if time)
- Auto-detect user's location via browser geolocation API
- Dark / light mode toggle

### Could-have (nice to have)
- Animated weather backgrounds
- Share forecast as image

## 5) Requirements (acceptance-level)
- R1: City search returns results within 1 second
  Acceptance: Type "Stockholm" → current weather renders within 1 s on 4G

- R2: Clothing suggestion matches conditions
  Acceptance: Temp < 5 °C + rain → suggests "warm jacket + umbrella"

- R3: 5-day forecast is accurate and readable
  Acceptance: Shows 5 distinct days with high/low temp and condition icon

## 6) UX / flows (lightweight)
- Main flow: Open app → see default city weather → (optional) search another city → view forecast + clothing tip
- Edge cases:
  - Invalid city name → show friendly error
  - API error → show cached data if available, else "try again" message
- Notes / constraints:
  - Single-page layout, no navigation needed for MVP

## 7) Success metrics
- Metric: Time to useful info — Target: < 5 seconds from page load
- Metric: User satisfaction (test group) — Target: 80 % rate it "better than current app"
- Metric: API error rate — Target: < 1 % of requests

## 8) Risks & assumptions
- Risk: Free weather API rate limits — Mitigation: cache responses for 10 min + pick API with generous free tier
- Risk: Clothing suggestions feel too generic — Mitigation: keep scope minimal, iterate post-MVP
- Assumption: Users prefer a single view over multiple screens — How to validate: user test with prototype

## 9) Decisions (product-level)
- [2026-01-15] Use OpenWeatherMap free tier — Why: 1 000 calls/day is enough for MVP testing — Impact: must cache aggressively
- [2026-01-20] Clothing suggestions text-only (no images) — Why: faster to ship — Impact: can iterate visuals later

## 10) Links
- Research: `RESEARCH.md`
- Technical design: `TDD.md`
- Plan: `BACKLOG.md` + `/sprints/`
