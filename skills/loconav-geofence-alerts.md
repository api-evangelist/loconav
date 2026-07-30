---
name: Set up geofences and subscribe to alerts
description: Create geofence polygons, subscribe a vehicle to alerts, and read alert history and webhook events.
api: openapi/loconav-integration-openapi.yml
operations: [createPolygon, listPolygons, getPolygon, createAlertSubscriptions, getAlertSubscriptions, getAlerts, listAlerts]
---

# Set up geofences and subscribe to alerts

## Auth & conventions
- Header `User-Authentication: <token>`; base URL `https://api.a.loconav.com/integration/api/v1`.
- Paginated listings (`page`, `perPage`); time in epoch seconds; `429` over 500 req/60s.

## Steps
1. `createPolygon` — POST `/polygons` to define a geofence area.
2. `listPolygons` / `getPolygon` — review geofences (`/polygons`, `/polygons/{polygonId}`).
3. `createAlertSubscriptions` — POST `/vehicles/alerts/subscriptions` to enable alerts for a vehicle.
4. `getAlertSubscriptions` — GET `/vehicles/{vehicle_uuid}/alerts/subscriptions` to confirm which alerts are active.
5. `getAlerts` / `listAlerts` — GET `/alerts` or `/vehicles/{vehicleId}/alerts` to read fired alerts.

## Webhooks
LocoNav also POSTs real-time events to your registered receiver URL — e.g. `GeofenceAlert`,
`OverspeedAlert`, `SuddenBrakingAlert`, `AntiTheftAlert`, plus periodic live-location pushes.
See `asyncapi/loconav-webhooks.yml` for the full event catalog (18 events).
