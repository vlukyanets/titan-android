# TITAN Android app specification

Status: **Draft v1**.

The product itself (domains, autonomy policy, users and roles) is specified once
in the backend repository:
[titan/docs/spec/product.md](https://github.com/vlukyanets/titan/blob/master/docs/spec/product.md).
This document covers only what is specific to the Android client.

## Role of the app

The Android app is the primary daily client. It is how family members chat with
the assistant, see today's plan, manage their data, and answer approval
requests and reminders.

## Connection

- The phone must be on the owner's **Tailscale** tailnet. The app talks only to
  TITAN nodes over the tailnet. There is no public endpoint.
- The app uses the **cluster address** (for example
  `titan.example-tailnet.ts.net`), a Tailscale Service that every ready node
  advertises. Tailscale connects the phone to the nearest available node, so
  failover needs no app logic
  ([titan ADR 0013](https://github.com/vlukyanets/titan/blob/master/docs/adr/0013-one-cluster-address.md)).
- **Pairing**: on first start the user enters the cluster address, username and
  password. The backend issues a device token, which is stored with the Android
  Keystore. The password is not stored. The token works on every node.
- As an advanced fallback, the user can add individual node addresses. If the
  cluster address is unreachable the app tries them in order.

## Screens (v1)

| Screen | Contents |
|---|---|
| **Today** | Today's events and time blocks, due tasks, habit check-ins, pending approvals |
| **Chat** | Conversation with the agent. Streamed replies, visible tool activity, inline Approve and Reject buttons for approval requests |
| **Tasks** | Projects and tasks: list, filter, create, edit, complete |
| **Calendar** | Day and week view of events and time blocks |
| **Notes** | Notes list, search (semantic and keyword), editor, the "What TITAN remembers about me" memory list |
| **Trackers** | Trackers with quick logging, streaks and simple charts |
| **Notifications** | History of reminders, approvals and system messages |
| **Settings** | Account, devices, per-domain autonomy overrides, nodes, notification setup, sign out |

Material 3, with light and dark themes and dynamic colour on Android 12+.

## Online-only v1 and offline behaviour

The v1 app has **no offline storage or write queue**. Every action needs a
connection to a node. Losing the connection must still not disrupt the user:

- **Content that is already on screen stays visible.** The screen does not
  clear, blank out or switch to an error page.
- **No full-screen spinner or blocking overlay** because of connectivity.
- A small **"Offline" status indicator** appears in a corner of the screen
  (the top app bar area) while nodes are unreachable, and disappears when the
  connection returns.
- Actions that need the server (send a message, save, complete) are disabled or
  fail with a short inline message such as a snackbar. Nothing is queued.
- When the connection returns, visible screens refresh quietly in the
  background.

Design: [ADR 0004](../adr/0004-online-only-v1-with-offline-indicator.md).

## Notifications

- Push through **UnifiedPush**, with the self-hosted **ntfy** server on the
  tailnet as the distributor. No Firebase or Google Play Services dependency
  ([ADR 0003](../adr/0003-unifiedpush-notifications.md)).
- Notification kinds: reminder (Snooze and Done actions), approval (Approve and
  Reject actions), daily plan summary, budget warnings.
- Actions in a notification work without opening the app.

## Platform

- Kotlin, Jetpack Compose, minSdk **26** (Android 8.0).
- The API client is generated from the backend's OpenAPI schema
  ([ADR 0002](../adr/0002-openapi-generated-client.md)).

## Acceptance criteria (v1)

- Pairing with a node over Tailscale works, and revoking the device on the
  backend signs the app out.
- Chat replies stream token by token. Approval requests can be answered inline
  and from the notification.
- Switching airplane mode on and off leaves the current screen content in place,
  shows and hides the offline indicator, and never shows a full-screen spinner.
- Every screen in the table above works on API 26 and on the current Android
  release.
