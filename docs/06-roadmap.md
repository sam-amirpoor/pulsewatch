# Development Roadmap

## Introduction

This roadmap outlines the planned development stages of PulseWatch.

The project is developed incrementally, with each milestone introducing a new set of features while maintaining clean architecture, documentation, and production-ready code quality.

---

# Version 0.1.0

## Project Foundation

- [x] Initialize NestJS project
- [x] Configure TypeScript
- [ ] Configure ESLint & Prettier
- [ ] Configure environment variables
- [ ] Configure PostgreSQL
- [ ] Configure TypeORM
- [ ] Create project structure
- [ ] Initial GitHub repository setup

---

# Version 0.2.0

## Authentication

- [ ] User registration
- [ ] User login
- [ ] Password hashing
- [ ] JWT authentication
- [ ] Authentication Guard
- [ ] Protected routes
- [ ] Current user endpoint

---

# Version 0.3.0

## Website Management

- [ ] Create website
- [ ] Get website
- [ ] List user websites
- [ ] Update website
- [ ] Delete website
- [ ] Enable / Disable monitoring

---

# Version 0.4.0

## Monitoring Engine

- [ ] HTTP request service
- [ ] Response time measurement
- [ ] HTTP status collection
- [ ] Error handling
- [ ] Save monitoring results
- [ ] Manual monitoring endpoint

---

# Version 0.5.0

## Scheduler

- [ ] Scheduled monitoring
- [ ] Monitor all active websites
- [ ] Automatic monitoring every minute
- [ ] Background monitoring service

---

# Version 0.6.0

## SSL Monitoring

- [ ] Read SSL certificate
- [ ] Store expiration date
- [ ] Calculate remaining days
- [ ] Update website SSL information

---

# Version 0.7.0

## Statistics

- [ ] Uptime calculation
- [ ] Average response time
- [ ] Success rate
- [ ] Failed requests
- [ ] Website statistics endpoint

---

# Version 0.8.0

## Dashboard

- [ ] Dashboard summary
- [ ] Latest checks
- [ ] Website overview
- [ ] Response time visualization
- [ ] Uptime overview

---

# Version 0.9.0

## Production Improvements

- [ ] Logging
- [ ] Global exception handling
- [ ] Validation
- [ ] Configuration improvements
- [ ] API documentation
- [ ] Performance optimization

---

# Version 1.0.0

## First Stable Release

- [ ] Stable REST API
- [ ] Complete documentation
- [ ] Docker support
- [ ] Docker Compose
- [ ] Production deployment guide
- [ ] First public release

---

# Future Versions

The following features are planned for future releases.

## Monitoring

- [ ] API monitoring
- [ ] TCP monitoring
- [ ] Ping monitoring
- [ ] Multi-region monitoring

---

## Notifications

- [ ] Email notifications
- [ ] Telegram notifications
- [ ] Discord notifications
- [ ] Webhook support

---

## Dashboard

- [ ] Historical charts
- [ ] Response time graphs
- [ ] Advanced analytics

---

## Infrastructure

- [ ] Redis
- [ ] Queue Workers
- [ ] Horizontal scaling
- [ ] Caching
- [ ] Health checks

---

# Development Principles

Every feature follows the same development workflow:

1. Requirements Analysis
2. System Design
3. Database Design
4. API Design
5. Implementation
6. Testing
7. Documentation

---

# Project Status

Current Version:

```
v0.1.0
```

Current Focus:

- Project setup
- Authentication
- Website management

---

# Related Documentation

- [01-project-overview.md](01-project-overview.md)
- [02-requirements.md](02-requirements.md)
- [03-system-design.md](03-system-design.md)
- [04-database-design.md](04-database-design.md)
- [05-api.md](05-api.md)
- [07-deployment.md](07-deployment.md)
