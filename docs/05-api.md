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

Authentication endpoints are responsible for user registration, authentication, token management, and session management.

All requests and responses use **JSON**.

---

## Register

```http
POST /api/auth/register
```

Creates a new user account.

### Authentication

Not required.

### Headers

```http
Content-Type: application/json
```

### Request Body

```json
{
  "email": "john@example.com",
  "password": "StrongPassword123"
}
```

| Field | Type | Required | Description |
| ------- | ------ | :------: | ------------------------- |
| email | string | ✅ | User email address |
| password | string | ✅ | User password (minimum 8 characters) |

### Success Response

**201 Created**

```json
{
  "data": {
    "id": "3b75b5d0-5a0f-4e4d-8fd0-f2efad95c2f2",
    "email": "john@example.com",
    "createdAt": "2026-08-01T12:00:00Z"
  }
}
```

### Error Responses

#### 400 Bad Request

Validation failed.

#### 409 Conflict

Email already exists.

---

## Login

```http
POST /api/auth/login
```

Authenticates a user and returns authentication tokens.

### Authentication

Not required.

### Headers

```http
Content-Type: application/json
```

### Request Body

```json
{
  "email": "john@example.com",
  "password": "StrongPassword123"
}
```

| Field | Type | Required |
| ------- | ------ | :------: |
| email | string | ✅ |
| password | string | ✅ |

### Success Response

**200 OK**

```json
{
  "data": {
    "user": {
      "id": "3b75b5d0-5a0f-4e4d-8fd0-f2efad95c2f2",
      "email": "john@example.com"
    },
    "accessToken": "jwt_access_token",
    "refreshToken": "jwt_refresh_token",
    "expiresIn": 604800
  }
}
```

### Error Responses

#### 400 Bad Request

Validation failed.

#### 401 Unauthorized

Invalid email or password.

---

## Refresh Access Token

```http
POST /api/auth/refresh
```

Generates a new access token using a valid refresh token.

### Authentication

Refresh Token required.

### Headers

```http
Content-Type: application/json
```

### Request Body

```json
{
  "refreshToken": "jwt_refresh_token"
}
```

| Field | Type | Required | Description |
| ------- | ------ | :------: | ---------------- |
| refreshToken | string | ✅ | Valid refresh token |

### Success Response

**200 OK**

```json
{
  "data": {
    "accessToken": "new_access_token",
    "refreshToken": "new_refresh_token",
    "expiresIn": 604800
  }
}
```

### Error Responses

#### 401 Unauthorized

Invalid or expired refresh token.

---

## Logout

```http
POST /api/auth/logout
```

Terminates the current authenticated session.

### Authentication

Bearer Token required.

### Headers

```http
Authorization: Bearer <access_token>
```

### Request Body

None.

### Success Response

**204 No Content**

### Error Responses

#### 401 Unauthorized

Unauthorized.

---

# Users

User endpoints allow authenticated users to manage their own account.

---

## Get Current User

```http
GET /api/users/me
```

Returns the authenticated user's profile.

### Authentication

Bearer Token required.

### Headers

```http
Authorization: Bearer <access_token>
```

### Request Body

None.

### Success Response

**200 OK**

```json
{
  "data": {
    "id": "3b75b5d0-5a0f-4e4d-8fd0-f2efad95c2f2",
    "email": "john@example.com",
    "createdAt": "2026-08-01T12:00:00Z",
    "updatedAt": "2026-08-01T12:30:00Z"
  }
}
```

### Error Responses

#### 401 Unauthorized

Unauthorized.

---

## Update Current User

```http
PATCH /api/users/me
```

Updates the authenticated user's profile.

### Authentication

Bearer Token required.

### Headers

```http
Authorization: Bearer <access_token>
Content-Type: application/json
```

### Request Body

```json
{
  "email": "new@example.com"
}
```

| Field | Type | Required | Description |
| ------- | ------ | :------: | ---------------- |
| email | string | ❌ | New email address |

### Success Response

**200 OK**

```json
{
  "data": {
    "id": "3b75b5d0-5a0f-4e4d-8fd0-f2efad95c2f2",
    "email": "new@example.com",
    "updatedAt": "2026-08-01T13:00:00Z"
  }
}
```

