# Integrations and Dependencies

## External integrations (observed)

- Database: Microsoft Access (`airlines.accdb`) in development; target migration to PostgreSQL (`tools/migration/schema_postgres.sql`).
- No cloud APIs, payment providers, or third-party SaaS integrations were obvious from a top-level scan.

## Libraries and frameworks

- Java Servlet API / JSP
- Project-specific libraries in `Project/TurkishAirlines/Libs/` (inspect for exact JARs)

| Integration / Dependency | Type | File Path | Purpose | Risk / Notes |
|---|---|---|---|---|
| airlines.accdb | Datastore (Access) | Project/TurkishAirlines/src/java/airlines.accdb | Stores flights/bookings data | High risk for concurrency/scaling
| tools/migration/schema_postgres.sql | Migration script | tools/migration/schema_postgres.sql | Target Postgres schema | Good starting point for migration

## Environment variables / config

- No clear `.env` or properties files were at repo root. Look for JDBC connection properties inside `web/WEB-INF` or Java source files.

## Next steps

- List exact JAR dependencies in `Project/TurkishAirlines/Libs/` and record versions.
- Search for external endpoint URLs and credentials (mask any secrets).
