# Milestone status

| Milestone | Scope | Status |
|---|---|---|
| M1 | Java 21 Spring Boot services and REST CRUD | Implemented starter |
| M2 | React TypeScript store/seller/admin screens | Implemented demo UI |
| M3 | Kafka order/inventory event flow | Implemented starter |
| M4 | Transactional outbox on order creation | Implemented basic poller; multi-replica safety requires improvement |
| M5 | OAuth2/OIDC and role-based security | Keycloak container only; integration pending |
| M6 | Kafka retries, DLT, idempotency | Inventory deduplication basic; retries/DLT pending |
| M7 | Unit, integration, E2E tests | Pending |
| M8 | Docker Compose local stack | Configured; unverified |
| M9 | Kubernetes deployment | Sample manifests; image registry/secrets pending |
| M10 | CI/CD | Build workflow starter; deployment pending |
| M11 | Metrics, logs and traces | Prometheus/Grafana starter; tracing pending |
| M12 | AWS/Azure/GCP production rollout | Architecture notes only; pending |

## Production gaps
- Authentication and authorization not enforced; APIs use permissive CORS for local demo.
- Services share one PostgreSQL database; separate service schemas/databases in production.
- Outbox publisher holds a database lock while waiting for Kafka; implement lease/claim batching and publisher concurrency handling.
- Inventory's event publication is not transactional with its database update; add an inventory outbox.
- No Kafka retry/DLT policy, schema registry, automated tests, or verified deployment.
- Keycloak needs a configured realm/client, token validation, and role mapping.
- Do not expose this starter publicly without completing security hardening.
