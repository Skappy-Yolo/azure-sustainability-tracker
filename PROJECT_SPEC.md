# PROJECT_SPEC.md — Azure Belgium Central Sustainability Tracker

## What This Is

An interactive dashboard visualizing Microsoft's published water usage efficiency (WUE) and sustainability data, contextualized for the Azure Belgium Central region launched November 2025. Uses only real, publicly available numbers — no fabricated data.

**This is the SECONDARY demo.** The Copilot Blast Radius Simulator is the opener. This only comes out if a Microsoft employee asks about Azure infrastructure, sustainability, or the Belgian data centers.

**Expo is March 26. Today is March 23. Blast Radius is the priority. Only build this if Blast Radius is done and time remains.**

---

## Current Status (as of March 23, 2026)

- ✅ PROJECT_SPEC.md spec written and updated
- ✅ GitHub repo created: https://github.com/Skappy-Yolo/azure-sustainability-tracker
- ❌ No code written yet
- ❌ No npm scaffold yet

**Build order:** Start this ONLY after Blast Radius Day 2 is complete.

---

## Honest Assessment

### What this is and isn't
This is a well-sourced, well-framed dashboard of numbers already on Microsoft's public website. Its value is not the data — it's the framing: "here's what's published, here's what's missing, and here's why that gap matters." The intellectual honesty angle is genuine differentiation.

What it is NOT: a technical depth demo. It shows research rigor and constructive thinking, not engineering capability. Do not lead with this at the booth.

### When it works
If the conversation naturally reaches Azure, sustainability, or Belgium's data center investment, pull it out. It gives you 30 more seconds of substance. It also shows you think beyond the immediate product to the broader Microsoft story.

### When NOT to use it
If Blast Radius is landing well, do not interrupt the momentum. This is a backup, not a co-headliner.

---

## Decision Log

### DS-01 | Priority: Secondary — only build if Blast Radius is complete
**Date:** 2026-03-23
**Decision:** This project is deprioritized relative to Blast Radius. With 3 days until expo, Blast Radius is the one that must exist. This is a 1-day build (all static data, no APIs) — if March 25 has time after Blast Radius polish, build it. If not, skip it.
**Why:** A polished single demo is better than two half-finished ones.

