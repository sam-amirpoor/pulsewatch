# Database Design

## Introduction

This document describes the database design of PulseWatch.

The database is designed to support website monitoring, uptime calculation, response time tracking, and SSL certificate expiration monitoring while keeping the schema simple and maintainable.

---

# Database Choice

PulseWatch uses **PostgreSQL** as its primary database.

Reasons:

- Relational data model
- Excellent indexing support
- Reliable performance
- Strong ecosystem
- Production-ready

---

# Core Entities

The initial version of PulseWatch consists of three primary entities:

- Users
- Websites
- Monitoring Results

---

# Entity: Users

Stores application users.

## Fields

- id (UUID)
- email
- password_hash
- created_at
- updated_at

## Relationships

- One User → Many Websites

---

# Entity: Websites

Stores websites monitored by the system.

## Fields

- id (UUID)
- user_id (FK → Users.id)
- name
- url
- is_active
- check_interval
- ssl_expiration_date
- last_ssl_check_at
- created_at
- updated_at

## Description

Each website belongs to one user.

SSL information is stored directly within the website record because only the latest SSL state is required.

Historical SSL records are intentionally excluded from the initial version.

---

# Entity: Monitoring Results

Stores every monitoring request performed by the monitoring engine.

## Fields

- id (UUID)
- website_id (FK → Websites.id)
- status_code
- response_time_ms
- is_success
- error_message
- checked_at

## Description

Each monitoring execution creates exactly one Monitoring Result.

This table serves as the historical monitoring log and is expected to grow continuously over time.

---

# Entity Relationships

```text
Users
   │
   ▼
Websites
   │
   ▼
MonitoringResults
```

---

# Relationship Details

## User → Website

Relationship:

```
One-to-Many
```

A user can register multiple websites.

Each website belongs to exactly one user.

---

## Website → Monitoring Result

Relationship:

```
One-to-Many
```

Each website generates many monitoring records throughout its lifetime.

---

# Monitoring Data Flow

```text
Scheduler
      │
      ▼
Monitoring Service
      │
      ▼
Load Website
      │
      ▼
HTTP Request
      │
      ▼
Measure Response
      │
      ▼
Save Monitoring Result
      │
      ▼
Update Website SSL Information
```

---

# Indexing Strategy

## Users

Indexes

- email (UNIQUE)

---

## Websites

Indexes

- user_id
- is_active

Reason:

- Fast retrieval of user websites
- Quickly identify websites requiring monitoring

---

## Monitoring Results

Indexes

- website_id
- checked_at
- (website_id, checked_at)

Reason:

- Monitoring history
- Dashboard statistics
- Time-based filtering
- Recent checks

---

# Data Growth

The largest table in the system will be **Monitoring Results**.

Since a new record is inserted after every monitoring cycle, this table is expected to grow significantly faster than the others.

Future versions may introduce:

- Data archiving
- Retention policies
- Aggregated statistics
- Partitioning

---

# Design Decisions

The initial database intentionally keeps SSL information inside the **Websites** table.

Reasons:

- Only the latest SSL state is required.
- Historical SSL data provides little value for the MVP.
- Simpler schema.
- Fewer joins.
- Easier maintenance.

If future requirements demand SSL history, a dedicated `ssl_checks` table can be introduced without major architectural changes.

---

# Future Improvements

Possible future entities include:

- Notifications
- Queue Jobs
- Team Members
- Roles & Permissions
- Public Status Pages
- API Monitoring
- SSL History

These features are intentionally excluded from the initial release.

---

# Summary

The initial database design prioritizes:

- Simplicity
- Readability
- Maintainability
- Fast monitoring writes
- Efficient dashboard queries
- Easy future extensibility

---

# Related Documentation

- [01-project-overview.md](01-project-overview.md)
- [02-requirements.md](02-requirements.md)
- [03-system-design.md](03-system-design.md)
- [05-api.md](05-api.md)
- [06-roadmap.md](06-roadmap.md)
- [07-deployment.md](07-deployment.md)
