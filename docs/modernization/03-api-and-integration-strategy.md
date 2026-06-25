# API & Integration Migration Strategy

Principles:
- Design RESTful, versioned APIs (`/api/v1/...`) matching current servlet responsibilities.
- Preserve existing behavior and URLs with an API Gateway mapping layer during migration.

Mapping examples (current servlet -> REST):
- `LoginManager` (`/Login`) -> `POST /api/v1/auth/login` (returns token or sets secure cookie)
- `SearchFlights.do` -> `GET /api/v1/flights` with query params
- `BookFlight.do` -> `POST /api/v1/bookings`

Legacy SOAP handling:
- Option A: Implement a SOAP adapter service that forwards SOAP requests to the REST backend (keeps `WSTester` working).
- Option B: Replace SOAP with REST on integration partners once both sides agree.

Email and asynchronous flows:
- Use message queue (RabbitMQ or cloud equivalent) for sending emails and inventory updates. Bookings push a message; worker sends email and updates audit logs.

Compatibility and incremental rollout:
- Start by exposing REST endpoints while keeping JSP UI working (backend in-place adapter layer).
- Add feature flags to toggle new endpoints for user groups.
