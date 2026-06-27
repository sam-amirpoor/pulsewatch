# Requirements

## Introduction

This document defines the functional and non-functional requirements for PulseWatch.

Its purpose is to describe **what the system should do**, without specifying **how it will be implemented**. Technical design decisions are documented separately in the System Design and Database Design documents.

---

# Functional Requirements

## 1. Authentication

The system shall allow users to securely access their personal dashboard.

### Requirements

- Users shall be able to register.
- Users shall be able to log in.
- Users shall receive an access token after successful authentication.
- Authenticated users shall access protected resources.
- Users shall be able to log out.
- Invalid credentials shall be rejected.

---

## 2. Website Management

The system shall allow authenticated users to manage monitored websites.

### Requirements

Users shall be able to:

- Add a new website
- View all registered websites
- View website details
- Update website information
- Delete a website
- Enable monitoring
- Disable monitoring

Each website shall include:

- Name
- URL
- Monitoring interval
- Monitoring status
- Creation date

---

## 3. Website Monitoring

The system shall periodically monitor every active website.

### Requirements

The monitoring service shall:

- Perform HTTP requests automatically
- Support manual health checks
- Record HTTP status codes
- Measure response time
- Detect unreachable websites
- Store every monitoring result
- Continue monitoring according to the configured interval

---

## 4. SSL Certificate Monitoring

The system shall inspect SSL certificates for HTTPS websites.

### Requirements

The system shall:

- Detect whether SSL is available
- Read certificate information
- Calculate certificate expiration date
- Calculate remaining days until expiration
- Store SSL information
- Report SSL validity status

---

## 5. Statistics

The system shall calculate useful monitoring statistics.

### Requirements

The system shall provide:

- Current website status
- Uptime percentage
- Average response time
- Total successful checks
- Total failed checks
- Total monitoring requests
- Last successful check
- Last failed check

---

## 6. Monitoring History

The system shall keep historical monitoring data.

### Requirements

Users shall be able to:

- View monitoring history
- View previous response times
- View previous status codes
- View historical uptime
- Review downtime events

---

## 7. Dashboard

The system shall provide a dashboard summarizing monitoring information.

### Requirements

The dashboard shall display:

- Total monitored websites
- Online websites
- Offline websites
- Average response time
- SSL warnings
- Recent monitoring activity

---

## 8. Background Monitoring

The monitoring process shall operate automatically.

### Requirements

The system shall:

- Execute monitoring jobs on schedule
- Continue monitoring without user interaction
- Process multiple websites
- Record monitoring results
- Continue operating after application restart

---

## 9. Notifications (Future)

The system may notify users when important events occur.

### Planned Requirements

- Website becomes unavailable
- Website recovers
- SSL certificate is close to expiration
- Monitoring failures occur repeatedly

---

# Non-Functional Requirements

## Performance

The system should:

- Respond to API requests with low latency
- Process monitoring jobs efficiently
- Support monitoring multiple websites simultaneously

---

## Scalability

The architecture should support future growth.

Future improvements may include:

- Queue-based processing
- Horizontal scaling
- Distributed monitoring workers

---

## Security

The system should:

- Protect authenticated endpoints
- Validate user input
- Prevent unauthorized access
- Store sensitive information securely

---

## Reliability

The monitoring service should:

- Continue operating despite temporary failures
- Handle network errors gracefully
- Recover automatically after restarts

---

## Maintainability

The project should follow software engineering best practices.

The codebase should emphasize:

- Clean Architecture
- Modular Design
- Separation of Concerns
- Reusable Components
- Readable Documentation

---

## Extensibility

The system should be designed to support future features without significant architectural changes.

Examples include:

- Public status pages
- Team management
- Role-based permissions
- API monitoring
- Multi-region monitoring
- Notification providers
- Monitoring integrations

---

# Assumptions

The initial version of PulseWatch assumes:

- Each website belongs to a single user.
- Monitoring is performed from a single server.
- HTTPS websites may expose SSL certificate information.
- Historical monitoring data is stored indefinitely unless removed by the user.

---

# Constraints

The initial release intentionally excludes:

- Microservices
- Distributed monitoring
- Kubernetes deployment
- Multi-region monitoring
- High availability architecture
- Real-time push notifications

These capabilities may be introduced in future versions.

---

# Related Documentation

- [01-project-overview.md](./01-project-overview.md)
- [03-system-design.md](./03-system-design.md)
- [04-database-design.md](./04-database-design.md)
- [05-api.md](./05-api.md)
- [06-roadmap.md](./06-roadmap.md)
- [07-deployment.md](./07-deployment.md)
