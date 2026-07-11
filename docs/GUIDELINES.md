# Project Guidelines

## Development Standards

### Code Quality
- Use TypeScript for type safety across the project
- Follow ESLint configuration for consistent code style
- Run Prettier before committing
- Maintain >80% test coverage

### Commit Messages
Format: `[scope] message`

Examples:
- `[auth] Add JWT token refresh logic`
- `[messages] Fix message edit timestamp`
- `[mobile] Improve list rendering performance`

### Branch Naming
- Feature: `feature/description`
- Bug fix: `fix/description`
- Chore: `chore/description`
- Hotfix: `hotfix/description`

## Database Conventions

### Naming
- Tables: lowercase_with_underscores (plural)
- Columns: lowercase_with_underscores
- Primary keys: id (UUID)
- Foreign keys: table_name_id
- Timestamps: created_at, updated_at

### Migrations
- Create one migration per logical change
- Always provide rollback logic
- Test both up and down migrations
- Name clearly: `20240711_create_users_table.js`

## API Design

### Response Format
```json
{
  "success": true,
  "data": {},
  "message": "Success message",
  "timestamp": "2024-07-11T00:00:00Z"
}
```

### Error Format
```json
{
  "success": false,
  "error": "ERROR_CODE",
  "message": "Human readable message",
  "statusCode": 400,
  "timestamp": "2024-07-11T00:00:00Z"
}
```

### HTTP Status Codes
- 200: Success
- 201: Created
- 400: Bad Request
- 401: Unauthorized
- 403: Forbidden
- 404: Not Found
- 409: Conflict
- 422: Unprocessable Entity
- 429: Too Many Requests
- 500: Internal Server Error

## Mobile App Guidelines

### Component Structure
```
ComponentName/
├── ComponentName.tsx
├── ComponentName.styles.ts (if needed)
├── ComponentName.test.tsx
└── index.ts
```

### Props Pattern
Use TypeScript interfaces:
```typescript
interface ComponentNameProps {
  required: string;
  optional?: boolean;
  onAction?: () => void;
}
```

### State Management
- Use Zustand for global state
- Keep component state for UI-only data
- Avoid prop drilling with context

## Testing Requirements

### Unit Tests
- Test business logic and utilities
- Aim for 80%+ coverage
- Mock external dependencies

### Integration Tests
- Test API endpoints
- Test component interactions
- Use test databases

### E2E Tests
- Test critical user flows
- Use realistic test data
- Run before release

## Performance Goals

### Mobile App
- First paint: <2s
- Time to interactive: <4s
- Message load time: <100ms
- 60fps animations

### API Server
- Response time: <200ms (p95)
- Database query: <50ms (p95)
- Throughput: 1000+ req/s

## Security Checklist

- [ ] All passwords hashed (bcrypt)
- [ ] JWT tokens with expiration
- [ ] CORS properly configured
- [ ] Input validation on all endpoints
- [ ] SQL injection prevention (ORM)
- [ ] XSS protection
- [ ] Rate limiting enabled
- [ ] Secure headers (Helmet)
- [ ] HTTPS only in production
- [ ] Environment variables for secrets
- [ ] No sensitive data in logs
- [ ] Regular security audits

## Deployment Checklist

- [ ] All tests passing
- [ ] Code review approved
- [ ] Security scan passed
- [ ] Database migrations tested
- [ ] Environment variables configured
- [ ] Monitoring alerts set up
- [ ] Backup strategy in place
- [ ] Rollback plan documented
- [ ] Performance baseline set
- [ ] Documentation updated

## Documentation Standards

- Update README when adding features
- Document breaking changes
- Include code examples
- Keep API docs in sync
- Add architecture diagrams
- Document complex logic with comments

## Tools & Services

- **Version Control**: GitHub
- **CI/CD**: GitHub Actions
- **Monitoring**: DataDog / New Relic
- **Error Tracking**: Sentry
- **Analytics**: Mixpanel
- **Logging**: CloudWatch / ELK Stack
- **Database**: PostgreSQL 13+
- **Cache**: Redis 6+
- **Storage**: AWS S3
- **CDN**: CloudFront
- **Email**: SendGrid
- **SMS**: Twilio (optional)
- **Push Notifications**: Firebase Cloud Messaging

## Release Process

1. Create release branch: `release/v1.0.0`
2. Update version numbers
3. Update CHANGELOG
4. Create GitHub release tag
5. Deploy to staging
6. Run full test suite
7. Deploy to production
8. Monitor metrics closely
9. Document any issues

## Support & Resources

- Documentation: `/docs`
- Design System: `/design/DESIGN_SYSTEM.md`
- API Reference: `/docs/API.md`
- Architecture: `/docs/ARCHITECTURE.md`
- Contributing: `/CONTRIBUTING.md`

## Questions?

- Check existing documentation first
- Review similar code in the repo
- Ask in team discussions
- Create an issue for guidance
