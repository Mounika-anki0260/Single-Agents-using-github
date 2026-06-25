# API Endpoints and Servlet Routes

Below are the primary servlets and their URL mappings as defined in `Project/TurkishAirlines/web/WEB-INF/web.xml`.

- `ChangeFeatures` -> `/ChangeFeatures.do` (servlet class: `admin.ChangeFeatures`)
- `ApproveFeatures` -> `/ApproveFeatures.do` (servlet class: `manager.ApproveFeatures`)
- `DisapproveFeatures` -> `/DisapproveFeatures.do` (servlet class: `manager.DisapproveFeatures`)
- `SetSeats` -> `/SetSeats.do` (servlet class: `admin.SetSeats`)
- `ApproveSeats` -> `/ApproveSeats.do` (servlet class: `manager.ApproveSeats`)
- `DisapproveSeats` -> `/DisapproveSeats.do` (servlet class: `manager.DisapproveSeats`)
- `LoginManager` -> `/Login` (servlet class: `LoginManager`)
- `LogoutManager` -> `/Logout` (servlet class: `LogoutManager`)
- `CustomerManager` -> `/BookFlight`, `/CurrentBooking` (servlet class: `CustomerManager`)
- `SearchFlights` -> `/SearchFlights.do` (servlet class: `customer.SearchFlights`)
- `ChooseFlight` -> `/ChooseFlight.do` (servlet class: `customer.ChooseFlight`)
- `CurrentBooking` -> `/CurrentBooking.do` (servlet class: `customer.CurrentBooking`)
- `BookFlight` -> `/BookFlight.do` (servlet class: `customer.BookFlight`)
- `OriginCompleter` -> `/OriginCompleter` (servlet class: `OriginCompleter`)
- SOAP endpoint (JAX-WS servlet) `PriceAndSeats` -> `/PriceAndSeats` (JAX-WS servlet `com.sun.xml.ws.transport.http.servlet.WSServlet`)

Security constraints (role-based) are also declared in `web.xml` and restrict access to admin/manager/customer resources. See the file `Project/TurkishAirlines/web/WEB-INF/web.xml` for the exact `url-pattern` and `security-constraint` blocks.
