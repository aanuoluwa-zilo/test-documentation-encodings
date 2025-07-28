# User Management API Documentation

## Overview
The User Management API provides comprehensive functionality for managing user accounts, authentication, and authorization within the system.

## Authentication
All API endpoints require authentication using Bearer tokens. Include the token in the Authorization header:
```
Authorization: Bearer <your-token>
```

## Endpoints

### GET /api/users
Retrieves a list of all users in the system.

**Parameters:**
- `page` (optional): Page number for pagination
- `limit` (optional): Number of users per page
- `status` (optional): Filter by user status (active, inactive, suspended)

**Response:**
```json
{
  "users": [
    {
      "id": 1,
      "username": "john_doe",
      "email": "john@example.com",
      "status": "active",
      "created_at": "2024-01-15T10:30:00Z"
    }
  ],
  "pagination": {
    "page": 1,
    "limit": 20,
    "total": 150
  }
}
```

### POST /api/users
Creates a new user account.

**Request Body:**
```json
{
  "username": "new_user",
  "email": "user@example.com",
  "password": "secure_password",
  "role": "user"
}
```

**Response:**
```json
{
  "id": 123,
  "username": "new_user",
  "email": "user@example.com",
  "status": "active",
  "created_at": "2024-01-15T10:30:00Z"
}
```

### PUT /api/users/9
Updates an existing user account.

**Request Body:**
```json
{
  "email": "updated@example.com",
  "status": "active"
}
```

### DELETE /api/users/9
Deactivates a user account.

## Error Codes
- `400`: Bad Request - Invalid input data
- `401`: Unauthorized - Invalid or missing authentication
- `403`: Forbidden - Insufficient permissions
- `404`: Not Found - User not found
- `500`: Internal Server Error - Server error

## Rate Limiting
API calls are limited to 1000 requests per hour per API key.

## Examples

### Creating a User
```bash
curl -X POST https://api.example.com/users \
  -H "Authorization: Bearer <your-token>" \
  -H "Content-Type: application/json" \
  -d '{
    "username": "john_doe",
    "email": "john@example.com",
    "password": "secure123",
    "role": "user"
  }'
```

### Retrieving Users
```bash
curl -X GET "https://api.example.com/users?page=1&limit=20" \
  -H "Authorization: Bearer <your-token>"
```
