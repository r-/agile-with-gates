# RESEARCH.md
Project: SkyLens – Weather Dashboard
Owner: Alex M / Product Lead
Last updated: 2026-01-22

## 1) Purpose
This is the **research scratchpad**: links + notes + comparisons + spike results.
Conclusions should be copied into:
- `PRD.md` (product scope/decisions)
- `TDD.md` (technical choices/design)

## 2) Questions we're answering
- Q1: Which free weather API gives us the best coverage and rate limits?
- Q2: Can we deliver the full view (current + forecast) in a single API call?
- Q3: What clothing suggestion logic already exists?

## 3) What we found (copy-ready)
- OpenWeatherMap free tier allows 1 000 calls/day and supports current + 5-day forecast → Impacts: TDD (API integration) → Evidence: §6 source #1
- WeatherAPI.com offers a combined current+forecast endpoint in one call → Impacts: TDD (fewer requests) → Evidence: §6 source #2
- No good open-source clothing suggestion library found — we'll build simple rule-based logic → Impacts: PRD (scope decision) → Evidence: §5 spike #1

## 4) Options (only if needed)
### A) OpenWeatherMap
- Pros: well-known, large community, good docs
- Cons: current + forecast require two separate API calls on free tier
- Risks: rate limit could be tight during testing

### B) WeatherAPI.com
- Pros: single endpoint for current + forecast, generous free tier (1M calls/month)
- Cons: less community content, newer service
- Risks: less battle-tested

**Recommendation:** B (WeatherAPI.com) — single call simplifies architecture and rate limits are generous enough for MVP and beyond.

## 5) Spikes / experiments (only if done)
- Spike: Clothing logic prototype — Goal: build a simple temp/rain → suggestion mapper in JS — Result: 15 rules cover 90 % of cases — Next: BL-005 (implement clothing module)
- Spike: API response time test — Goal: measure WeatherAPI.com latency from Sweden — Result: avg 180 ms — Next: confirm caching strategy in TDD

## 6) Sources & notes
- WeatherAPI.com docs — https://www.weatherapi.com/docs/
  - Free tier: 1M calls/month, current + forecast in one call
  - Returns JSON with hourly, daily, and current data
- OpenWeatherMap docs — https://openweathermap.org/api
  - Free tier: 1 000 calls/day, 5-day/3-hour forecast
  - Separate endpoints for current and forecast
- yr.no API — https://api.met.no/
  - Free, no key needed, but Norwegian-centric and XML-heavy

## 7) Open questions / next steps
- Should we cache in localStorage or use a simple server proxy? → Next: decide in TDD
- How do we handle unit preferences (°C vs °F)? → Next: add to should-have in PRD if time
