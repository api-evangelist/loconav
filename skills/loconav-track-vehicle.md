---
name: Track a vehicle and its telematics
description: Look up a vehicle, read its last-known telematics, distance travelled and timeline, and produce a live-share link.
api: openapi/loconav-integration-openapi.yml
operations: [listVehicles, getVehicleDetails, lastKnown, getDistanceTravelled, getTimeline, getLiveShareLink]
---

# Track a vehicle and its telematics

Use the LocoNav Integration API to find a vehicle and read its position/telematics.

## Auth & conventions
- Send the `User-Authentication: <token>` header on every request (token from your LocoNav SPOC).
- Base URL: `https://api.a.loconav.com/integration/api/v1` (use the regional host for KSA/Oman/Nepal).
- Listing calls are paginated — pass `page` and `perPage`.
- All time parameters (`startTime`, `endTime`) are **epoch seconds**.
- Stay under 500 requests / 60s or you get `429`. A missing/invalid token returns `401`.

## Steps
1. `listVehicles` — list vehicles (paginated) to find the target `vehicleId` / `vehicle_uuid`.
2. `getVehicleDetails` — GET `/vehicles/{vehicleId}` for full vehicle metadata.
3. `lastKnown` — POST `/vehicles/telematics/last_known` to read the latest telematics/position.
4. `getDistanceTravelled` — GET `/vehicles/{vehicleId}/distance_travelled` for a time window (epoch seconds).
5. `getTimeline` — GET `/vehicles/{vehicleId}/timeline` for the movement/stop timeline.
6. `getLiveShareLink` — GET `/vehicles/{vehicleId}/live_share_link` to hand a viewer a live tracking URL.
