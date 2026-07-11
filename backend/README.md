# ConnectHub Backend API

A robust Node.js/Express backend API providing real-time messaging, server management, and community features for the ConnectHub mobile app.

## Tech Stack

- **Runtime**: Node.js 18+
- **Framework**: Express.js with TypeScript
- **Database**: PostgreSQL with Sequelize ORM
- **Real-time**: Socket.io for WebSocket connections
- **Authentication**: JWT + OAuth2 (Google, Apple)
- **File Storage**: AWS S3
- **Caching**: Redis
- **Queue**: Bull for async jobs
- **Validation**: Joi
- **Logging**: Winston
- **Testing**: Jest + Supertest

## Quick Start

### Prerequisites
- Node.js 18+
- PostgreSQL 13+
- Redis (optional)

### Installation

```bash
cd backend
npm install
cp .env.example .env
npm run migrate
npm run dev
```

## Available Scripts

```bash
npm run dev              # Development server
npm run build            # Production build
npm start               # Start production server
npm test                # Run tests
npm run lint            # Run linter
npm run format          # Format code
npm run migrate         # Run migrations
npm run migrate:undo    # Rollback migrations
npm run seed            # Seed database
```

## Key Features

- ✅ Email/password and OAuth authentication
- ✅ Real-time messaging with Socket.io
- ✅ Server and channel management
- ✅ Friend system with activity tracking
- ✅ Message reactions and threading
- ✅ File attachments (AWS S3)
- ✅ Push notifications (Firebase)
- ✅ Role-based access control
- ✅ Message search and indexing
- ✅ User presence tracking

## Security

- Password hashing with bcrypt
- JWT token authentication
- CORS and security headers
- Rate limiting (1000 req/min)
- Input validation with Joi
- SQL injection prevention (ORM)
- HTTPS in production

## Contributing

See [CONTRIBUTING.md](../CONTRIBUTING.md) for guidelines.

## Support

For issues and questions, create a GitHub issue or check documentation.