---
name: Manage drivers and vehicle assignment
description: Create, read, update and delete drivers, and assign or unassign a driver to a vehicle.
api: openapi/loconav-integration-openapi.yml
operations: [listDriversFilter, createDrivers, getDriver, updateDrivers, deleteDriver, vehicleAssignment, vehicleUnassignment]
---

# Manage drivers and vehicle assignment

## Auth & conventions
- Header `User-Authentication: <token>` on every call.
- Base URL `https://api.a.loconav.com/integration/api/v1`.
- Listing is paginated (`page`, `perPage`); `401` on bad auth, `429` over 500 req/60s.

## Steps
1. `listDriversFilter` — GET `/drivers?name=&page=&perPage=` to search existing drivers.
2. `createDrivers` — POST `/drivers` with `{name, countryCode, phoneNumber}` to add a driver.
3. `getDriver` — GET `/drivers/{driverId}` to read full profile (license, guarantor, documents).
4. `updateDrivers` — PUT `/drivers/{driverId}` to update name/contact.
5. `vehicleAssignment` — POST `/driver_vehicle_assignments` to bind the driver to a vehicle.
6. `vehicleUnassignment` — PUT `/driver_vehicle_unassignments` to release the binding.
7. `deleteDriver` — DELETE `/drivers/{driverId}` to remove the driver.
