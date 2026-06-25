# Integrations and Dependencies

Explicit integrations found in code and config:
- UCanAccess JDBC driver (`net.ucanaccess.jdbc.UcanaccessDriver`) for MS Access (see `Project/TurkishAirlines/src/java/SContextListener.java`).
- JAX-WS (reference implementation) used for SOAP webservices: `com.sun.xml.ws.transport.http.servlet.WSServlet` registered in `web.xml` and tested via `Project/WSTester`.
- Filters for security/XSS: `filters.SecurityFilter` and `filters.XSSFilter` (see `Project/TurkishAirlines/src/java/filters/`).

Libraries and folders to check for jars:
- `Project/TurkishAirlines/build/web/WEB-INF/lib/` (packaged webapp libraries)
- `Project/TurkishAirlines/Libs/` (project-level libs)

Operational dependencies (external):
- Apache Tomcat server (deployment and FORM-based auth as shown in README)
- Java 8 (README recommends JDK 8 and NetBeans with Tomcat)

Notes / assumptions:
- Needs confirmation: exact versions of UCanAccess, JAX-WS RI and other jars — check `Project/TurkishAirlines/build/web/WEB-INF/lib/` or `Libs/` directories for JAR filenames.
- Assumption: Email sending is implemented using JavaMail or similar — search for `javax.mail` in the codebase to confirm.
