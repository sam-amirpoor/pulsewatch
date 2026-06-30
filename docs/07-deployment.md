# Deployment Guide

## Introduction

This document describes how PulseWatch can be deployed in different environments.

The project is designed with production readiness in mind while keeping the deployment process simple.

---

# Deployment Architecture

The application consists of two independent services.

```text
Frontend (Next.js)
        │
        ▼
REST API
        │
        ▼
Backend (NestJS)
        │
        ▼
PostgreSQL
```

Future versions may introduce additional services such as Redis and Queue Workers.

---

# Environments

The project supports multiple environments.

## Development

Used during local development.

Characteristics:

- Local PostgreSQL
- Hot Reload
- Debugging enabled
- Development configuration

---

## Production

Used for public deployment.

Characteristics:

- Optimized build
- Secure environment variables
- HTTPS
- Reverse proxy
- Production database

---

# Environment Variables

Backend requires the following environment variables.

| Variable          | Description        |
| ----------------- | ------------------ |
| PORT              | Application port   |
| DATABASE_HOST     | PostgreSQL host    |
| DATABASE_PORT     | PostgreSQL port    |
| DATABASE_NAME     | Database name      |
| DATABASE_USER     | Database username  |
| DATABASE_PASSWORD | Database password  |
| JWT_SECRET        | JWT signing secret |

---

# Build Process

## Backend

```bash
npm run build
```

Produces the production build.

---

## Frontend

```bash
npm run build
```

Builds the optimized Next.js application.

---

# Database

Before starting the backend:

- Create the PostgreSQL database
- Configure environment variables
- Run migrations

Example:

```bash
npm run migration:run
```

---

# Running the Application

## Backend

```bash
npm run start:prod
```

---

## Frontend

```bash
npm run start
```

---

# Reverse Proxy

In production, a reverse proxy such as **Nginx** is recommended.

Responsibilities include:

- HTTPS termination
- Request forwarding
- Compression
- Security headers
- Static asset delivery

---

# Monitoring Scheduler

The backend includes a background scheduler responsible for:

- Loading active websites
- Sending HTTP requests
- Measuring response time
- Updating SSL expiration dates
- Saving monitoring results

The scheduler runs automatically and requires no additional configuration.

---

# Security Considerations

Production deployments should:

- Store secrets in environment variables
- Use HTTPS
- Keep dependencies updated
- Enable authentication on all protected routes
- Validate all incoming requests

---

# Logging

Application logs should include:

- Startup information
- Monitoring execution
- Errors
- Authentication events
- Unexpected exceptions

Future versions may integrate centralized logging solutions.

---

# Scaling

The current architecture is intended for a single backend instance.

Future improvements may include:

- Redis
- Queue Workers
- Horizontal scaling
- Load balancing

---

# Deployment Checklist

Before deploying:

- [ ] Environment variables configured
- [ ] PostgreSQL running
- [ ] Database migrations executed
- [ ] Production build completed
- [ ] HTTPS configured
- [ ] Backend started
- [ ] Frontend started
- [ ] Scheduler verified
- [ ] Website monitoring tested

---

# Related Documentation

- [01-project-overview.md](./01-project-overview.md)
- [02-requirements.md](./02-requirements.md)
- [03-system-design.md](./03-system-design.md)
- [04-database-design.md](./04-database-design.md)
- [05-api.md](./05-api.md)
- [06-roadmap.md](./06-roadmap.md)