### Error Responses

#### 400 Bad Request

Validation failed.

#### 401 Unauthorized

Unauthorized.

#### 409 Conflict

Email already exists.

---

## Change Password

```http
PATCH /api/users/me/password
```

Changes the authenticated user's password.

### Authentication

Bearer Token required.

### Headers

```http
Authorization: Bearer <access_token>
Content-Type: application/json
```

### Request Body

```json
{
  "currentPassword": "OldPassword123",
  "newPassword": "NewPassword123"
}
```

| Field | Type | Required | Description |
| ---------------- | ------ | :------: | ---------------- |
| currentPassword | string | ✅ | Current password |
| newPassword | string | ✅ | New password |

### Success Response

**200 OK**

```json
{
  "message": "Password changed successfully"
}
```

### Error Responses

#### 400 Bad Request

Validation failed.

#### 401 Unauthorized

Current password is incorrect.

---

## Delete Current User

```http
DELETE /api/users/me
```

Permanently deletes the authenticated user's account and all associated resources.

### Authentication

Bearer Token required.

### Headers

```http
Authorization: Bearer <access_token>
```

### Request Body

None.

### Success Response

**204 No Content**

### Error Responses

#### 401 Unauthorized

Unauthorized.

---

# Websites

Website endpoints are responsible for managing monitored websites.

All endpoints require authentication.

---

## Create Website

```http
POST /api/websites
```

Creates a new website for monitoring.

### Authentication

Bearer Token required.

### Headers

```http
Authorization: Bearer <access_token>
Content-Type: application/json
```

### Request Body

```json
{
  "name": "Production API",
  "url": "https://api.example.com"
}
```

| Field | Type | Required | Description |
| ------- | ------ | :------: | ---------------------------- |
| name | string | ✅ | Website display name |
| url | string | ✅ | Website URL |

### Success Response

**201 Created**

```json
{
  "data": {
    "id": "uuid",
    "name": "Production API",
    "url": "https://api.example.com",
    "isActive": true,
    "sslExpirationDate": null,
    "lastSslCheckAt": null,
    "createdAt": "2026-08-01T12:00:00Z",
    "updatedAt": "2026-08-01T12:00:00Z"
  }
}
```

### Error Responses

#### 400 Bad Request

Validation failed.

#### 401 Unauthorized

Unauthorized.

---

## Get All Websites

```http
GET /api/websites
```

Returns all websites owned by the authenticated user.

### Authentication

Bearer Token required.

### Headers

```http
Authorization: Bearer <access_token>
```

### Success Response

**200 OK**

```json
{
  "data": [
    {
      "id": "uuid",
      "name": "Production API",
      "url": "https://api.example.com",
      "isActive": true,
      "sslExpirationDate": "2027-01-05T00:00:00Z",
      "lastSslCheckAt": "2026-08-01T12:00:00Z",
      "createdAt": "2026-08-01T12:00:00Z",
      "updatedAt": "2026-08-01T12:00:00Z"
    }
  ]
}
```

---

## Get Website

```http
GET /api/websites/:id
```

Returns detailed information about a specific website.

### Authentication

Bearer Token required.

### Headers

```http
Authorization: Bearer <access_token>
```

### Success Response

**200 OK**

```json
{
  "data": {
    "id": "uuid",
    "name": "Production API",
    "url": "https://api.example.com",
    "isActive": true,
    "sslExpirationDate": "2027-01-05T00:00:00Z",
    "lastSslCheckAt": "2026-08-01T12:00:00Z",
    "createdAt": "2026-08-01T12:00:00Z",
    "updatedAt": "2026-08-01T12:00:00Z"
  }
}
```

### Error Responses

#### 404 Not Found

Website not found.

---

## Update Website

```http
PATCH /api/websites/:id
```

Updates website information.

### Authentication

Bearer Token required.

### Headers

```http
Authorization: Bearer <access_token>
Content-Type: application/json
```

### Request Body

```json
{
  "name": "Production API",
  "url": "https://new-api.example.com"
}
```

Both fields are optional.

| Field | Type | Required |
| ------- | ------ | :------: |
| name | string | ❌ |
| url | string | ❌ |

