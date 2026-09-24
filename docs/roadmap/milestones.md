# Milestones

Last updated: 2026-09-24.

## A1: Project skeleton

- [ ] Gradle Kotlin DSL project, version catalog, the modules from the
      [architecture overview](../architecture/overview.md).
- [ ] Material 3 theme, navigation scaffold, offline indicator component.
- [ ] ktlint or detekt, unit tests, GitHub Actions CI named `CI TITAN Android`
      (build, lint, test).
- [ ] OpenAPI Generator wired to a placeholder schema.

Exit: an empty app with navigation builds in CI and runs on API 26.

## A2: Pairing and chat

Depends on backend M1 (accounts, device tokens, chat API).

- [ ] Pairing flow and Keystore-backed token storage.
- [ ] `ConnectivityState` and node failover.
- [ ] Chat screen with SSE streaming and inline approvals.

Exit: pair with a node, chat with streaming, approve an action, and lose and
regain the connection without losing screen content.

## A3: Domain screens

Depends on backend M2.

- [ ] Today.
- [ ] Tasks and projects.
- [ ] Calendar day and week views.
- [ ] Notes, search and the memory list.
- [ ] Trackers with quick logging.

Exit: the acceptance criteria in the [app spec](../spec/app.md) pass for these
screens.

## A4: Notifications and settings

- [ ] UnifiedPush registration and the ntfy setup guide.
- [ ] Notification actions (Snooze, Done, Approve, Reject).
- [ ] Notification history screen.
- [ ] Settings: devices, per-domain autonomy overrides, nodes.

Exit: a reminder and an approval can be handled from the notification shade.

## Open questions

- Which charting library to use for trackers (Vico or custom Canvas)?
- Should the Tailscale connection state be detected and explained in the app
  (for example "Tailscale is off")?
- Widgets for Today and quick tracker logging after v1?
