# Migration Strategy (Access -> Postgres)

## Goals

- Safely migrate data from `airlines.accdb` into Postgres without downtime for read operations and with a controlled cutover for writes.

## Steps

1. Extract schema and data from Access
   - Use `export_access_example.ps1` or ODBC export to CSV/SQL.
   - Create DDL for Postgres based on `tools/migration/schema_postgres.sql`.

2. Create staging Postgres instance
   - Provision a staging DB and load data. Validate types and constraints.

3. Migrate incremental changes
   - For large datasets, use a staged sync (bulk load + delta sync). Use timestamps or change capture where possible.

4. Validate and reconcile
   - Run counts and checksums per table. Validate booking counts, referential integrity, and seat allocations.

5. Cutover
   - Disable writes to Access or run writes to both systems during controlled window.
   - Switch application datasource to Postgres and run smoke tests.

6. Post-cutover monitoring
   - Monitor errors, throughput, and data integrity for several days before deprecating Access.

## Tools & verification

- Use `psql`, `pg_restore`, and verification scripts. Record checksums and counts.
- Keep `tools/migration/schema_postgres.sql` as source-of-truth and update it with discovered schema changes.
