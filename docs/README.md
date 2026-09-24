# TITAN Android documentation

This folder holds the **permanent** documentation for the Android app. Planning
material that changes often lives separately in [`roadmap/`](roadmap/README.md).

The product as a whole (domains, users, autonomy policy) is specified in the
backend repository:
[titan/docs](https://github.com/vlukyanets/titan/blob/master/docs/README.md).

## Specification

- [App spec](spec/app.md): screens, connection, offline behaviour, notifications

## Architecture

- [Overview](architecture/overview.md): stack, modules, data flow, streaming

## Decisions

| ADR | Title | Status |
|---|---|---|
| [0001](adr/0001-record-architecture-decisions.md) | Record architecture decisions | Accepted |
| [0002](adr/0002-openapi-generated-client.md) | API client generated from the backend's OpenAPI schema | Accepted |
| [0003](adr/0003-unifiedpush-notifications.md) | Push notifications through UnifiedPush and ntfy | Accepted |
| [0004](adr/0004-online-only-v1-with-offline-indicator.md) | Online-only v1 with a non-blocking offline indicator | Accepted |

New ADRs start from the [template](adr/0000-template.md).

## Process

- [Contributing: commits and pull requests](CONTRIBUTING.md)
- [Roadmap (volatile)](roadmap/README.md)
