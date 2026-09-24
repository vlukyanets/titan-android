# 0003. Push notifications through UnifiedPush and ntfy

- Status: Accepted
- Date: 2026-09-24

## Context

TITAN has no public endpoint, and everything runs on the owner's tailnet.
Firebase Cloud Messaging would need a Firebase project, Google Play Services
on the phone, and notification content passing through Google.

## Decision

The app uses the UnifiedPush connector library. The backend cluster runs an ntfy
server on the tailnet that acts as the push server, and the ntfy Android app is
the UnifiedPush distributor on the phone. The app registers its UnifiedPush
endpoint with the backend after pairing.

## Consequences

- Users install the ntfy app (or another UnifiedPush distributor) once. The
  settings screen guides them through it.
- Delivery works only while the phone can reach the tailnet. Missed
  notifications are fetched from the backend's notification history.
- There is no Google dependency, so the app also works on de-Googled devices.
