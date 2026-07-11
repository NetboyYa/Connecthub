# ConnectHub Architecture

## System Overview

ConnectHub is a distributed mobile-first application with the following components:

```
┌─────────────────────────────────┐         ┌──────────────────────────────┐
│  Mobile App                     │◄────────┤  API Server                  │
│ (React Native)                  │         │ (Node.js)                    │
└─────────────────────────────────┘         └──────────────────────────────┘
                                               ▲
                                               │
                    ┌──────────────────────────┼──────────────────────────┐
                    │                          │                          │
              ┌─────┴──────────┐   ┌──────────┴──────────┐   ┌──────────┴──────┐
              │PostgreSQL      │   │WebSocket           │   │S3/CDN           │
              │Database        │   │Server              │   │Storage          │
              └────────────────┘   └────────────────────┘   └─────────────────┘
```

## Components

### Mobile App
- **Framework**: React Native with Expo
- **State Management**: Redux or Zustand
- **Networking**: Axios + Socket.io client
- **Real-time Updates**: WebSocket connection
- **Local Storage**: AsyncStorage for caching

### Backend API
- **Framework**: Express.js with TypeScript
- **Database**: PostgreSQL with Sequelize ORM
- **Real-time**: Socket.io for WebSocket connections
- **Authentication**: JWT + OAuth2 (Google, Apple)
- **File Storage**: AWS S3
- **Caching**: Redis for session management

### Database Schema

Key entities:
- **Users**: accounts, profiles, settings
- **Servers**: community management
- **Channels**: text, voice, announcement
- **Messages**: chat history with threading
- **Roles & Permissions**: access control
- **Friends & Relationships**: social graph

## API Design

### RESTful Endpoints

```
Auth:
  POST /api/auth/signup
  POST /api/auth/login
  POST /api/auth/refresh
  POST /api/auth/logout

Users:
  GET /api/users/:id
  PUT /api/users/:id
  GET /api/users/:id/friends
  POST /api/users/:id/friends/:friendId

Servers:
  GET /api/servers
  POST /api/servers
  GET /api/servers/:id
  PUT /api/servers/:id
  DELETE /api/servers/:id

Channels:
  GET /api/servers/:serverId/channels
  POST /api/servers/:serverId/channels
  GET /api/channels/:id/messages
  POST /api/channels/:id/messages

Direct Messages:
  GET /api/dms
  POST /api/dms
  GET /api/dms/:conversationId/messages
  POST /api/dms/:conversationId/messages
```

### WebSocket Events

```
Connection:
  CONNECT
  DISCONNECT

Messaging:
  MESSAGE_SEND
  MESSAGE_EDIT
  MESSAGE_DELETE
  TYPING_START
  TYPING_STOP

Server Events:
  USER_JOINED
  USER_LEFT
  VOICE_STATE_UPDATE
  PRESENCE_UPDATE

Notifications:
  MENTION
  FRIEND_REQUEST
  FRIEND_ACCEPTED
```

## Data Flow

1. User performs action in mobile app
2. App sends request to backend API
3. API processes request (authentication, validation, business logic)
4. Database is updated
5. Real-time events broadcast via WebSocket to affected users
6. Mobile app receives updates and re-renders

## Security

- **Authentication**: JWT tokens with refresh rotation
- **Authorization**: Role-based access control (RBAC)
- **Encryption**: TLS for all communications, bcrypt for passwords
- **Validation**: Input validation on backend
- **Rate Limiting**: API rate limiting per user
- **CORS**: Configured for mobile app domains

## Scalability Considerations

- Horizontal scaling: Stateless API servers
- Database replication: Read replicas for scaling
- Caching: Redis for sessions and frequently accessed data
- CDN: CloudFront for media delivery
- Message Queue: Consider for async operations (email, notifications)
