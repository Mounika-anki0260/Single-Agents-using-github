# Deployment and CI/CD Blueprint

## CI pipeline (recommended)

- On push or PR to `main`:
  - Checkout
  - Build: `ant clean && ant build`
  - Static analysis: run a Java linter / SpotBugs if added
  - Unit tests: run JUnit (after migrating tests)
  - Build Docker image and push to registry

Example GitHub Actions snippet (conceptual):

```yaml
name: CI
on: [push, pull_request]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Set up JDK
        uses: actions/setup-java@v4
        with:
          distribution: 'temurin'
          java-version: '17'
      - name: Build (Ant)
        run: ant clean build
      - name: Build Docker image
        run: docker build -t ghcr.io/${{ github.repository }}/flight-app:${{ github.sha }} .
      - name: Push image
        run: docker push ghcr.io/${{ github.repository }}/flight-app:${{ github.sha }}
```

## Dockerfile (guidance)

- Start from an OpenJDK runtime image, copy the WAR, and run via `java -jar` (or run embedded server if packaging as Spring Boot).

## Deployment

- Deploy to Kubernetes, Azure Container Apps, or App Service for Containers. Use image tags and manifests stored in repo.
- Use secrets manager for DB credentials, and use readiness/liveness probes.
