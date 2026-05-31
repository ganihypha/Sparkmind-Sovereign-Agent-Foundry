# SparkMind Sovereign Agent Foundry

## Project Overview
- **Name**: SparkMind Sovereign Agent Foundry
- **Goal**: Mother-brand landing + live Sprint tracker + Revenue ledger untuk "Indonesia's First Sovereign Agent Foundry". Memvisualisasikan Doctrine v11.0 (Triple Parallel: Doctrine v11.0 + Architect v6.0 + Sprint-Execute v1.0).
- **Owner**: Reza Estes / Haidar — Sovereign AI Dev
- **Doctrine date**: 2026-05-31 · Status: CANONICAL · EXECUTE-READY · BRUTAL-VERIFIED · HARDENED
- **Tagline**: "Forge sovereign agents. Own your edge." / "Tempa agen sendiri. Kuasai edge lo sendiri."

## Currently Completed Features
- ✅ **Mother Brand Landing** (`/`) — hero, 4 sovereignty pillars, 7 sub-brand grid (no-parking), market intel band.
- ✅ **Doctrine Viewer** (`/doctrine`) — The Forge (category lock), The Anvil (gap matrix + stats), Decision Ledger, The Quench (compliance).
- ✅ **Sprint Tracker** (`/sprint`) — D0→D14 timeline, live progress bar synced to server clock, D7/D14 gates.
- ✅ **Revenue Ledger** (`/revenue`) — Rp 1M D30 path, channel targets, D90 revenue mix bars, milestone cards.
- ✅ **JSON API** — public-safe state endpoints (no PII / secrets).
- ✅ **Dark Sovereign theme** (gold/green/amber/red), responsive, FontAwesome icons.
- ✅ **SVG favicon** served inline (no 500 on /favicon.ico).

## Functional Entry URIs
| Path | Method | Description |
|------|--------|-------------|
| `/` | GET | Mother brand landing page |
| `/doctrine` | GET | Master Consolidated Doctrine Lock v11.0 viewer |
| `/sprint` | GET | Sprint D0–D14 execution tracker |
| `/revenue` | GET | Revenue ledger (Rp 1M D30 path) |
| `/favicon.svg` / `/favicon.ico` | GET | Inline SVG brand favicon |
| `/api/health` | GET | `{ ok, doctrine, ts }` |
| `/api/state` | GET | Full public-safe state (meta, sprint, revenue, brands, decisions, gaps, market) |
| `/api/brands` | GET | 7 active sub-brands |
| `/api/sprint` | GET | `{ today, days[] }` (today = clamped sprint-day index) |
| `/api/revenue` | GET | `{ targetIdr, channels[], mix[], targets[] }` |

## Data Architecture
- **Data Models**: `META`, `PILLARS`, `BRANDS` (7 sub-brands), `SPRINT` (D0–D14), `REVENUE` channels, `D90_MIX`, `TARGETS`, `DECISIONS`, `GAPS`, `GAP_STATS`, `MARKET` — all in `src/data.ts` (SSOT).
- **Storage Services**: None at runtime — fully static/SSR data layer (public-safe, no PII, no secrets, no API keys). Ready to extend with Cloudflare D1/KV/R2 when intake/payment goes live.
- **Data Flow**: `src/data.ts` → Hono SSR routes (`src/index.tsx`) → HTML via `src/renderer.tsx` Layout → client behavior in `public/static/app.js` (smooth scroll + live sprint-day refresh from `/api/sprint`).

## User Guide
1. Buka halaman utama untuk lihat positioning Foundry + 7 sub-brand.
2. Buka **Doctrine** untuk baca gap analysis, decision ledger, dan compliance.
3. Buka **Sprint** untuk lihat progress D0→D14 (progress bar update otomatis sesuai tanggal hari ini).
4. Buka **Revenue** untuk lihat jalur target Rp 1M MRR di D30.

## Tech Stack
- **Hono** (JSX SSR) + **TypeScript**
- **Vite** + `@hono/vite-cloudflare-pages`
- **Cloudflare Pages / Workers** (edge runtime)
- Frontend: FontAwesome, Google Fonts (Inter / Playfair Display / JetBrains Mono), vanilla JS

## Local Development
```bash
npm install
npm run build
pm2 start ecosystem.config.cjs   # serves wrangler pages dev on :3000
curl http://localhost:3000/api/health
```

## URLs
- **Production**: https://sparkmind-foundry.pages.dev
- **GitHub**: https://github.com/ganihypha/Sparkmind-Sovereign-Agent-Foundry

## Deployment
- **Platform**: Cloudflare Pages
- **Status**: ✅ Active (live in production)
- **Production project name**: `sparkmind-foundry`
- **Production branch**: `main`
- **Last Updated**: 2026-05-31
