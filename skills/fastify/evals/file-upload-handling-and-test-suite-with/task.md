# File Upload Service with Tests

## Problem/Feature Description

DataVault, a document management platform, needs a file upload endpoint that accepts documents from users. Previous implementations had a serious bug: the multipart parser silently truncated files that exceeded the size limit, storing incomplete documents without notifying the uploader. This caused data corruption in production. The team wants a proper implementation with explicit, enforced limits and a comprehensive test suite.

The team uses Node.js 22 and wants to avoid external test framework dependencies — they want tests that can be run with the platform's built-in test runner. Tests should validate the upload endpoint's behavior without actually binding to a network port, keeping the test suite fast and runnable in CI without port conflicts.

## Output Specification

Produce the following files:

- `src/app.ts` — Fastify app factory with the upload endpoint registered
- `src/routes/uploads.ts` — `POST /uploads` endpoint that accepts a file upload and returns metadata (filename, mimetype, size)
- `src/routes/uploads.test.ts` — Test file for the uploads route

The upload endpoint should:
- Accept a single file field named `file`
- Return JSON with `{ filename, mimetype, size }` on success
- Return an appropriate error if no file is provided

Include `package.json` with a test script.

Also add a `GET /static/*` route (or register static file serving) that serves files from a `public/` directory relative to the source file's location.

## Input Files

The following starter app.ts is provided. Extract it, then build on it.

=============== FILE: src/app.ts ===============
import Fastify from 'fastify'

export async function buildApp() {
  const app = Fastify({ logger: false })

  // Register routes here

  return app
}
