# Data Model and Database

## Database technology

- Development appears to use a Microsoft Access file at `Project/TurkishAirlines/src/java/airlines.accdb`.
- Migration helpers and a Postgres schema are provided in `tools/migration/schema_postgres.sql` and related scripts.

## Observed artifacts

| Entity / Table | File Path | Fields | Relationships | Purpose |
|---|---|---|---|---|
| (Unknown - needs extraction) | Project/TurkishAirlines/src/java/airlines.accdb | --- | --- | Stores flights, bookings, customers, seats (assumed from filenames) |

## Important queries and access patterns

- Search by origin/destination for ShowFlights.jsp and related classes.
- Insert/update operations for bookings and seat allocations from booking flows.

## Migration notes

- `tools/migration/schema_postgres.sql` provides a target Postgres schema. Use the PowerShell script `export_access_example.ps1` to export Access DB to a transferable format before importing.

## Next steps

- Extract table definitions from `airlines.accdb` (requires Access/ODBC export or a tool) and populate the Entities table above.
- Generate an ER diagram from extracted schema and include Mermaid ER diagram here.
