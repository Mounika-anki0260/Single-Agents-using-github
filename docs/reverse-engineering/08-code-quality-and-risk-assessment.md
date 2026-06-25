# Code Quality and Risk Assessment

Observations:
- Project is organized around clear MVC conventions (servlets as controllers, JSPs as views, `models/` for data types).
- Basic security considerations are present: a `SecurityFilter` and `XSSFilter` are declared in `web.xml`.

Risks and technical debt:
- Database: Microsoft Access (`airlines.accdb`) is single-file and not suitable for concurrent, scalable production deployments.
- Session management: `session-timeout` configured as `-1` (infinite) — risk of stale sessions and resource leaks.
- Hardcoded sample credentials in README for `tomcat-users.xml` (sensitive) — must not be used in production, should be masked or managed in secrets store.
- In-memory state: application loads customers/flights/features into `ServletContext` on startup — potential consistency and concurrency issues if multiple app instances or external updates occur.

Security considerations:
- Form authentication with roles is used; ensure TLS is enforced in production.
- Filters exist for security & XSS but audit filter implementations for bypasses and edge cases.

Recommendations (short):
- Migrate DB to a server RDBMS with connection pooling (e.g., PostgreSQL, MySQL) and use a connection pool (e.g., HikariCP).
- Add CSRF protection and enforce secure session timeouts.
- Remove any sample credentials from docs and code; use environment-based secrets.
