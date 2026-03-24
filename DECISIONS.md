# Decision Log — Azure Belgium Central Sustainability Tracker

---

## DS-01 | Priority: Secondary — only build if Blast Radius is complete
**Date:** 2026-03-23
**Status:** ACTIVE
**Decision:** Deprioritized relative to Copilot Blast Radius Simulator. This is a 1-day build. Attempt only after Blast Radius Day 2 is complete (March 24 evening at earliest).
**Why:** With 3 days until expo, a polished single demo beats two half-finished ones. Blast Radius is the one that must exist.

---

## DS-02 | All data is static TypeScript — no API calls, no build-time fetching
**Date:** 2026-03-23
**Status:** ACTIVE
**Decision:** All numbers live in `src/data/sustainabilityData.ts`. No runtime or build-time API calls.
**Why:** Belgium-specific WUE data does not exist publicly. Microsoft has not published per-region WUE. There is nothing to fetch. Every number comes from a URL that can be cited directly. Baking it in is both simpler and more honest.

---

## DS-03 | Show data gaps explicitly, not silently
**Date:** 2026-03-23
**Status:** ACTIVE
**Decision:** The TransparencyPanel shows exactly which data points are not publicly reported, with a reference to Microsoft's community-first commitment as the basis for why they should eventually be reported.
**Why:** Silently omitting missing data would make the dashboard look complete when it isn't. Showing the gaps explicitly is the intellectual honesty angle that makes this demo memorable — and it invites a real conversation with Microsoft employees about what data they actually have internally.