### Success Response

**200 OK**

```json
{
  "data": {
    "id": "uuid",
    "name": "Production API",
    "url": "https://new-api.example.com",
    "updatedAt": "2026-08-01T13:00:00Z"
  }
}
```

---

## Update Monitoring Settings

```http
PATCH /api/websites/:id/monitoring
```

Updates website monitoring settings.

### Authentication

Bearer Token required.

### Headers

```http
Authorization: Bearer <access_token>
Content-Type: application/json
```

### Request Body

```json
{
  "isActive": false,
}
```

Both fields are optional.

| Field | Type | Required | Description |
| ---------------- | ------- | :------: | ---------------- |
| isActive | boolean | ❌ | Enable or disable monitoring |

### Success Response

**200 OK**

```json
{
  "message": "Monitoring settings updated successfully"
}
```

---

## Delete Website

```http
DELETE /api/websites/:id
```

Deletes a monitored website.

### Authentication

Bearer Token required.

### Headers

```http
Authorization: Bearer <access_token>
```

### Success Response

**204 No Content**

### Error Responses

#### 404 Not Found

Website not found.

---

# Monitoring

Monitoring endpoints provide website health checks, monitoring history, and performance statistics.

All endpoints require authentication.

---

## Run Manual Check

```http
POST /api/websites/:id/check
```

Immediately performs a monitoring check for the specified website.

### Authentication

Bearer Token required.

### Headers

```http
Authorization: Bearer <access_token>
```

### Success Response

**200 OK**

```json
{
  "data": {
    "statusCode": 200,
    "responseTime": 187,
    "isSuccess": true,
    "checkedAt": "2026-08-01T12:30:00Z",
    "sslExpirationDate": "2027-01-05T00:00:00Z"
  }
}
```

---

## Get Latest Check

```http
GET /api/websites/:id/latest
```

Returns the latest monitoring result.

### Authentication

Bearer Token required.

### Headers

```http
Authorization: Bearer <access_token>
```

### Success Response

**200 OK**

```json
{
  "data": {
    "statusCode": 200,
    "responseTime": 183,
    "isSuccess": true,
    "errorMessage": null,
    "checkedAt": "2026-08-01T12:30:00Z"
  }
}
```

---

## Get Monitoring History

```http
GET /api/websites/:id/history?page=1&limit=20
```

Returns monitoring history with pagination.

### Authentication

Bearer Token required.

### Headers

```http
Authorization: Bearer <access_token>
```

### Query Parameters

| Parameter | Type | Default |
| ---------- | ------ | ------- |
| page | number | 1 |
| limit | number | 20 |

### Success Response

**200 OK**

```json
{
  "data": [
    {
      "statusCode": 200,
      "responseTime": 180,
      "isSuccess": true,
      "errorMessage": null,
      "checkedAt": "2026-08-01T12:00:00Z"
    },
    {
      "statusCode": 503,
      "responseTime": 0,
      "isSuccess": false,
      "errorMessage": "Service Unavailable",
      "checkedAt": "2026-08-01T11:59:00Z"
    }
  ],
  "meta": {
    "page": 1,
    "limit": 20,
    "total": 152
  }
}
```

---

## Get Website Statistics

```http
GET /api/websites/:id/statistics
```

Returns calculated monitoring statistics.

### Authentication

Bearer Token required.

### Headers

```http
Authorization: Bearer <access_token>
```

### Success Response

**200 OK**

```json
{
  "data": {
    "uptime": 99.92,
    "averageResponseTime": 183,
    "successfulChecks": 1248,
    "failedChecks": 6,
    "lastCheck": "2026-08-01T12:30:00Z",
    "currentStatus": "UP"
  }
}
```

---

## Get Website Uptime

```http
GET /api/websites/:id/uptime
```

Returns uptime statistics for the specified website.

### Authentication

Bearer Token required.

### Headers

```http
Authorization: Bearer <access_token>
```

### Success Response

**200 OK**

```json
{
  "data": {
    "uptime": 99.92,
    "downtime": 0.08,
    "totalChecks": 1254,
    "successfulChecks": 1248,
    "failedChecks": 6
  }
}
```

---

## Monitoring Process

