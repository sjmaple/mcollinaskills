# Production-Ready Fastify API Scaffold

## Problem/Feature Description

A fintech startup called CredPay is launching a new payment processing API. They need to stand up the initial Fastify server foundation before the product team builds out individual endpoints. The infrastructure engineer on the team has identified several requirements that often trip up production deployments: the app must fail fast and loudly if required environment variables are missing, configuration must be loaded consistently regardless of deployment environment, the server needs to handle graceful shutdown when it receives OS signals (especially important for containerized deployments doing rolling updates), and it must protect itself from memory and event loop exhaustion under sudden traffic spikes.

The team also uses TypeScript extensively and wants to run it directly on Node.js 22+ without a build step, keeping the developer experience smooth. Logging must be structured and must not leak sensitive headers or credential fields into log aggregation tools.

## Output Specification

Produce a working Fastify server scaffold under `src/`. At minimum include:

- `src/app.ts` — The Fastify instance factory function (exported, not started inline)
- `src/server.ts` — Entry point that builds the app, starts listening, and handles shutdown
- `src/plugins/config.ts` — A plugin that loads and validates environment configuration
- `package.json` — With correct `scripts` for running the app in development and type-checking

The server must listen on the host and port read from the environment. Include a simple `GET /health` endpoint that returns `{ "status": "ok" }`.

Document any environment variables required in a `.env.example` file.
