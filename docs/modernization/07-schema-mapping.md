# Model → Database Column Mapping

This document maps the Java model fields (from `Project/TurkishAirlines/src/java/models/`) to the existing Microsoft Access column names (observed in `FBS` queries) and shows an appropriate Postgres type for the migration.

Customers
- Java class: `models.Customer` (extends `Person`)
  - `name` -> Access column: `name` -> Postgres: `TEXT`
  - `email` -> Access column: `email` -> Postgres: `TEXT` (unique)

Features
- Java class: `models.Features`
  - `isChanged` (static) -> Access: `isChanged` -> Postgres: `BOOLEAN`
  - `type` -> Access: `type` -> Postgres: `INT`
  - `price` -> Access: `price` -> Postgres: `INT`
  - `newPrice` -> Access: `newPrice` -> Postgres: `INT`
  - `seatPitch` -> Access: `seatPitch` -> Postgres: `DOUBLE PRECISION`
  - `seatWidth` -> Access: `seatWidth` -> Postgres: `DOUBLE PRECISION`
  - `newSeatPitch` -> Access: `NewSeatPitch` -> Postgres: `DOUBLE PRECISION`
  - `newSeatWidth` -> Access: `NewSeatWidth` -> Postgres: `DOUBLE PRECISION`
  - `videoType` -> Access: `VideoType` -> Postgres: `TEXT`
  - `newVideoType` -> Access: `NewVideoType` -> Postgres: `TEXT`
  - `seatType` -> Access: `SeatType` -> Postgres: `TEXT`
  - `newSeatType` -> Access: `NewSeatType` -> Postgres: `TEXT`
  - `powerType` -> Access: `PowerType` -> Postgres: `TEXT`
  - `newPowerType` -> Access: `NewPowerType` -> Postgres: `TEXT`
  - `wifi` -> Access: `Wifi` -> Postgres: `TEXT`
  - `newWifi` -> Access: `NewWifi` -> Postgres: `TEXT`
  - `specialFood` -> Access: `SpecialFood` -> Postgres: `TEXT`
  - `newSpecialFood` -> Access: `NewSpecialFood` -> Postgres: `TEXT`

Flights
- Java class: `models.Flight`
  - `isChanged` -> Access: `isChanged` -> Postgres: `BOOLEAN`
  - `flightName` -> Access: `FlightName` -> Postgres: `TEXT` (unique)
  - `totalSeats` -> Access: `TotalSeats` -> Postgres: `INT`
  - `currentSeats` -> Access: `CurrentSeats` -> Postgres: `INT`
  - `departureCity` -> Access: `DepartureCity` -> Postgres: `TEXT`
  - `arrivalCity` -> Access: `ArrivalCity` -> Postgres: `TEXT`
  - `departureDate` -> Access: `DepartureDate` -> Postgres: `TIMESTAMP`
  - `arrivalDate` -> Access: `ArrivalDate` -> Postgres: `TIMESTAMP`
  - `economySeats` -> Access: `EconomySeats` -> Postgres: `INT`
  - `businessSeats` -> Access: `BusinessSeats` -> Postgres: `INT`
  - `firstSeats` -> Access: `FirstSeats` -> Postgres: `INT`
  - `oldESeats` -> Access: `OldESeats` -> Postgres: `INT`
  - `oldBSeats` -> Access: `OldBSeats` -> Postgres: `INT`
  - `oldFSeats` -> Access: `OldFSeats` -> Postgres: `INT`
  - `oldTSeats` -> Access: `OldTSeats` -> Postgres: `INT`

Seats
- Java class: `models.Seat`
  - `seatNumber` -> Access: `SeatNumber` -> Postgres: `INT`
  - `flight` (reference) -> Access: `flightName` (used in Seats query) -> Postgres: `flight_id` (FK to `flights`)
  - `Customer` reference -> Access: `CustomerEmail` -> Postgres: `customer_id` (FK to `customers`)
  - `FeatureType` -> Access: `FeatureType` -> Postgres: `TEXT` (or FK to `features.type`)

Cities
- Access table `CITIES` with column `CITYNAME` -> Postgres: `cities(city_name TEXT)`

Import tips
- Preserve Access column names when exporting CSV to minimize mapping changes during `COPY`.
- Recommended CSV headers: use exact Access column names (`FlightName`, `TotalSeats`, etc.).

Validation queries
- Row counts: `SELECT COUNT(*) FROM Flights;` vs Access counts.
- Spot-check prices: `SELECT price FROM Features WHERE type = 0;` should match Access.
