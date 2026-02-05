---
name: backend-engineer
description: Build and maintain the NestJS backend for the project. Use this skill when the user needs API endpoints, database schema, payment integration, email automation, order management, reporting, or any server-side logic. Stack is NestJS (TypeScript) with SQLite via TypeORM.
---

This skill guides backend development using NestJS + TypeScript + SQLite/TypeORM. Read `requirements.md` at the project root and the existing codebase to understand what to build. Derive all structure, schema, and endpoints from the actual requirements — never from a preset template.

## Approach

1. **Read requirements first** — understand what the feature needs before writing any code
2. **Check existing code** — find existing modules, entities, and patterns in the codebase. Follow them.
3. **Design from the domain** — entities, endpoints, and modules should reflect what the requirements describe, not a generic boilerplate
4. **Implement incrementally** — one module or feature at a time, tested before moving on

## Architecture Principles

- **One module per domain** — group related controllers, services, and entities together
- **Thin controllers** — controllers handle HTTP concerns only. Business logic lives in services.
- **DTOs for all input** — validate with `class-validator`, transform with `class-transformer`
- **Entities reflect the domain** — derive columns and relationships from what the requirements actually need, not from assumptions
- **Keep it flat** — avoid deep nesting or over-abstraction. Add structure only when complexity demands it.

## Database (SQLite + TypeORM)

- Enable WAL mode for better concurrent read performance
- Use TypeORM migrations for schema changes — never modify the DB manually
- Seed data through dedicated seed scripts when initial data is needed
- Store the DB file outside the repo (gitignored)
- Design schema from requirements — only create the entities and columns that are needed
- If the project outgrows SQLite, the TypeORM abstraction makes migration to PostgreSQL straightforward

## API Design

- RESTful conventions: proper HTTP verbs, status codes, and resource naming
- Consistent error shape across all endpoints (statusCode, message, error)
- Paginate list endpoints — never return unbounded collections
- Swagger/OpenAPI documentation via `@nestjs/swagger`
- Separate public and admin endpoints — admin routes require JWT authentication
- Webhook endpoints verify signatures before processing and return 200 immediately

## Payment Integration

- Create/initiate payment on the server, return client token or redirect URL to frontend
- Verify payment completion exclusively through webhook callbacks — never trust client-side confirmation
- Verify webhook signatures using raw body (not parsed JSON)
- Implement idempotency — duplicate webhooks must not create duplicate records
- Store the payment provider's transaction ID for reconciliation
- Handle failure gracefully — update order status and trigger appropriate notifications

## Email

- Use templates (Handlebars or similar) for transactional emails
- Support both HTML and plain-text versions
- Trigger emails from service layer events, not controllers
- Always include essential context in emails (order number, product, amount, support contact)

## Security

- Helmet for HTTP headers
- CORS restricted to allowed origins
- Rate limiting on public endpoints
- Webhook endpoints verify provider signatures
- Admin endpoints protected by JWT
- Secrets in `.env`, never committed
- Sanitize all user input
- Never expose internal details in error messages

## Testing

- Unit test services with mocked dependencies
- E2E test critical flows (order creation, payment webhooks, auth)
- Use `@nestjs/testing` for dependency injection in tests
