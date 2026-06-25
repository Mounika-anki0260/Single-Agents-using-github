# Repository Overview

Project: Flight-Booking-System-JavaServlets_App

## Project summary

This repository contains a Java-based flight booking application implemented as a traditional Java Servlet / JSP webapp (NetBeans/Ant project layout) along with auxiliary migration and tooling scripts. The app appears to be a monolithic web application that renders JSP pages and uses server-side Java classes for business logic.

## Technology stack (observed)

- Java Servlets and JSP (presentation + controllers)
- Ant / NetBeans project files (`build.xml`, `nbproject/`)
- Microsoft Access database file (`airlines.accdb`) with migration helpers to PostgreSQL under `tools/migration`
- Shell/PowerShell and SQL migration scripts
- A `backend-spring/` folder exists (likely a modernization or parallel backend)

## Repository structure (top-level)

- Project/: contains the NetBeans web application projects (e.g., `TurkishAirlines/`, `WSTester/`)
- backend-spring/: Spring-based backend sources (separate module)
- docs/: modernization and reverse-engineering notes
- tools/migration/: scripts to export Access and import to PostgreSQL

## Main folders and purpose

- Project/TurkishAirlines/: Main webapp sources and build output (JSPs, Java sources, libs)
- Project/TurkishAirlines/src/java/: Server-side Java classes (business logic / managers / servlets)
- Project/TurkishAirlines/web/: JSP pages and web assets
- tools/migration/: `export_access_example.ps1`, `schema_postgres.sql`, `import_postgres_example.sql`
- backend-spring/: Spring project (investigate for migration path)

## Key files and configurations

- [Project/TurkishAirlines/web/](Project/TurkishAirlines/web/) - user-facing JSPs
- [Project/TurkishAirlines/src/java/airlines.accdb](Project/TurkishAirlines/src/java/airlines.accdb) - embedded Access DB file
- `build.xml`, `nbproject/project.xml` - NetBeans/Ant build configuration
- `tools/migration/schema_postgres.sql` - target Postgres schema

## Application startup flow (high level)

1. Application is deployed as a WAR (Ant/NetBeans build) to a Java servlet container (Tomcat/GlassFish).
2. User requests are served by JSP pages and backing Java classes (servlets / manager classes) present in `Project/TurkishAirlines/src/java`.
3. Data is read from the embedded Access DB (development) or from whatever JDBC datasource is configured in deployment.

## Assumptions / Items to confirm

- Assumption: The Access DB (`airlines.accdb`) is the development data source. Confirm production DB and connection details.
- Needs confirmation: Exact servlet mapping and `web.xml` entry points (search `WEB-INF/web.xml`).
