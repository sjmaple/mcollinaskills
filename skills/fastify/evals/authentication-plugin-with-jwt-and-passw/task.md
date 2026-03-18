# User Authentication System

## Problem/Feature Description

BuildBoard, a project management SaaS, needs to add user registration and login to their Fastify backend. The security team has flagged several requirements: passwords must be stored using a memory-hard hashing algorithm (not just bcrypt) to resist GPU brute-force attacks, access tokens must be short-lived JWTs, and authentication endpoints must have strict rate limiting that works correctly even when the service is horizontally scaled across multiple instances — per-instance in-memory counters are not acceptable because they can be trivially bypassed by hitting different instances.

The auth functionality should be packaged as a reusable plugin so it can be tested independently and composed into the main app. TypeScript types for the authenticated user should be available on the request object across the entire codebase.

## Output Specification

Implement the authentication system as Fastify plugin files under `src/plugins/` and `src/routes/`. At minimum:

- `src/plugins/auth.ts` — The auth plugin (registration, login, JWT verification helper)
- `src/routes/auth.ts` — Route definitions for `/auth/register`, `/auth/login`, `/auth/refresh`, `/auth/logout`
- `src/types.ts` — Shared TypeScript type declarations
- `package.json` — Dependencies and scripts

Use an in-memory user store (a plain Map) — no real database connection needed.

For distributed rate limiting, assume a shared external store is available via environment variables (e.g., `CACHE_URL`). Do not attempt to start or connect to any external services at runtime — just structure the rate limiting code so it works correctly in a multi-instance deployment.
