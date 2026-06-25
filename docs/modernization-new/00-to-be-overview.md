# To-Be Repository & System Overview

This document describes the recommended To‑Be target for the Flight Booking System based on the reverse engineering findings in `docs/reverse-engineering-new/`.

Goals

- Replace single-file database with a managed RDBMS (Postgres) for scale and reliability.
- Separate concerns: RESTful backend (Spring Boot) and a modern frontend (single-page app or server-side rendered UI) to improve testability and maintainability.
- Add CI/CD, containerization, observability, and secure configuration management.

Key To‑Be characteristics

- Architecture: Modular services (API / Auth / Booking / Catalog) packaged as containers and deployable to Kubernetes or Container Apps.
- Data: Postgres as primary store with migration from `airlines.accdb` using scripts in `tools/migration/`.
- Platform: GitHub Actions for CI, Docker images built in CI and pushed to registry, deployments via declarative IaC (Bicep/Terraform or K8s manifests).
- Observability: Centralized logs and metrics (e.g., Application Insights, Prometheus, Grafana).

Mapping to current repo

- Use `backend-spring/` as starting point for the Spring Boot API; migrate business logic from `Project/TurkishAirlines/src/java/` into service modules.
- Keep `Project/TurkishAirlines/web/` as a migration candidate: either rewrite as React/Angular or convert to server-side templates that call the API.

Assumptions

- Existing business logic is discoverable in `docs/reverse-engineering-new/02-business-capabilities.md` and can be incrementally ported.
- Production environment will not use Access DB; Postgres is acceptable as the target RDBMS.
