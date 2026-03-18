# Product Catalog REST API

## Problem/Feature Description

RetailHub, an e-commerce platform, needs a product catalog microservice built with Fastify and TypeScript. The engineering team has had issues with inconsistent response shapes and runtime type errors between their frontend and backend — data fields being missing, wrong types, or containing sensitive database internals that leaked into API responses. They need a solution where the TypeScript types and the JSON validation/serialization are derived from a single source of truth, so there's no drift between what the code says and what actually goes over the wire.

The team also wants the API to be fast at scale, as the catalog serves high read traffic and serialization overhead has been identified as a bottleneck in profiling sessions. The API must have consistent error responses so frontend clients can reliably parse failures.

## Output Specification

Build a Fastify REST API for the product catalog. The API should support:

- `GET /products` — list products with pagination (page, limit query params)
- `POST /products` — create a product
- `GET /products/:id` — get a single product
- `PATCH /products/:id` — update a product
- `DELETE /products/:id` — delete a product

Products have at minimum: `id` (string/uuid), `name` (string), `price` (number), `category` (string), `inStock` (boolean).

Produce source files under `src/`. Use an in-memory store (a plain Map or array) for the product data — no real database needed. Include a `package.json` with install and run scripts.

The implementation should include at least:
- `src/app.ts` — Fastify app factory
- `src/routes/products.ts` — route definitions
- `src/schemas/products.ts` — schema definitions
