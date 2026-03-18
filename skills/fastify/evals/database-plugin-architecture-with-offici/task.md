# Fastify Database Plugin and Secure API

## Problem/Feature Description

DevTrack, a software project tracking tool, is migrating their monolith to a Fastify-based microservice. They have a PostgreSQL database and need a proper database integration that the rest of the application can use. A key requirement from their infrastructure team: database access must be encapsulated as a plugin so it can be cleanly initialized, shut down (connection pool cleanup), and replaced with a mock during tests. The plugin's database connection must be available to routes even though the plugin and routes live in separate files.

Additionally, the DevTrack API will be consumed by a browser-based frontend from a different domain, and it needs to pass security audits that check for missing HTTP security headers. The team also runs structured log analysis and needs to ensure sensitive data (tokens, passwords) never appears in logs.

## Output Specification

Produce a Fastify application under `src/` that demonstrates the database plugin architecture:

- `src/plugins/database.ts` — Database plugin that provides a `pg` connection
- `src/plugins/repositories.ts` — A plugin that creates repository objects on top of the database
- `src/routes/projects.ts` — Simple CRUD routes for projects (in-memory is fine, or using fastify.pg if wiring the db plugin)
- `src/app.ts` — Main app factory that registers all plugins and routes
- `package.json` — Dependencies and run scripts

The database plugin should connect to `process.env.DATABASE_URL` but does not need to actually run queries for this task — you can stub the implementation. Write the plugin structure correctly so it integrates properly with Fastify's lifecycle. Include CORS and security header setup for the API.
