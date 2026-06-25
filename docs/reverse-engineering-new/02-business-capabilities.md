# Business Capabilities

This document maps discovered business features to code locations and key logic.

| Business Capability | Description | Main Files | Key Logic | Notes |
|---|---|---|---|---|
| User login / authentication | Users sign in to access booking features | Project/TurkishAirlines/src/java/LoginManager.java | LoginManager handles credential check and session creation | Needs confirmation of password storage (plain/text vs hashed)
| Search flights | Search available flights by origin/destination/date | Project/TurkishAirlines/web/ShowFlights.jsp, Project/TurkishAirlines/src/java/OriginCompleter.java | Search logic likely in DAO/helper classes in `src/java` | Assumption: flight availability logic in Access DB queries
| Book flight | Select seats and create a booking | Project/TurkishAirlines/web/BookFlight.jsp, SetSeats.jsp, ShowItinery.jsp | Booking persists to DB via manager classes (e.g., CustomerManager.java) | Verify transaction handling
| View current bookings | Users view existing bookings | Project/TurkishAirlines/web/CurrentBooking.jsp | Server-side lookup by user id | 
| Admin approve features/seats | Administrative pages to approve features/seats | Project/TurkishAirlines/web/ApproveFeatures.jsp, ApproveSeats.jsp | Likely protected pages with admin checks | Confirm auth/authorization enforcement

## Business rules / validation (high level)

- Input validation performed server-side in servlet/manager classes and possibly client-side in JSPs.
- Booking likely requires seat availability check before persisting.

## Next steps to complete mapping

- Inspect `Project/TurkishAirlines/src/java` to enumerate exact classes and methods implementing each capability and extract business rules into the `Key Logic` column.
