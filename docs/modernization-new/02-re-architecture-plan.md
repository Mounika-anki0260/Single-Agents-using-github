# Re-Architecture Plan (phased)

This plan describes a pragmatic, low-risk path to move from the current monolith to the To‑Be architecture.

Phase 0 — Discovery & Safety

- Inventory servlets, JSPs, and manager classes (`Project/TurkishAirlines/src/java/`) and finalize `docs/reverse-engineering-new/03-api-endpoints.md`.
- Extract DB schema from `airlines.accdb` and create CI-validated migration scripts.

Phase 1 — Stabilize and Modernize DevOps

- Add GitHub Actions that run build (`ant`), static analysis, and unit tests.
- Add a Dockerfile and make Ant produce a container image for the app or migrate build to Maven/Gradle for modern toolchains.

Phase 2 — Backend API First

- Create a Spring Boot API module (use `backend-spring/` as base). Implement API endpoints that mirror current servlets. Keep JSP UI pointing to new API endpoints for gradual cutover.
- Port business logic to service-layer classes; add unit tests for each capability.

Phase 3 — Data Migration & Cutover

- Run incremental data migration from Access -> Postgres. Validate referential integrity and sample data correctness.
- Switch runtime datasource to Postgres in staging; run integration tests.

Phase 4 — Frontend Modernization

- Option A: Rebuild UI as SPA (React/Vue) that calls API.
- Option B: Convert JSPs to lightweight templating that consumes API data.

Phase 5 — Harden & Operate

- Add autoscaling, observability, backup/restore, DR plan, and security hardening.
- Migrate to K8s or host on managed container service.

Rollback & mitigation

- Deploy new services behind feature flags. Keep monolith available for rollback. Use DB replicas and transactional sync for cutover.
