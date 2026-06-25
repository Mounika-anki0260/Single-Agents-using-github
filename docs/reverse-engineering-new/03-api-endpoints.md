# API Endpoints and Routes

This repository is a server-rendered JSP/Servlet web application. The "endpoints" are JSP pages and servlets defined in Java classes and possibly mapped in `WEB-INF/web.xml`.

| Method | Endpoint / Interface | File Path | Handler / Function | Purpose | Request | Response |
|---|---:|---|---|---|---|---|
| GET/POST | /ShowFlights.jsp | Project/TurkishAirlines/web/ShowFlights.jsp | Backing servlet/manager (search handler) | Display flight search results | form params: origin/destination/date | HTML page with results |
| GET/POST | /BookFlight.jsp | Project/TurkishAirlines/web/BookFlight.jsp | Booking manager class | Start booking flow | form params: flightId, passenger data | Booking form / confirm |
| GET/POST | /Login.jsp (or LoginManager) | Project/TurkishAirlines/src/java/LoginManager.java and JSPs | LoginManager | Authenticate users | credentials | session + redirect |

Notes:
- Exact servlet URL mappings are in `WEB-INF/web.xml` or in `@WebServlet` annotations. Search for `web.xml` and `@WebServlet` to enumerate precise routes.
- For every servlet class in `Project/TurkishAirlines/src/java`, add a row to this table mapping the URL to handler method.
