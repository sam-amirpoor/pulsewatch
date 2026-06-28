# PulseWatch

> An open-source website monitoring platform for tracking website availability, response time, uptime, and SSL certificate health.

---

## Repositories

| Repository        | Description                                         |
| ----------------- | --------------------------------------------------- |
| **Documentation** | https://github.com/sam-amirpoor/pulsewatch          |
| **Backend**       | https://github.com/sam-amirpoor/pulsewatch-backend  |
| **Frontend**      | https://github.com/sam-amirpoor/pulsewatch-frontend |

---

## Overview

PulseWatch is a modern website monitoring platform built with software engineering best practices in mind.

It periodically monitors websites, collects performance metrics, inspects SSL certificates, and provides historical monitoring data through a modern dashboard.

This project is designed as a real-world engineering project rather than a simple CRUD application, with a strong emphasis on documentation, clean architecture, scalability, and maintainability.

---

## Features

### Monitoring

- Website availability monitoring
- Manual website checks
- Automatic scheduled monitoring
- HTTP status tracking
- Response time measurement
- Uptime calculation
- Downtime history

### SSL Monitoring

- SSL certificate inspection
- Expiration tracking
- Remaining days calculation

### Dashboard

- Overall monitoring overview
- Website statistics
- Historical monitoring data
- Performance analytics

### Authentication

- JWT Authentication
- Protected REST API
- User management

---

## Tech Stack

### Backend

- NestJS
- TypeScript
- PostgreSQL
- TypeORM

### Frontend

- Next.js
- React
- TypeScript
- Tailwind CSS

### Infrastructure

- Docker _(planned)_
- Docker Compose _(planned)_

---

## Project Goals

PulseWatch is primarily built to demonstrate practical software engineering concepts, including:

- Clean Architecture
- REST API Design
- Database Modeling
- Authentication & Authorization
- Background Jobs
- Monitoring Systems
- Logging
- Error Handling
- Scalability
- Production-ready Project Structure

---

## Documentation

Project documentation is available inside the **docs** directory.

| Document                                             | Description                                |
| ---------------------------------------------------- | ------------------------------------------ |
| [01 - Project Overview](docs/01-project-overview.md) | General introduction and project goals     |
| [02 - Requirements](docs/02-requirements.md)         | Functional and non-functional requirements |
| [03 - System Design](docs/03-system-design.md)       | High-level architecture and system design  |
| [04 - Database Design](docs/04-database-design.md)   | Database schema and relationships          |
| [05 - API Documentation](docs/05-api.md)             | REST API specification                     |
| [06 - Roadmap](docs/06-roadmap.md)                   | Development roadmap                        |
| [07 - Deployment](docs/07-deployment.md)             | Deployment strategy                        |

---

## Diagrams

System diagrams are available in the **diagrams** directory.

- Architecture Diagram
- Database ERD
- Sequence Diagrams

---

## Project Status

🚧 **Under Active Development**

PulseWatch is currently in active development.

Features are implemented incrementally following a documented roadmap while maintaining clean architecture and comprehensive documentation.

---

## Roadmap

- [x] Documentation structure
- [ ] Authentication
- [ ] Website management
- [ ] Monitoring engine
- [ ] SSL monitoring
- [ ] Statistics
- [ ] Dashboard
- [ ] Background jobs
- [ ] Notifications
- [ ] Docker deployment
- [ ] Public status pages

---

## Contributing

Contributions, ideas, discussions, and feedback are always welcome.

---

## License

This project is licensed under the MIT License.
