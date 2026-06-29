# API Design

## Introduction

This document defines the REST API for PulseWatch.

The API follows RESTful principles and communicates using JSON.

All endpoints are prefixed with:

```text
/api
```

---

# Authentication

Protected endpoints require a valid JWT access token.

Example:

```http
Authorization: Bearer <access_token>
```

---

# Authentication

## Register

```http
POST /api/auth/register
```

Creates a new user account.

---

## Login

```http
POST /api/auth/login
```

Authenticates a user and returns a JWT access token.

---

## Get Current User

```http
GET /api/auth/me
```

Returns the authenticated user's information.

---

# Websites

## Create Website

```http
POST /api/websites
```

Creates a new website for monitoring.

### Request Body

```json
{
  "name": "My Website",
  "url": "https://example.com"
}
```

---

## Get All Websites

```http
GET /api/websites
```

Returns all websites owned by the authenticated user.

---

## Get Website

```http
GET /api/websites/:id
```

Returns detailed information about a website.

---

## Update Website

```http
PATCH /api/websites/:id
```

Updates website information.

Example:

```json
{
  "name": "Production API",
  "url": "https://api.example.com"
}
```

---

## Enable / Disable Monitoring

```http
PATCH /api/websites/:id
```

Updates monitoring state.

Example:

```json
{
  "isActive": true
}
```

or

```json
{
  "isActive": false
}
```

---

## Delete Website

```http
DELETE /api/websites/:id
```

Deletes a monitored website.

---

# Monitoring

## Run Manual Check

```http
POST /api/websites/:id/check
```

Immediately performs a monitoring check for the selected website.

This endpoint:

- Sends an HTTP request
- Measures response time
- Reads SSL expiration date (if HTTPS)
- Stores a Monitoring Result
- Updates website SSL information

---

## Get Latest Check

```http
GET /api/websites/:id/latest
```

Returns the latest monitoring result.

---

## Get Monitoring History

```http
GET /api/websites/:id/history
```

Returns historical monitoring results.

Supports pagination.

Example:

```http
GET /api/websites/:id/history?page=1&limit=20
```

---

## Get Website Statistics

```http
GET /api/websites/:id/statistics
```

Returns calculated statistics.

Example response:

```json
{
  "uptime": 99.92,
  "averageResponseTime": 183,
  "successfulChecks": 1248,
  "failedChecks": 6,
  "lastCheck": "2026-06-29T12:00:00Z",
  "currentStatus": "UP"
}
```

---

# Dashboard

## Dashboard Summary

```http
GET /api/dashboard
```

Returns an overview of the monitoring system.

Example response:

```json
{
  "totalWebsites": 8,
  "online": 7,
  "offline": 1,
  "averageResponseTime": 176
}
```

---

# Response Format

Successful responses:

```json
{
  "data": {}
}
```

---

Error responses:

```json
{
  "statusCode": 404,
  "message": "Website not found",
  "error": "Not Found"
}
```

---

# HTTP Status Codes

| Code | Description           |
| ---- | --------------------- |
| 200  | OK                    |
| 201  | Created               |
| 204  | No Content            |
| 400  | Bad Request           |
| 401  | Unauthorized          |
| 403  | Forbidden             |
| 404  | Not Found             |
| 409  | Conflict              |
| 500  | Internal Server Error |

---

# Automatic Monitoring

PulseWatch periodically checks all active websites.

Monitoring is executed by a background scheduler every minute.

The scheduler:

- Loads all active websites
- Sends HTTP requests
- Measures response time
- Updates SSL expiration date
- Stores monitoring history

This process is fully automatic and requires no user interaction.

---

# API Version

Current version:

```text
v1
```

Future versions may be exposed as:

```text
/api/v2
```

---

# Future Endpoints

The following endpoints are planned for future releases.

## Notifications

```http
GET    /api/notifications
PATCH  /api/notifications/:id/read
```

---

## Public Status Pages

```http
GET /api/status/:slug
```

---

## Team Management

```http
POST   /api/teams
GET    /api/teams
PATCH  /api/teams/:id
DELETE /api/teams/:id
```

---

## API Monitoring

```http
POST /api/apis
GET  /api/apis
```

---

# API Summary

| Resource       | Endpoints                                       |
| -------------- | ----------------------------------------------- |
| Authentication | Register, Login, Current User                   |
| Websites       | CRUD                                            |
| Monitoring     | Manual Check, Latest Check, History, Statistics |
| Dashboard      | Summary                                         |

---

# Related Documentation

- [01-project-overview.md](01-project-overview.md)
- [02-requirements.md](02-requirements.md)
- [03-system-design.md](03-system-design.md)
- [04-database-design.md](04-database-design.md)
- [06-roadmap.md](06-roadmap.md)
- [07-deployment.md](07-deployment.md)
