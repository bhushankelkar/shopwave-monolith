# ShopWave Monolith

The first phase of [ShopWave](https://github.com/YOUR_USERNAME/shopwave) — a single Spring Boot application implementing the full e-commerce order flow before it gets split into microservices.

## What's inside

- **Auth** — JWT-based registration, login, token refresh
- **Product catalog** — CRUD with proper Postgres indexing
- **Cart** — Redis-backed, TTL-based
- **Orders** — idempotent order placement, transactional consistency
- **Payments** — Stripe integration (test mode), webhook handling
- **Inventory** — optimistic locking to handle concurrent purchase contention
- **Kafka events** — `order.placed` → `payment.confirmed` → `order.confirmed`, consumed by notification and analytics services
- **Saga pattern** — compensating transactions roll back prior steps when a later step in the order flow fails

## Tech stack

- Java 21, Spring Boot 3
- Spring Data JPA + PostgreSQL
- Spring Data Redis
- Spring Kafka
- Spring Security (JWT)
- Stripe Java SDK
- Prometheus + Micrometer, Grafana
- Docker Compose (local dev)

## Running locally

```bash
docker compose up -d      # Postgres, Redis, Kafka, Prometheus, Grafana
mvn spring-boot:run
