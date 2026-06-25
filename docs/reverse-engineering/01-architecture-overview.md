# Architecture Overview

- Architectural style: Traditional server-side MVC using Java Servlets (controllers) + JSPs (views) + model classes in `Project/TurkishAirlines/src/java/models/`.
- Servlet container: Apache Tomcat (FORM authentication configured in `web.xml`).
- Application context initialization: `SContextListener` (`Project/TurkishAirlines/src/java/SContextListener.java`) loads the `airlines.accdb` via UCanAccess and places objects in `ServletContext`.

Key runtime components (exact files):
- Servlet mappings and security constraints: `Project/TurkishAirlines/web/WEB-INF/web.xml` (see servlet->url-pattern mappings).
- Context listener + DB connection: `Project/TurkishAirlines/src/java/SContextListener.java`.
- Security and XSS filters: `filters.SecurityFilter` and `filters.XSSFilter` (filter classes present under `Project/TurkishAirlines/src/java/filters/` — see code).

Data access pattern:
- Uses embedded Microsoft Access file (`airlines.accdb`) accessed with `net.ucanaccess.jdbc.UcanaccessDriver` created in `SContextListener` and stored as `ServletContext` attribute `con`.

External runtime: JAX-WS servlet (SOAP) registered as `PriceAndSeats` using `com.sun.xml.ws.transport.http.servlet.WSServlet` in `web.xml`.
