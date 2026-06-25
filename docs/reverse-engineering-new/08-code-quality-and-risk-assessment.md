# Code Quality and Risk Assessment

## Observations

- Presentation and logic are mixed (JSPs + server-side Java classes), increasing maintenance cost.
- No obvious unit or integration test suites detected in the main Java webapp.
- Embedded Access DB raises concerns about concurrency, backups, and production-readiness.

| Risk Area | Description | File Path | Severity | Recommendation |
|---|---|---|---|---|
| Datastore | Use of Access DB is not production-grade | Project/TurkishAirlines/src/java/airlines.accdb | High | Migrate to Postgres (use provided schema_postgres.sql)
| Tests | Lack of automated tests | repository root | High | Add unit/integration tests and CI pipeline
| Security | Possible hardcoded config or weak auth handling | Project/TurkishAirlines/src/java/* | Medium | Review credential handling, use hashed passwords and secure config
| Maintainability | JSP/servlet mix increases coupling | Project/TurkishAirlines/web + src/java | Medium | Separate concerns: move to templating/front-end + API backend (Spring)
