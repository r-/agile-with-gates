# TDD.md
Project: <name>
Owner: <name/role>
Status: <draft / active / locked>
Last updated: <YYYY-MM-DD>
Related milestone: <MS-XX / M-XX> (optional)

## 1) Summary
- What this builds (from PRD/GDD): <1–2 lines>
- Technical approach in one sentence: <...>
- Key constraints: <platform/perf/tools>

## 2) Architecture (big picture)
### Modules / boundaries
- <Module A> — responsibility: <...> — API: <...>
- <Module B> — responsibility: <...> — API: <...>

### Data ownership
- <who owns what data?>
- <where is state stored?>

### Event / flow (if relevant)
- Input → <...> → <...> → Output

## 3) Core components
- Component: <name> — Purpose: <...>
- Component: <name> — Purpose: <...>

## 4) Public contracts
- Contract: <interface/endpoint/event>
  - Input: <...>
  - Output: <...>

## 5) Key scenarios
### Scenario A: <name>
1. <step>
2. <step>
3. <step>

### Scenario B: <name>
1. <step>
2. <step>

## 6) Risks & mitigations
- Risk: <...> — Mitigation: <...>

## 7) Testing plan (minimal)
- Unit: <what is unit-tested?>
- Integration: <what is integration-tested?>
- PlayMode/E2E: <what must run in Unity?>
- Smoke test: <1–3 manual steps for “release-ready”>

## 8) Performance / constraints (if needed)
- Target FPS / budgets: <...>
- Memory / allocations: <...>
- Platform constraints: <...>

## 9) Decisions (technical)
- [YYYY-MM-DD] <decision> — Why: <1 line> — Impact: <1 line>

## 10) Optional splits (only if TDD gets too big)
- `DESIGN.md` — UI/UX + interaction + game feel (flows, wireframes, feedback)
- `ART_BIBLE.md` — visual style + rules (colors, typography, icons, VFX/UI consistency)

## 11) Links
- Product requirements: `PRD.md` (or `GDD.md`)
- Research notes: `RESEARCH.md`
- Plan: `BACKLOG.md` + `/sprints/`