A manual or scheduled monitoring check performs the following steps:

1. Load website information.
2. Send an HTTP request.
3. Measure response time.
4. Record HTTP status code.
5. Determine whether the request succeeded.
6. Retrieve SSL certificate information (HTTPS only).
7. Update the website's latest SSL status.
8. Save a Monitoring Result record.

---

# Dashboard

Dashboard endpoints provide an overview of the user's monitored websites and overall monitoring statistics.

All dashboard endpoints require authentication.

---

## Dashboard Summary

```http
GET /api/dashboard
```

Returns a summary of the authenticated user's monitoring system.

### Authentication

Bearer Token required.

### Headers

```http
Authorization: Bearer <access_token>
```

### Success Response

**200 OK**

```json
{
  "data": {
    "totalWebsites": 8,
    "online": 7,
    "offline": 1,
    "averageResponseTime": 176,
    "overallUptime": 99.94
  }
}
```

### Error Responses

#### 401 Unauthorized

Unauthorized.

---

# Response Format

All successful responses follow a consistent format.

## Success Response

```json
{
  "data": {}
}
```

For operations that do not return any resource, the API responds with:

```http
204 No Content
```

---

## Error Response

```json
{
  "statusCode": 404,
  "message": "Website not found",
  "error": "Not Found"
}
```

Validation errors may contain additional details.

Example:

```json
{
  "statusCode": 400,
  "message": [
    "email must be an email",
    "password must be at least 8 characters"
  ],
  "error": "Bad Request"
}
```

---

# HTTP Status Codes

| Status Code | Description |
| ------------ | ---------------------- |
| 200 | OK |
| 201 | Created |
| 204 | No Content |
| 400 | Bad Request |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 409 | Conflict |
| 422 | Unprocessable Entity |
| 500 | Internal Server Error |

---

# Automatic Monitoring

PulseWatch continuously monitors all active websites in the background.

The monitoring scheduler runs automatically at the configured interval and performs the following steps:

1. Load all active websites.
2. Send an HTTP request to each website.
3. Measure response time.
4. Record the HTTP status code.
5. Determine whether the check was successful.
6. Retrieve SSL certificate information (HTTPS only).
7. Update the website's latest SSL status.
8. Store a Monitoring Result record.

This process requires no user interaction.

---

# API Version

Current API version:

```text
v1
```

All endpoints are currently available under:

```text
/api
```

Future versions may be exposed using versioned routes:

```text
/api/v2
/api/v3
```

---

# Future Endpoints

The following resources are planned for future releases.

## Notifications

```http
GET    /api/notifications
PATCH  /api/notifications/:id/read
PATCH  /api/notifications/read-all
DELETE /api/notifications/:id
```

Description:

- Retrieve notifications.
- Mark a notification as read.
- Mark all notifications as read.
- Delete a notification.

---

## Public Status Pages

```http
POST   /api/status-pages
GET    /api/status-pages
GET    /api/status-pages/:id
PATCH  /api/status-pages/:id
DELETE /api/status-pages/:id
```

Description:

Create and manage public status pages for monitored websites.

---

## API Keys

```http
POST   /api/api-keys
GET    /api/api-keys
DELETE /api/api-keys/:id
```

Description:

Manage personal API keys for programmatic access.

---

## Webhooks

```http
POST   /api/webhooks
GET    /api/webhooks
PATCH  /api/webhooks/:id
DELETE /api/webhooks/:id
```

Description:

Receive real-time events when monitoring results change.

---

# API Summary

| Resource | Endpoints |
| -------- | --------- |
| Authentication | Register, Login, Refresh Token, Logout |
| Users | Current User, Update Profile, Change Password, Delete Account |
| Websites | Create, List, Details, Update, Delete, Monitoring Settings |
| Monitoring | Manual Check, Latest Check, History, Statistics, Uptime |
| Dashboard | Dashboard Summary |

---

# Related Documentation

- [01-project-overview.md](01-project-overview.md)
- [02-requirements.md](02-requirements.md)
- [03-system-design.md](03-system-design.md)
- [04-database-design.md](04-database-design.md)
- [06-roadmap.md](06-roadmap.md)
- [07-deployment.md](07-deployment.md)
