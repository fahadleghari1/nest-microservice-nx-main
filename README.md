# NestJS Microservices with Nx

A monorepo scaffold for a NestJS-based microservices architecture, managed with [Nx](https://nx.dev). It currently contains an API gateway and two backend services, each independently runnable and testable through the Nx workspace.

## Tech stack

**Implemented today**

- [Nx](https://nx.dev) monorepo (v21) — workspace orchestration, task running, and code generation
- [NestJS](https://nestjs.com) (v11) — service framework
- TypeScript 5.9
- [SWC](https://swc.rs) — fast build/transpile for dev and test
- Jest 30 — unit testing
- ESLint 9 + Prettier — linting and formatting
- Webpack — production builds for each service

**Planned / on the roadmap**

- [Prisma](https://www.prisma.io) ORM
- PostgreSQL as the primary database
- Redis for caching
- Apache Kafka for inter-service messaging
- Centralized authentication/authorization across services
- Shared library of common DTOs, guards, and interceptors

## Project structure

```
apps/
  api-gateway/         # Entry point for external traffic (port 6000)
  api-gateway-e2e/
  auth-service/         # Auth service (port 6001)
  auth-service-e2e/
  user-service/         # User service (port 6002)
  user-service-e2e/
packages/               # Shared/publishable libraries (empty so far)
```

## Features

**Current state**

- Three independently deployable NestJS apps scaffolded via Nx generators
- Each service exposes a placeholder `GET /api` endpoint
- E2E test projects wired up for each service
- Shared Nx task pipeline for build, serve, lint, and test across all apps

**Planned**

- Auth service: user registration/login, token issuance and validation
- User service: user profile and account management
- API gateway: request routing and auth enforcement for downstream services
- Inter-service communication via Kafka and/or Redis pub/sub
- Persistent storage via Prisma + PostgreSQL

## Prerequisites

- Node.js 20+
- npm

## Setup

```sh
# Install dependencies
npm install
```

## Running the services

Serve a single service:

```sh
npx nx serve api-gateway
npx nx serve auth-service
npx nx serve user-service
```

Serve all services at once:

```sh
npx nx run-many -t serve --all
```

Default ports (each prefixed with `/api`):

| Service       | Port | URL                          |
| ------------- | ---- | ----------------------------- |
| api-gateway   | 6000 | http://localhost:6000/api     |
| auth-service  | 6001 | http://localhost:6001/api     |
| user-service  | 6002 | http://localhost:6002/api     |

## Building

```sh
npx nx build <project-name>
```

## Testing

```sh
# Unit tests for a single project
npx nx test <project-name>

# Unit tests for all projects
npx nx run-many -t test --all

# End-to-end tests
npx nx e2e api-gateway-e2e
npx nx e2e auth-service-e2e
npx nx e2e user-service-e2e
```

## Linting

```sh
npx nx lint <project-name>
```

## Generating new code

Generate a new app:

```sh
npx nx g @nx/nest:app apps/<service-name>
```

Generate a shared library:

```sh
npx nx g @nx/js:lib packages/<lib-name>
```

## Screenshots

_Coming soon — screenshots will be added once the API gateway and services have real endpoints and/or Swagger docs to show._

## Learn more

- [Nx documentation](https://nx.dev)
- [NestJS documentation](https://docs.nestjs.com)
