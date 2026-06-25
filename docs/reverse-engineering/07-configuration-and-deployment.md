# Configuration and Deployment

Deployment notes (from README and web.xml):

- Application packaged as a standard Java webapp for Apache Tomcat.
- `web.xml` defines servlet mappings, security constraints and FORM-based authentication (see `Project/TurkishAirlines/web/WEB-INF/web.xml`).
- README recommends JDK 8 and NetBeans with Tomcat. The provided sample Tomcat users to enable roles is shown in README (do NOT commit real credentials to Tomcat in production).

Important files and locations:
- `Project/TurkishAirlines/web/WEB-INF/web.xml` — application descriptor and role constraints.
- `Project/TurkishAirlines/src/java/SContextListener.java` — database connection initialization.
- `Project/TurkishAirlines/src/java/airlines.accdb` — embedded DB file loaded at runtime.

Run steps (developer guide excerpt):
1. Install JDK 8 and NetBeans with Tomcat.
2. Add role users to Tomcat `tomcat-users.xml` (example provided in README). Mask or replace sample passwords in real deployments.
3. Open the `Project` folder in NetBeans, run `TurkishAirlines` project. Optionally run `WSTester` to test SOAP endpoints.

Configuration cautions:
- `session-timeout` is set to `-1` in `web.xml` (infinite session lifetime) — revisit for production.
- The app stores DB file inside application code tree; backup and migration strategy required for production.
