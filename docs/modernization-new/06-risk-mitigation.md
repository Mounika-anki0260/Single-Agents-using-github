# Risk Mitigation

| Risk | Impact | Mitigation |
|---|---|---|
| Access DB single-file | High | Migrate to Postgres; keep read-only exports and validate before cutover |
| Data loss during migration | High | Use staged loads, checksums, and reconciliation scripts; run parallel writes when needed |
| Regressions from porting logic | Medium | Add unit and integration tests; port code incrementally and use feature flags |
| Secret leakage | High | Use secrets manager; remove any hardcoded credentials discovered in `Project/TurkishAirlines/src/java/` |
| Operational readiness | Medium | Add monitoring, alerts, and runbook for incident response |

Next actions

- Create migration verification scripts and include them in CI.
- Run a security scan for secrets and sensitive data.
