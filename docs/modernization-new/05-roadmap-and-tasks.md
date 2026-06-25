# Roadmap and Tasks

This roadmap maps the Re-Architecture Plan into milestones and actionable tasks.

Quarter 0 — Preparation (2–4 weeks)

- Inventory code (complete `docs/reverse-engineering-new/03-api-endpoints.md`).
- Extract DB schema and run sample migration to Postgres (`tools/migration/`).
- Add basic CI that builds the project.

Quarter 1 — Backend API & Data (4–8 weeks)

- Implement Spring Boot API for core capabilities (login, search, booking).
- Port business logic and add unit tests.
- Run staging migration to Postgres and validate data.

Quarter 2 — Frontend & Cutover (4–8 weeks)

- Migrate or rewrite frontend to call APIs.
- Perform controlled cutover to Postgres in staging and then production.

Quarter 3 — Harden & Scale (ongoing)

- Add autoscaling, observability, backup/DR, and performance tuning.

Owners and checkpoints

- Engineering lead: owns architecture decisions and cutover windows.
- QA: prepares integration tests and data validation scripts.
- DevOps: CI, Docker registry, and deployment manifests.

Deliverables

- Working Spring Boot APIs in `backend-spring/` with test coverage.
- Postgres instance seeded with migrated data.
- CI pipeline, Docker images, and deployment manifests.
