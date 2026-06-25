# Repository Overview

- **Repository root:** Flight-Booking-System-JavaServlets_App-master
- **Primary project folder:** Project/TurkishAirlines
- **Support project (web service tester):** Project/WSTester

Purpose: A Java Servlet + JSP based Flight Booking System (Turkish Airlines sample) that demonstrates a small booking workflow with Admin / Manager / Customer roles.

Key technologies (explicitly used in source):
- Java Servlets and JSPs (server-side UI)
- Apache Tomcat deployment (FORM authentication, `tomcat-users.xml` shown in README)
- Microsoft Access database file (`airlines.accdb`) accessed via UCanAccess JDBC driver
- SOAP Web Services (JAX-WS runtime used: com.sun.xml.ws)

Important paths (exact):
- Project/TurkishAirlines/ (main webapp and sources)
- Project/TurkishAirlines/web/ (compiled web content)
- Project/TurkishAirlines/src/java/ (Java source including `models/`, servlets, and `airlines.accdb`)
- Project/WSTester/ (utilities to test SOAP webservices)

Notes / assumptions:
- Assumption: The included `airlines.accdb` is the application database and is packaged with the project at `Project/TurkishAirlines/src/java/airlines.accdb`.
- Needs confirmation: exact list of model class fields and DB schema — see `Project/TurkishAirlines/src/java/models/` for source.
