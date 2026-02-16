# Carrier Intelligence Suite (MVP)

A lightweight web app that scores LTL carriers using cost + service + risk metrics and produces explainable routing recommendations.

## What’s inside
- **Carrier Performance Scorecard** (cost/CWT, on-time, reclass, damage, invoice accuracy)
- **Routing Intelligence** (density-aware recommendation + guardrails + explanation + fallbacks)
- **Procurement Simulator** (shift volume between carriers and estimate savings + risk deltas)
- **Data Upload** (CSV ingestion to power dashboards with real metrics)
- **Ops Insights** (lane heatmap, outlier lanes, dock SOP impact — unlocked when CSV includes the optional compliance column)

## Tech
- Vite + React
- TailwindCSS
- Recharts
- Local CSV parsing (in-memory) for MVP

## Quick start
```bash
npm install
npm run dev
```

Build / preview:
```bash
npm run build
npm run preview
```

## CSV format (shipments)
Minimum recommended columns:
- `shipment_id`
- `ship_date` (YYYY-MM-DD or any parseable date)
- `carrier_id` (A/B/C/D or SCAC) **or** `carrier_name`
- `origin_zip3`
- `dest_zip3`
- `weight_lb`
- `cube_ft3`
- `packaging_type` (pallet/crate/carton/odd)
- `billed_total` (optional; falls back to `quoted_total`)
- `quoted_total` (optional)
- `delivered_on_time` (true/false/1/0)
- `reclass_flag` (true/false/1/0)
- `damage_flag` (true/false/1/0)
- `invoice_disputed` (true/false/1/0)

Optional (unlocks Dock SOP impact):
- `dock_compliance_color` (green/yellow/red)

Download a template from the **Data** tab in the app.

## Notes / next production step
This MVP stores uploaded CSV data in memory per browser session.
For production:
- Add a backend API + Postgres
- Add real auth (Clerk/Auth0/Cognito)
- Add tenant isolation (Row Level Security / per-tenant schemas)
- Add scheduled ingestion from TMS/ERP sources

## License
MIT (see LICENSE).
