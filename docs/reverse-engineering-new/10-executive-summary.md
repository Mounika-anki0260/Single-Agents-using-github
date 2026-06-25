# Executive Summary

What the application does:

- A monolithic Java Servlet/JSP web application for flight search and booking. Users can search flights, select seats, and create bookings. Administrative pages allow approving seats/features.

Current architecture:

- Server-rendered JSPs + Java manager/servlet classes backed by an Access DB (development). Ant/NetBeans is used for building and packaging.

Key risks:

- Use of Microsoft Access as datastore — not suitable for production concurrency or scale.
- Lack of automated tests and CI/CD.
- Mixed presentation and business logic reduces maintainability.

Recommended next steps:

1. Extract schema from `airlines.accdb` and migrate to PostgreSQL using `tools/migration/schema_postgres.sql`.
2. Inventory servlets and map endpoints to business capabilities (complete `03-api-endpoints.md`).
3. Add CI: build, static analysis, and test runners.
4. Plan a phased modernization: introduce REST APIs (Spring Boot) and separate frontend, containerize, and add observability.
