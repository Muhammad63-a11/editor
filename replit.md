# Audiobook Video Maker

An offline-first Android app for turning premade background clips and audiobook audio into fast YouTube videos.

## Run & Operate

- `pnpm --filter @workspace/api-server run dev` — run the API server (port 5000)
- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from the OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- Required env: `DATABASE_URL` — Postgres connection string

## Stack

- pnpm workspaces, Node.js 24, TypeScript 5.9
- API: Express 5
- DB: PostgreSQL + Drizzle ORM
- Validation: Zod (`zod/v4`), `drizzle-zod`
- API codegen: Orval (from OpenAPI spec)
- Build: esbuild (CJS bundle)
- Mobile: Expo Router, AsyncStorage, local document/audio pickers

## Where things live

- `artifacts/audiobook-video-maker/app/index.tsx` — core mobile flow and local persistence
- `artifacts/audiobook-video-maker/constants/colors.ts` — product theme

## Architecture decisions

- The first build is frontend-only and persists clips/projects locally with AsyncStorage.
- Normal export is intentionally presented as stream-copy muxing; PIP is a separate future encoding mode.
- Edge TTS is an optional online action; imported audio remains independent.

## Product

Creators can import and manage premade clips, create projects, import or generate audiobook audio, calculate automatic looping, preview the arrangement, and prepare a fast local export.

## User preferences

- User requires Android-native/offline-first behavior; internet is only needed for Edge TTS.

## Gotchas

- Keep normal audiobook creation free of video frame processing; visual modifications belong in a separate heavy pipeline.

## Pointers

- See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details
