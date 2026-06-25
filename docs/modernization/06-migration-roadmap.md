# Phased Migration Roadmap & Estimates

This is a pragmatic 6-phase plan to modernize the application while keeping production risk low.

Phase 0 — Preparation (1–2 weeks)
- Inventory code and dependencies (use `docs/reverse-engineering/*`).
- Add automated tests baseline and CI skeleton.

Phase 1 — Backend refactor & APIs (2–4 weeks)
- Implement a Spring Boot backend that exposes REST equivalents to critical servlets (search, book, current bookings, login).
- Keep JSP UI calling new REST endpoints (adapter) so UI remains stable.

Phase 2 — Database migration (2–3 weeks)
- Create Postgres schema, run test imports, and enable dual-write or reconciliation.

Phase 3 — Background processing & email (1–2 weeks)
- Add message queue and worker; offload email sending and heavy processing.

Phase 4 — UI modernization (optional, 2–6 weeks)
- Replace JSP front-end with SPA (React/Vue) or progressively enhance with fetch/ajax to REST.

Phase 5 — Hard cutover & operations (1–2 weeks)
- Switch production to new backend + Postgres, decommission Access DB.

Estimated total: 2–3 months for minimal viable production migration (phases 0–3), depending on team size and QA rigor.

Notes:
- Parallelize tasks where possible (API + DB schema work). Add rollback and testing gates for each phase.