### DS-02 | Data: All static, no API calls
**Date:** 2026-03-23
**Decision:** All data lives in `src/data/sustainabilityData.ts` as hardcoded TypeScript. No runtime API calls. No build-time data fetching.
**Why:** This was already the spec. Reconfirmed: the Belgium-specific WUE data does not exist publicly (not published separately from Microsoft's global fleet numbers). There is nothing to fetch. Every number is sourced from a published URL and baked in directly.

---

## Why This Matters

Microsoft committed to "water positive" by 2030, but AI-driven data center growth is pushing water consumption upward. Azure Belgium Central — three data centers near Brussels, Microsoft's largest Belgian investment at €1B+ — launched into a country with climate-driven drought/flood cycles and EU environmental scrutiny. Brad Smith (January 2026) committed to "community-first" reporting on environmental impact. This dashboard is a concept of what that reporting could look like for Belgium specifically.

EU regulation is expected in 2026 requiring data center operators to set minimum performance standards for water usage. Timing is relevant.

---

## Published Data Points (VERIFIED — every number must have a source)

### Microsoft Global WUE
- **FY2024:** 0.30 L/kWh — Source: datacenters.microsoft.com/sustainability/efficiency/
- **FY2021:** 0.49 L/kWh (39% improvement) — Source: same
- **Water saved per zero-water facility:** 125 million liters/year — Source: Microsoft Cloud Blog, December 9, 2024
- **Zero-water cooling pilots:** Phoenix AZ and Mt. Pleasant WI, 2026 — Source: same
- **Fleet-wide zero-water target:** Late 2027 for all new builds — Source: same
- **Community-first commitment:** Brad Smith, January 2026 — Source: Microsoft On The Issues blog

### Industry Benchmarks
- **Industry average WUE:** 1.8 L/kWh — Source: Uptime Institute Annual Data Center Survey 2023
- **AWS WUE:** ~0.18 L/kWh — Source: AWS Sustainability page
- **Google WUE:** ~0.20 L/kWh — Source: Google Environmental Report

### Azure Belgium Central
- **Launch date:** November 18, 2025
- **Configuration:** 3 availability zones near Brussels
- **Investment:** €1B+ over 4 years
- **Cooling:** Industrial canal water — Source: aquatechtrade.com
- **Economic impact projection:** ~€59B additional revenue over 4 years; ~85,000 new jobs — Source: IDC/Microsoft

### What Is NOT Publicly Available — Do NOT fabricate
- Belgium-specific facility WUE (not published separately)
- Actual water consumption volume in liters for Azure Belgium Central
- Specific cooling technology detail beyond "industrial canal water"
- Per-region energy mix or PUE

**CRITICAL: If a number is not in the list above, do not put it in the dashboard. Show "Not yet publicly reported" instead. This honesty is the point.**

---

## The Demo Flow (30 seconds)

1. **Open the dashboard.** Clean, light-mode layout with sourced sustainability numbers.

2. **Overview panel:**
   - Line chart: Microsoft global WUE 2021 → 2024 (0.49 → 0.30 L/kWh)
   - Bar chart: Microsoft vs AWS vs Google vs industry average
   - Azure Belgium Central card: launch date, 3 AZs, investment, cooling approach

3. **Belgium context panel:**
   - Zero-water commitment timeline: pilot 2026 → fleet-wide 2027
   - What 125M liters saved means in Belgian household terms
   - EU 2026 regulation context

4. **"What's missing" panel** — the intellectual honesty moment:
   - Cards for Belgium-specific WUE (not reported), per-facility water volume (not reported), energy mix (not reported)
   - "Microsoft's community-first commitment suggests this data should become available."

**The 30-second pitch:**
"I also put together something on the sustainability side. Microsoft's global WUE dropped from 0.49 to 0.30 liters per kilowatt-hour between 2021 and 2024, and zero-water cooling saves 125 million liters per facility per year. I assembled all the public data into a Belgium-specific dashboard — every number sourced. The interesting part is what's NOT yet public: Belgium-specific WUE, actual water volumes, energy mix. Brad Smith committed to community-first reporting in January. This is a concept of what that could look like."

---

## Tech Stack

- **React 18 + TypeScript + Vite**
- **Fluent UI v9** (`webLightTheme` — light mode, contrast with Blast Radius dark mode)
- **Recharts** — line charts, bar charts, responsive containers

No backend. No API calls. Pure static frontend on Azure Static Web Apps.

---

## Data Structure

```typescript
// src/data/sustainabilityData.ts
interface DataPoint {
  value: number;
  unit: string;
  year: number;
  source: string;        // Full URL to published source
  sourceName: string;    // Human-readable source name
  verified: boolean;     // Always true — only verified data included
}

interface MissingDataPoint {
  label: string;         // e.g., "Belgium-Specific WUE"
  reason: string;        // Why it's missing
  commitment: string;    // Which Microsoft commitment should cover this
}
```

Every chart and card must render a clickable source link. No exceptions.

---

## UI Layout

```
┌─────────────────────────────────────────────────────────┐
│  Azure Belgium Central — Sustainability Tracker         │
│  "Every number sourced. Every gap acknowledged."        │
├─────────────────────────┬───────────────────────────────┤
│  [WUE Trend Chart]      │  [Industry Comparison]        │
│  Line: 2021-2024        │  Bar: MSFT vs AWS vs Google   │
│  0.49 → 0.30 L/kWh     │  vs Industry Avg              │
│  Source link below      │  Source links below           │
├─────────────────────────┴───────────────────────────────┤
│  [Azure Belgium Central Card]                           │
│  Launched Nov 18, 2025 | 3 AZs | €1B+ investment       │
│  Cooling: Industrial canal water                        │
│  Zero-water: Pilot 2026 → Fleet 2027                   │
├─────────────────────────────────────────────────────────┤
│  [What's Missing — Data Transparency Panel]             │
│  Belgium WUE (not reported) | Water Volume (not rep.)   │
│  Energy Mix (not reported)                              │
│  "Brad Smith committed to community-first reporting."   │
└─────────────────────────────────────────────────────────┘
```

### Mobile
Stack everything vertically. Recharts `ResponsiveContainer` handles chart scaling. Cards go full-width. No D3 — this dashboard has no D3.

---

## Project Structure

```
azure-sustainability-tracker/
├── .github/
│   └── workflows/
│       └── deploy.yml
├── src/
│   ├── components/
│   │   ├── WUETrendChart.tsx         # Line chart: WUE 2021-2024
│   │   ├── IndustryComparison.tsx    # Bar chart: MSFT vs peers
│   │   ├── BelgiumCentralCard.tsx    # Info card for Azure Belgium Central
│   │   ├── ZeroWaterTimeline.tsx     # Timeline: pilot → fleet-wide
│   │   ├── TransparencyPanel.tsx     # "What's missing" data gap cards
│   │   └── SourceCitation.tsx        # Reusable source link component
│   ├── data/
│   │   └── sustainabilityData.ts     # All verified data with source URLs
│   ├── types/
│   │   └── index.ts
│   ├── App.tsx
│   └── main.tsx
├── package.json
├── tsconfig.json
├── vite.config.ts
├── staticwebapp.config.json
├── DECISIONS.md
└── README.md
```

---

## 1-Day Build Plan (only attempt after Blast Radius Day 2 is done)

### Morning: Scaffold + Data + Layout
- `npm create vite@latest . -- --template react-ts`
- Install deps
- Write `sustainabilityData.ts` with all verified data points and source URLs
- Basic App layout with Fluent UI light theme
- `SourceCitation.tsx` reusable component

### Afternoon: Charts + Cards
- `WUETrendChart.tsx` — Recharts LineChart, 2 data points (2021, 2024)
- `IndustryComparison.tsx` — Recharts BarChart, 4 providers
- `BelgiumCentralCard.tsx` — Fluent UI Card component
- `ZeroWaterTimeline.tsx` — simple visual timeline
- `TransparencyPanel.tsx` — 3 "not reported" cards

### Evening: Polish + Deploy
- Verify every number has a clickable source link
- Test mobile layout
- Deploy to Azure SWA
- 30-second demo rehearsal

---

## Dependencies

```bash
npm create vite@latest . -- --template react-ts
npm install @fluentui/react-components @fluentui/react-icons
npm install recharts
```

---

## Critical Constraints

1. **NEVER fabricate data.** Not in the dashboard. Not in the source citations. If uncertain, leave it out.
2. **Every number has a visible, clickable source.** This is the core message.
3. **Do not frame this as criticism of Microsoft.** It is constructive: "here's what Brad Smith committed to, here's a concept of what it would look like."
4. **This is the secondary demo.** Do not over-engineer it.
5. **If the conversation doesn't go to sustainability, don't force it.**
