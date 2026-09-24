# 0004. Online-only v1 with a non-blocking offline indicator

- Status: Accepted
- Date: 2026-09-24

## Context

A full offline mode (local database, write queue, conflict handling) is a large
amount of work, and the backend's own replication design is still open. On the
other hand, apps that clear the screen or show a full-screen spinner whenever
the network drops are frustrating to use.

## Decision

v1 is online-only: no Room database and no queued writes. When the connection
is lost:

- data already on screen stays visible, kept in ViewModel state;
- nothing blocks the screen, so no full-screen spinner or overlay;
- a small "Offline" indicator appears in the corner of the top app bar;
- actions that need the server are disabled or fail with a short inline
  message;
- screens refresh quietly once the connection returns.

## Consequences

- Data does not survive process death while offline. Reopening the app offline
  shows empty screens with the offline indicator. This is accepted for v1.
- A later offline mode can add a cache under the repositories without changing
  the UI rules.
- UI tests must cover losing the connection on every screen.
