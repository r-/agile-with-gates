# TDD.md
Project: SkyLens – Weather Dashboard
Owner: Alex M / Product Lead
Status: active
Last updated: 2026-02-01
Related milestone: MS-01 (MVP)

## 1) Summary
- What this builds (from PRD): A single-page weather dashboard showing current conditions, 5-day forecast, and clothing suggestions.
- Technical approach in one sentence: Vanilla HTML/CSS/JS front-end fetching from WeatherAPI.com, with localStorage caching and a simple rule-based clothing module.
- Key constraints: No back-end for MVP — everything runs client-side. Must work on modern browsers (Chrome, Firefox, Safari).

## 2) Architecture (big picture)
### Modules / boundaries
- **WeatherService** — responsibility: API calls + caching — API: `getWeather(city) → WeatherData`
- **ClothingAdvisor** — responsibility: map conditions to suggestions — API: `getSuggestion(temp, condition) → string`
- **UIRenderer** — responsibility: render data to DOM — API: `render(WeatherData, suggestion)`
- **SearchController** — responsibility: handle user input and coordinate modules — API: `onSearch(city)`

### Data ownership
- WeatherService owns API responses and cache (localStorage)
- UIRenderer owns DOM state
- No shared mutable state between modules

### Event / flow (if relevant)
- User types city → SearchController.onSearch() → WeatherService.getWeather() → ClothingAdvisor.getSuggestion() → UIRenderer.render()

## 3) Core components
- Component: WeatherService — Purpose: fetch + cache weather data, handle API errors
- Component: ClothingAdvisor — Purpose: rule-based clothing suggestions (15 rules)
- Component: UIRenderer — Purpose: update DOM with weather cards, forecast row, suggestion box
- Component: SearchController — Purpose: debounce input, validate city name, orchestrate flow

## 4) Public contracts
- Contract: `WeatherService.getWeather(city: string): Promise<WeatherData>`
  - Input: city name string
  - Output: `{ current: { temp, condition, wind, humidity, icon }, forecast: [{ day, high, low, condition, icon }] }`

- Contract: `ClothingAdvisor.getSuggestion(temp: number, condition: string): string`
  - Input: temperature in °C + condition keyword (e.g. "rain", "snow", "clear")
  - Output: suggestion text (e.g. "Warm jacket and umbrella")

## 5) Key scenarios
### Scenario A: Happy path — search city
1. User types "Gothenburg" and presses Enter
2. SearchController validates input and calls WeatherService
3. WeatherService checks cache (< 10 min old) → miss → fetches from API
4. API returns data → WeatherService caches it and returns WeatherData
5. ClothingAdvisor maps temp + condition → suggestion string
6. UIRenderer updates current weather card, forecast row, suggestion box

### Scenario B: API error
1. User searches "Gothenburg"
2. WeatherService.getWeather() → API returns 500
3. WeatherService checks cache → stale cache exists → returns cached data with "stale" flag
4. UIRenderer shows cached data + "Data may be outdated" banner

### Scenario C: Invalid city
1. User searches "asdf123"
2. API returns 400 / no results
3. WeatherService throws CityNotFoundError
4. UIRenderer shows "City not found — please try again"

## 6) Risks & mitigations
- Risk: WeatherAPI.com changes response format — Mitigation: isolate parsing in WeatherService, easy to update
- Risk: localStorage full — Mitigation: only cache last 5 cities, evict oldest

## 7) Testing plan (minimal)
- Unit: ClothingAdvisor rules (15 cases), WeatherService cache logic (hit/miss/stale)
- Integration: SearchController → WeatherService (mocked API) → UIRenderer (check DOM output)
- E2E: not needed for MVP
- Smoke test:
  1. Open index.html
  2. Search "Stockholm" — verify current weather + forecast + suggestion appear
  3. Disconnect network — search "Stockholm" again — verify cached data appears

## 8) Performance / constraints (if needed)
- Target: full render < 2 s on 4G (API ~200 ms + parse + render)
- Cache TTL: 10 minutes per city
- No build tools — plain files served statically

## 9) Decisions (technical)
- [2026-01-25] WeatherAPI.com over OpenWeatherMap — Why: single endpoint, generous limits — Impact: simpler fetch logic
- [2026-01-28] localStorage over server-side cache — Why: no back-end in MVP, simplest path — Impact: cache per-browser only
- [2026-02-01] No framework (vanilla JS) — Why: keep scope small, no build step — Impact: manual DOM updates

## 10) Optional splits (only if TDD gets too big)
- Not needed for this project size.

## 11) Links
- Product requirements: `PRD.md`
- Research notes: `RESEARCH.md`
- Plan: `BACKLOG.md` + `/sprints/`
