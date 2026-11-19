# E-commerce Kafka Capstone (runnable starter)

Java 21, Spring Boot 3.3, React/TypeScript, PostgreSQL, Kafka (KRaft), Docker Compose.

## Run
`docker compose up --build`

Frontend: http://localhost:5173 | Orders API: http://localhost:8081 | Inventory API: http://localhost:8082

Use the frontend to create an order. Order service persists PENDING, publishes `order.created` after commit, inventory consumes and publishes `inventory.reserved` or `inventory.rejected`; order service updates the status. The starter uses an in-memory processed-event table for idempotency backed by PostgreSQL. Kafka publication after DB commit is **not atomic**: for production, implement a transactional outbox and CDC/poller. The frontend polls order status.

## Quick test
`curl -X POST http://localhost:8081/api/orders -H 'Content-Type: application/json' -d '{"sku":"SKU-1","quantity":2}'`

Seed stock: SKU-1 = 100. Open http://localhost:5173 to view the UI.

## Next production milestones
- Auth/OIDC (Keycloak), API gateway, roles, product catalog, seller portal, admin dashboard
- Outbox and inbox patterns, DLQ/retry policies, Kafka schema registry, observability
- Testcontainers integration tests, Kubernetes manifests, Helm, CI/CD, Terraform
- Payment integration deliberately deferred

This is a **working vertical slice**, not a completed production e-commerce platform. No payment, authentication or API gateway is implemented yet.
