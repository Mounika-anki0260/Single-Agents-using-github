# Component Design and Technology Choices

Recommended components and mapping to the existing app:

- Backend API: Spring Boot (Java 17+), replace servlets with REST controllers.
  - Map current servlets to REST endpoints (see `docs/reverse-engineering/03-api-endpoints.md`).
  - Example: `customer.SearchFlights` -> `GET /api/v1/flights?origin=&dest=&date=`.

- Data Layer: PostgreSQL
  - Use a connection pool (HikariCP) and JPA or lightweight DAO layer.
  - Migrate model classes: `models.Customer`, `models.Flight`, `models.Features`, `models.FBS` -> JPA entities.

- Session & Cache: Redis (session store or distributed cache) instead of ServletContext in-memory state.

- Background Workers: lightweight worker (Spring Boot app or Node worker) consuming messages (RabbitMQ or Azure Service Bus) for sending email and long-running tasks.

- Legacy SOAP: keep `WSTester` integration during migration and provide a `SOAP Adapter` microservice that translates SOAP to internal REST calls if needed.

- Auth & Roles: delegate authentication to an IdP (OAuth2/OIDC) or continue using Tomcat-managed roles temporarily.

- UI: Option A — keep server-rendered JSPs during phase 1; Option B — modern SPA (React/Vue) calling REST APIs for phase 2.

Non-functional choices:
- Observability: Prometheus + Grafana or Application Insights; structured logs (JSON) and error tracking (Sentry).
- CI/CD: GitHub Actions (build, test, containerize, push to registry, deploy).
- Container runtime: Docker + Kubernetes (or managed container service).
