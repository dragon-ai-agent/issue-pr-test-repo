# API Documentation

## Overview

This document describes the available API endpoints.

## Authentication

All API requests require a Bearer token in the Authorization header:

```
Authorization: Bearer <token>
```

### Rate Limiting

API requests are rate limited to **100 requests per minute** per API key. Rate limit headers are included in all responses:

- `X-RateLimit-Limit`: Maximum requests per minute
- `X-RateLimit-Remaining`: Requests remaining in current window
- `X-RateLimit-Reset`: Unix timestamp when the limit resets

## Endpoints

### GET /api/health

Check service health status.

**Response:**
```json
{
  "status": "healthy",
  "timestamp": "2024-01-15T10:30:00Z"
}
```

### GET /api/users

Retrieve list of users.

**Response:**
```json
{
  "users": [
    {"id": 1, "name": "Alice"},
    {"id": 2, "name": "Bob"}
  ]
}
```

### POST /api/users

Create a new user.

**Request:**
```json
{
  "name": "Charlie",
  "email": "charlie@example.com"
}
```

**Response:**
```json
{
  "id": 3,
  "name": "Charlie",
  "email": "charlie@example.com"
}
```

### DELETE /api/users/{id}

Delete a user by ID.

**Response:**
```json
{
  "message": "User deleted successfully"
}
```

## Error Responses

All errors follow this format:

```json
{
  "error": "Error message",
  "code": "ERROR_CODE"
}
```

### HTTP Status Codes

| Code | Description |
|------|-------------|
| 400 | Bad Request - Invalid input or malformed JSON |
| 401 | Unauthorized - Missing or invalid authentication token |
| 404 | Not Found - Resource does not exist |
| 429 | Too Many Requests - Rate limit exceeded |
| 500 | Internal Server Error - Unexpected server error |
