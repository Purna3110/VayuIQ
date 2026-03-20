# Workspace

## Overview

VayuIQ - AI-powered Air Quality Intelligence Platform. A premium full-stack web app with 3D globe, Hyderabad heatmap, AQI dashboards, carbon tracker, citizen reporting, and authority management.

## Stack

- **Monorepo tool**: pnpm workspaces
- **Node.js version**: 24
- **Package manager**: pnpm
- **TypeScript version**: 5.9
- **API framework**: Express 5
- **Database**: PostgreSQL + Drizzle ORM
- **Validation**: Zod (`zod/v4`), `drizzle-zod`
- **API codegen**: Orval (from OpenAPI spec)
- **Build**: esbuild (CJS bundle)
- **Frontend**: React + Vite + Tailwind CSS v4
- **Globe**: react-globe.gl + three.js
- **Map**: react-leaflet + leaflet
- **Charts**: Recharts
- **Animations**: Framer Motion

## Structure

```text
artifacts-monorepo/
├── artifacts/
│   ├── api-server/         # Express API server
│   └── vayuiq/             # React + Vite frontend (previewPath: /)
├── lib/                    # Shared libraries
│   ├── api-spec/           # OpenAPI spec + Orval codegen config
│   ├── api-client-react/   # Generated React Query hooks
│   ├── api-zod/            # Generated Zod schemas from OpenAPI
│   └── db/                 # Drizzle ORM schema + DB connection
├── scripts/
├── pnpm-workspace.yaml
├── tsconfig.base.json
├── tsconfig.json
└── package.json
```

## VayuIQ Features

### Frontend (artifacts/vayuiq)
- Login page with Citizen / Authority tabs
- Hero page: 3D Earth globe (react-globe.gl) with AQI panel + cinematic zoom to Hyderabad
- Dashboard: real-time AQI (5s refresh), prediction charts, heatmap, hotspots
- Carbon Tracker: carbon footprint calculator with suggestions
- Report System: submit pollution reports with location
- Authority Dashboard: task management + live heatmap

### Backend (artifacts/api-server)
Routes:
- `GET /api/aqi/current?lat=&lng=` - current AQI data
- `GET /api/aqi/prediction` - 3-day forecast
- `GET /api/aqi/hotspots` - Hyderabad pollution hotspots
- `POST /api/auth/login` - login (citizen + authority)
- `GET/POST /api/reports` - citizen pollution reports
- `GET/POST /api/tasks` - authority tasks
- `PATCH /api/tasks/:id` - update task status/notes

### Authority Credentials
- Ravi / 1234, Priya / 1234, Arjun / 1234, Sneha / 1234, Kiran / 1234

### DB Schema
- `reports` table: location, description, severity, status, lat, lng
- `tasks` table: title, description, status, notes, location

## TypeScript & Composite Projects

Every package extends `tsconfig.base.json` which sets `composite: true`. The root `tsconfig.json` lists all packages as project references.

## Root Scripts

- `pnpm run build` — runs `typecheck` first, then recursively runs `build` in all packages
- `pnpm run typecheck` — runs `tsc --build --emitDeclarationOnly` using project references
