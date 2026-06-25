# Security and Operations Recommendations

Key security improvements:
- Use TLS everywhere (HTTPS enforced at load balancer) and redirect all HTTP.
- Replace Tomcat `tomcat-users.xml` sample credentials with an IdP (OIDC) or integrate with enterprise SSO.
- Store secrets in a vault, never in repo or README.
- Set a reasonable `session-timeout` and store sessions in Redis when scaling.
- Add CSRF protection (Spring Security provides this by default for form flows).

Operational recommendations:
- Add centralized logging (structured JSON) and correlation IDs for traces.
- Add health probes and readiness checks for containers.
- Schedule DB backups and define RTO/RPO for production DB.

Audit & compliance:
- Mask PII in logs and ensure email templates comply with privacy requirements.
