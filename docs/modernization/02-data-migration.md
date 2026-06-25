# Data Migration Plan (MS Access -> PostgreSQL)

Objective: Safely move `airlines.accdb` data into Postgres with minimal downtime.

Steps:
1. Inventory schema
   - Inspect `Project/TurkishAirlines/src/java/models/` to extract field-to-column mappings.
   - Optionally open `airlines.accdb` in MS Access or use `mdb-tools` to list tables.

2. Create Postgres schema
   - Design normalized tables: `customers`, `flights`, `features`, `bookings`, `seat_inventory`, `audit_logs`.

3. Export data from Access
   - Use UCanAccess or `mdb-export` to dump CSVs per table.
   - Example (Linux with mdb-tools):
```bash
mdb-export airlines.accdb Customers > customers.csv
mdb-export airlines.accdb Flights > flights.csv
```

4. Load into Postgres
   - Create tables and use `COPY` or `psql --	csv` to load CSVs. Cleanse data during import.

5. Validation
   - Run counts and spot-check records. Add integrity checks.

6. Cutover strategy
   - Phase 1 (dual-read): Keep Access file as read-only; write new bookings into Postgres only. Run reconciliation job nightly.
   - Phase 2 (final cutover): Migrate remaining deltas and switch backend to Postgres.

7. Rollback plan
   - Keep Access backup and move Postgres import scripts into version control so revert is possible.

Tools & scripts to add into repo:
- `tools/migration/export_access.sh` — CSV export helper.
- `tools/migration/import_postgres.sql` — table DDL + COPY commands.

Files added in this workspace:
- `tools/migration/schema_postgres.sql` (DDL draft aligned to Access column names)
- `tools/migration/import_postgres_example.sql` (COPY placeholders)
- `tools/migration/export_access_example.ps1` (Windows PowerShell example placeholder)
- `docs/modernization/07-schema-mapping.md` (field-to-column mapping and import tips)
