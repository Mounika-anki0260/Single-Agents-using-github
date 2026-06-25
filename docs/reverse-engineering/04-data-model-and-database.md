# Data Model and Database

Database:
- The application uses a bundled Microsoft Access file located at: `Project/TurkishAirlines/src/java/airlines.accdb`.
- `SContextListener` opens the DB with UCanAccess: `net.ucanaccess.jdbc.UcanaccessDriver` and sets the connection into the ServletContext attribute `con` (see `Project/TurkishAirlines/src/java/SContextListener.java`).

Model classes:
- Java model classes live under `Project/TurkishAirlines/src/java/models/` — these include `Customer`, `FBS`, `Flight`, `Features` (referenced from `SContextListener`).
- The `FBS` model is responsible for bootstrapping application data at startup (`populateFeatures`, `populateCustomers`, `getAllFlights`).

Schema details and limitations:
- Needs confirmation: exact table and field names inside `airlines.accdb`. Inspect `Project/TurkishAirlines/src/java/models/` to extract field-to-column mappings.
- Risk: Microsoft Access (single-file DB) is not suitable for multi-user, high-concurrency or cloud deployment. Consider migrating to a server RDBMS for production.

Runtime data flow:
- On startup `SContextListener` populates `ServletContext` attributes: `features`, `fbs`, `flights`, `customers` for in-memory use by servlets and JSPs.
