# To‑Be Architecture Overview

This document proposes a practical, low-risk re-architecture of the existing `Project/TurkishAirlines` monolithic JavaServlet + JSP app into a modern, maintainable platform.

Goals:
- Improve reliability and concurrency by replacing MS Access single-file DB with a managed RDBMS.
- Decouple UI from backend with an API-first design.
- Enable repeatable builds and deployments via containers and CI/CD.
- Improve security, observability and testability.

High-level To‑Be architecture (logical):

```mermaid
graph LR
  Browser[Customer/Admin/Manager Browser]
  Browser -->|HTTPS| API_GW[API Gateway / Load Balancer]
  API_GW --> Backend_API[Backend API (stateless) - Spring Boot]
  Backend_API --> Auth[Auth Service / IdP]
  Backend_API --> DB[(Postgres)]
  Backend_API --> MQ[(Message Queue - e.g., RabbitMQ)]
  MQ --> EmailSvc[Email Worker]
  Backend_API --> SOAP_Legacy[Optional SOAP Adapter]
```

Key principles:
- Backend services are stateless and horizontally scalable. Session state stored in Redis or JWT depending on requirements.
- Data stored in Postgres with migration from `airlines.accdb`.
- Background processing (email, heavy jobs) moved to workers consuming a message queue.
- Legacy SOAP endpoints can be preserved behind an adapter layer during migration.

Files for reference from current repo: `docs/reverse-engineering/*`, `Project/TurkishAirlines/web/WEB-INF/web.xml`, `Project/TurkishAirlines/src/java/SContextListener.java`.
