# Outpost

Offline-first field app for technicians, inspectors and delivery staff: log jobs, take photos, capture GPS. Everything syncs automatically when back online.

## Notes
Local SQLite on device, background sync, conflict resolution, per-record sync status (pending / syncing / done), push notifications.

## Brand
Main color: `#15803D`. Use it as the single primary color across the whole app (NativeWind theme token `primary`). Support light and dark mode, large touch targets, accessible contrast.

## Layout
- `backend/`  Symfony (PHP) REST API
- `frontend/` React Native + Expo (Expo Router) + TypeScript mobile app
- `docker-compose.yml` Postgres, Redis, Mailpit (dev services only)

## Stack
- Backend: Symfony, API Platform (OpenAPI), Doctrine ORM, PostgreSQL, LexikJWT auth, Symfony Messenger
- Mobile: React Native, Expo, Expo Router, TypeScript, NativeWind, TanStack Query, expo-sqlite / expo-location where relevant
- Quality: PHPUnit, PHPStan, PHP-CS-Fixer / Jest, ESLint, Prettier / GitHub Actions

## Local setup
- Start services: `docker compose up -d`
- Database URL: `DATABASE_URL="postgresql://app:app@127.0.0.1:5435/outpost?serverVersion=16&charset=utf8"` (put in `backend/.env.local`)
- Backend: `cd backend`, `composer install`, `php bin/console doctrine:migrations:migrate`, `symfony serve`
- Mobile: `cd frontend`, `npm install`, `npx expo start`
- On a real phone, the API URL must be your PC's LAN IP (not localhost). Keep it in an `EXPO_PUBLIC_API_URL` env variable.
- Tests: `cd backend && php bin/phpunit` / `cd frontend && npm test`
- Mail catcher UI: http://localhost:8028

## Rules
- TypeScript strict mode; no `any` unless justified in a comment.
- Generate the mobile API client from the backend OpenAPI spec (openapi-typescript or Orval). Never hand-write API types.
- Use `npx expo install <pkg>` for native packages so versions match the Expo SDK.
- Small, focused commits (Conventional Commits). Add or update tests with every feature.
- Never commit secrets; use `.env.local`.
- Prefer simple, readable code over clever code. Ask before adding a new dependency or changing the architecture.
## UI spec
The full UI specification (design system, screens, states, light/dark theming) is in `docs/ui-spec.md`. Treat it as the source of truth for every screen. Build screens in the batches requested, with typed mock data in `src/mocks/`, and keep all colors in the central theme file.