# Project Overview

## Introduction

PulseWatch is an open-source website monitoring platform designed to monitor website availability, performance, and SSL certificate status.

The project continuously checks registered websites, collects monitoring data, and provides useful insights such as uptime percentage, response time, HTTP status codes, and SSL certificate expiration.

PulseWatch is being developed as a real-world software engineering project with a strong focus on clean architecture, scalability, maintainability, and production-ready design.

---

# Problem Statement

Website owners need to know when their services become unavailable or start responding slowly.

Manually checking websites is inefficient and unreliable.

PulseWatch automates this process by periodically monitoring websites and storing historical monitoring data for analysis.

---

# Project Goals

The primary goals of PulseWatch are:

- Monitor website availability
- Measure response times
- Track SSL certificate expiration
- Store monitoring history
- Calculate uptime statistics
- Provide a modern dashboard
- Demonstrate software engineering best practices

---

# Target Users

PulseWatch is intended for:

- Developers
- Freelancers
- Small businesses
- SaaS owners
- Anyone managing websites or APIs

---

# Core Features

## Website Management

- Add websites
- Edit websites
- Delete websites
- Enable or disable monitoring
- Configure monitoring intervals

---

## Website Monitoring

- Manual website checks
- Automatic scheduled monitoring
- HTTP status monitoring
- Response time measurement
- Downtime tracking

---

## SSL Monitoring

- SSL certificate inspection
- Expiration date monitoring
- Remaining days calculation

---

## Analytics

- Uptime percentage
- Average response time
- Monitoring history
- Website statistics

---

## Authentication

- User registration
- Login
- JWT authentication
- Protected APIs

---

# High-Level Architecture

PulseWatch consists of three main repositories.

## Frontend

Responsible for:

- User interface
- Dashboard
- Authentication pages
- Data visualization

Repository:

https://github.com/sam-amirpoor/pulsewatch-frontend

---

## Backend

Responsible for:

- Business logic
- REST API
- Monitoring engine
- Authentication
- SSL inspection
- Background jobs
- Database operations

Repository:

https://github.com/sam-amirpoor/pulsewatch-backend

---

## Documentation

Responsible for:

- Project documentation
- System design
- API documentation
- Database design
- Diagrams
- Roadmap

Repository:

https://github.com/sam-amirpoor/pulsewatch

---

# Technology Stack

## Frontend

- Next.js
- React
- TypeScript
- Tailwind CSS

## Backend

- NestJS
- TypeScript
- PostgreSQL
- TypeORM

## Infrastructure

- Docker (planned)
- Docker Compose (planned)

---

# Development Philosophy

PulseWatch is being developed using an engineering-first approach.

Before implementing any feature, the following steps are completed:

1. Requirements analysis
2. System design
3. Database design
4. API design
5. Sequence diagrams
6. Implementation

This workflow ensures that every feature is well-designed before development begins.

---

# Current Project Status

The project is currently under active development.

Development follows an incremental roadmap, where features are implemented gradually while maintaining clean architecture and comprehensive documentation.

---

# Future Plans

The following features are planned for future releases:

- Background workers
- Queue system
- Notifications
- Public status pages
- Team management
- Role-based permissions
- API monitoring
- Docker deployment
- Horizontal scalability

---

# Related Documentation

- [02-requirements.md](./02-requirements.md)
- [03-system-design.md](./03-system-design.md)
- [04-database-design.md](./04-database-design.md)
- [05-api.md](./05-api.md)
- [06-roadmap.md](./06-roadmap.md)
- [07-deployment.md](./07-deployment.md)
