# Deployment, CI/CD and Containerization

Recommended pipeline:
- Use GitHub Actions (or Azure Pipelines) to build, test and publish images.
- Build steps: `checkout` -> `maven build` -> `unit tests` -> `docker build` -> `push to registry` -> `deploy`.

Dockerization notes:
- Provide a `Dockerfile` for the Spring Boot backend and a separate `Dockerfile` for worker/adapter.

Example `Dockerfile` (Spring Boot):
```dockerfile
FROM eclipse-temurin:17-jdk-jammy
ARG JAR_FILE=target/app.jar
COPY ${JAR_FILE} /app/app.jar
ENTRYPOINT ["java","-jar","/app/app.jar"]
```

Deployment targets:
- Small teams: Docker Compose for dev and staging.
- Production: Kubernetes (AKS/GKE/EKS) or managed container service; use Helm for manifests.

Secrets and config:
- Use environment variables or platform secret store (Kubernetes Secrets, Azure Key Vault).

Observability & health:
- Expose `/actuator/health` and metrics endpoints. Scrape with Prometheus and visualize in Grafana.
