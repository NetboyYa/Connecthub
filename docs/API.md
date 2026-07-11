# ConnectHub API Documentation

## Base URL

```
https://api.connecthub.app/v1
```

## Authentication

All authenticated endpoints require an Authorization header:

```
Authorization: Bearer <JWT_TOKEN>
```

## Authentication Endpoints

### Sign Up

```http
POST /auth/signup
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "securePassword123",
  "username": "username",
  "displayName": "Display Name"
}

Response: 201 Created
{
  "id": "uuid",
  "email": "user@example.com",
  "username": "username",
  "token": "jwt_token",
  "refreshToken": "refresh_token"
}
```

### Login

```http
POST /auth/login
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "securePassword123"
}

Response: 200 OK
{
  "id": "uuid",
  "token": "jwt_token",
  "refreshToken": "refresh_token"
}
```

### OAuth Login (Google/Apple)

```http
POST /auth/oauth
Content-Type: application/json

{
  "provider": "google",
  "idToken": "provider_id_token"
}

Response: 200 OK
{
  "id": "uuid",
  "token": "jwt_token",
  "refreshToken": "refresh_token"
}
```

## User Endpoints

### Get User Profile

```http
GET /users/:userId

Response: 200 OK
{
  "id": "uuid",
  "username": "username",
  "displayName": "Display Name",
  "email": "user@example.com",
  "avatar": "avatar_url",
  "banner": "banner_url",
  "bio": "User bio",
  "pronouns": "they/them",
  "status": "online",
  "createdAt": "2024-01-01T00:00:00Z"
}
```

### Update User Profile

```http
PUT /users/:userId
Content-Type: application/json

{
  "displayName": "New Name",
  "bio": "New bio",
  "pronouns": "he/him",
  "avatar": "avatar_url",
  "banner": "banner_url"
}

Response: 200 OK
```

## Server Endpoints

### Create Server

```http
POST /servers
Content-Type: application/json

{
  "name": "Server Name",
  "icon": "icon_url",
  "banner": "banner_url",
  "description": "Server description",
  "isPublic": true
}

Response: 201 Created
{
  "id": "server_uuid",
  "name": "Server Name",
  "ownerId": "user_uuid",
  "icon": "icon_url",
  "isPublic": true,
  "createdAt": "2024-01-01T00:00:00Z"
}
```

### Get Server

```http
GET /servers/:serverId

Response: 200 OK
{
  "id": "server_uuid",
  "name": "Server Name",
  "ownerId": "user_uuid",
  "icon": "icon_url",
  "banner": "banner_url",
  "description": "Server description",
  "isPublic": true,
  "memberCount": 42,
  "channels": [...],
  "roles": [...],
  "members": [...]
}
```

### List User's Servers

```http
GET /users/:userId/servers

Response: 200 OK
[
  { id, name, icon, ... },
  ...
]
```

## Channel Endpoints

### Create Channel

```http
POST /servers/:serverId/channels
Content-Type: application/json

{
  "name": "channel-name",
  "type": "text",
  "categoryId": "category_uuid",
  "isPrivate": false,
  "topic": "Channel topic"
}

Response: 201 Created
{
  "id": "channel_uuid",
  "serverId": "server_uuid",
  "name": "channel-name",
  "type": "text",
  "createdAt": "2024-01-01T00:00:00Z"
}
```

### Get Channel Messages

```http
GET /channels/:channelId/messages?limit=50&before=message_uuid

Response: 200 OK
[
  {
    "id": "message_uuid",
    "authorId": "user_uuid",
    "content": "Message content",
    "timestamp": "2024-01-01T00:00:00Z",
    "edited": false,
    "reactions": [...],
    "attachments": [...]
  },
  ...
]
```

### Send Message

```http
POST /channels/:channelId/messages
Content-Type: application/json

{
  "content": "Message content",
  "mentions": ["user_uuid"],
  "attachments": [...]
}

Response: 201 Created
{
  "id": "message_uuid",
  "authorId": "user_uuid",
  "content": "Message content",
  "timestamp": "2024-01-01T00:00:00Z"
}
```

## Error Responses

```json
{
  "error": "error_code",
  "message": "Human readable error message",
  "statusCode": 400
}
```

Common error codes:
- `UNAUTHORIZED`: Missing or invalid token
- `FORBIDDEN`: Insufficient permissions
- `NOT_FOUND`: Resource not found
- `VALIDATION_ERROR`: Invalid input data
- `RATE_LIMITED`: Too many requests
- `INTERNAL_ERROR`: Server error
