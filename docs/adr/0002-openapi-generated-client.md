# 0002. API client generated from the backend's OpenAPI schema

- Status: Accepted
- Date: 2026-09-24

## Context

The backend publishes its API contract as `docs/api/openapi.json`, generated
from FastAPI
([titan ADR 0004](https://github.com/vlukyanets/titan/blob/master/docs/adr/0004-openapi-from-fastapi.md)).
Hand-written Kotlin models would drift away from it.

## Decision

The app generates its API models and Retrofit interfaces from a copy of
`openapi.json` at build time, using the OpenAPI Generator Gradle plugin with
kotlinx.serialization. The copy lives in `core/network/openapi/openapi.json` and
is updated on purpose: each update is a commit that names the backend commit or
tag it came from.

## Consequences

- Backend changes never break the app silently. The app moves to a new
  contract when it chooses to.
- Generated code is not committed. It is rebuilt from the schema.
- SSE event payloads are generated as models too. The streaming transport is
  written by hand.
