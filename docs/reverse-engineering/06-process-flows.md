# Process Flows

1) Customer booking flow (high-level):
   - Customer visits `home.jsp` -> uses `SearchFlights` (`/SearchFlights.do`) to filter flights.
   - Customer picks a flight (`ChooseFlight.do`), views itinerary (`ShowItinery.jsp`), proceeds to `BookFlight`.
   - Payment is simulated in UI; on confirmation servlet marks seat as sold and application updates in-memory state (via `FBS` / models).
   - System sends email with itinerary (see implementation paths for mail).

2) Admin / Manager approval flow:
   - Admin logs in -> `LoginManager` redirects Admin to `ChangeFeatures.jsp` and `SetSeats.jsp` to create/update prices and seat counts.
   - Manager logs in -> `ApproveFeatures.jsp` and `ApproveSeats.jsp` to accept or reject admin changes. Approval toggles availability for customers.

3) Startup flow:
   - `SContextListener` runs on application start, loads `airlines.accdb` and populates `features`, `customers`, `flights`, `fbs` into `ServletContext`.

Files with flow logic:
- `Project/TurkishAirlines/src/java/SContextListener.java`
- Servlet controllers in `Project/TurkishAirlines/src/java/` and subpackages (`admin/`, `manager/`, `customer/`)
