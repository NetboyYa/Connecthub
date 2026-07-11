# Deployment Guide

## Overview

ConnectHub can be deployed to various cloud platforms. This guide covers common deployment scenarios.

## Prerequisites

- Docker installed (for containerized deployment)
- Cloud provider account (AWS, Heroku, DigitalOcean, etc.)
- Environment variables configured
- SSL certificates for HTTPS

## Environment Variables

### Backend (.env)
```env
NODE_ENV=production
PORT=3000
API_URL=https://api.connecthub.app

# Database
DB_HOST=your-db-host
DB_PORT=5432
DB_NAME=connecthub
DB_USER=postgres
DB_PASSWORD=secure_password

# Redis
REDIS_URL=redis://your-redis-host:6379

# JWT
JWT_SECRET=your_super_secret_key
JWT_REFRESH_SECRET=refresh_secret
JWT_EXPIRATION=24h

# OAuth
GOOGLE_CLIENT_ID=your_google_id
GOOGLE_CLIENT_SECRET=your_secret
APPLE_CLIENT_ID=your_apple_id
APPLE_CLIENT_SECRET=your_apple_secret

# AWS S3
AWS_ACCESS_KEY_ID=your_key_id
AWS_SECRET_ACCESS_KEY=your_secret_key
AWS_REGION=us-east-1
AWS_S3_BUCKET=connecthub-prod

# Firebase
FIREBASE_PROJECT_ID=your_project
FIREBASE_PRIVATE_KEY=your_key
FIREBASE_CLIENT_EMAIL=your_email
```

### Mobile (.env)
```env
REACT_APP_API_URL=https://api.connecthub.app/v1
REACT_APP_SOCKET_URL=https://socket.connecthub.app
REACT_APP_GOOGLE_CLIENT_ID=your_google_id
REACT_APP_APPLE_CLIENT_ID=your_apple_id
```

## Docker Deployment

### Build Backend Image
```bash
cd backend
docker build -t connecthub-api:1.0.0 .
```

### Run with Docker Compose
```bash
docker-compose up -d
```

### Docker Compose File
```yaml
version: '3.8'
services:
  api:
    image: connecthub-api:1.0.0
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=production
      - DB_HOST=db
      - REDIS_URL=redis://cache:6379
    depends_on:
      - db
      - cache
    
  db:
    image: postgres:15-alpine
    environment:
      - POSTGRES_DB=connecthub
      - POSTGRES_PASSWORD=secure_password
    volumes:
      - postgres_data:/var/lib/postgresql/data
  
  cache:
    image: redis:7-alpine
    volumes:
      - redis_data:/data

volumes:
  postgres_data:
  redis_data:
```

## AWS EC2 Deployment

### 1. Launch EC2 Instance
```bash
# t3.medium or larger recommended
# Ubuntu 22.04 LTS AMI
```

### 2. Install Dependencies
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y nodejs npm postgresql redis-server
```

### 3. Clone Repository
```bash
git clone https://github.com/NetboyYa/ConnectHub.git
cd ConnectHub/backend
```

### 4. Setup Application
```bash
npm install
npm run build
```

### 5. Configure PM2
```bash
npm install -g pm2
pm2 start dist/app.js --name connecthub-api
pm2 save
pm2 startup
```

### 6. Configure Nginx
```nginx
upstream connecthub_api {
  server localhost:3000;
}

server {
  listen 443 ssl http2;
  server_name api.connecthub.app;

  ssl_certificate /path/to/certificate.crt;
  ssl_certificate_key /path/to/private.key;

  location / {
    proxy_pass http://connecthub_api;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection "upgrade";
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
  }
}

server {
  listen 80;
  server_name api.connecthub.app;
  return 301 https://$server_name$request_uri;
}
```

### 7. Setup SSL with Let's Encrypt
```bash
sudo apt install certbot python3-certbot-nginx
sudo certbot certonly --nginx -d api.connecthub.app
```

## Heroku Deployment

### 1. Install Heroku CLI
```bash
curl https://cli.heroku.com/install.sh | sh
```

### 2. Create Heroku App
```bash
heroku create connecthub-api
heroku addons:create heroku-postgresql:standard-0
heroku addons:create heroku-redis:premium-0
```

### 3. Set Environment Variables
```bash
heroku config:set NODE_ENV=production
heroku config:set JWT_SECRET=your_secret_key
# ... set all other variables
```

### 4. Deploy
```bash
git push heroku main
heroku run npm run migrate
```

## Mobile App Deployment

### iOS App Store
```bash
cd mobile
npm run build
# Follow Expo/Apple guidelines for submission
eas build --platform ios
eas submit --platform ios
```

### Google Play Store
```bash
cd mobile
npm run build
# Follow Expo/Google guidelines
eas build --platform android
eas submit --platform android
```

### Web Deployment
```bash
cd mobile
npm run build
# Deploy 'dist' folder to any static host
# Vercel, Netlify, GitHub Pages, etc.
```

## Database Migrations

### Before Deployment
```bash
npm run migrate
npm run seed  # If needed
```

### Rollback
```bash
npm run migrate:undo
```

## Monitoring & Logging

### Setup Monitoring
- Configure DataDog or New Relic
- Set up error tracking with Sentry
- Configure log aggregation (CloudWatch, ELK)
- Set up performance monitoring

### Key Metrics to Monitor
- API response time
- Database query performance
- WebSocket connection count
- Error rate
- Memory usage
- CPU usage
- Network I/O

## Backup Strategy

### Database Backups
```bash
# Manual backup
pg_dump connecthub > backup.sql

# Automated daily backups (AWS RDS)
# Configured in AWS console
```

### Configuration Backups
- Store .env files securely (e.g., AWS Secrets Manager)
- Version control Docker/infrastructure code
- Document all manual configurations

## Scaling

### Horizontal Scaling
- Add more API server instances
- Use load balancer (AWS ALB, Nginx)
- Configure auto-scaling groups

### Database Scaling
- Enable read replicas
- Implement connection pooling
- Use caching (Redis)

### WebSocket Scaling
- Use Redis Adapter for Socket.io
- Deploy multiple WebSocket servers
- Balance connections across instances

## Performance Optimization

### Before Release
- [ ] Run performance tests
- [ ] Optimize database queries
- [ ] Compress assets
- [ ] Enable caching headers
- [ ] Minimize bundle size

### Production Tuning
- [ ] Enable GZIP compression
- [ ] Configure CDN for static assets
- [ ] Set appropriate cache TTLs
- [ ] Enable database connection pooling
- [ ] Monitor and optimize slow queries

## Rollback Procedure

```bash
# If deployment fails
git revert HEAD
git push heroku main

# Or
heroku releases
heroku rollback v123
```

## Health Checks

### API Health Endpoint
```
GET /health
Response: { "status": "ok", "timestamp": "..." }
```

### Database Health
```
POST /health/db
Response: { "status": "connected" }
```

## Troubleshooting

### Common Issues

**High Memory Usage**
- Check for memory leaks
- Increase Node.js memory limit
- Optimize database queries

**Slow API Response**
- Check database indexes
- Review slow query logs
- Increase Redis cache TTL

**WebSocket Connection Issues**
- Check firewall rules
- Verify Socket.io configuration
- Monitor server load

### Logs
```bash
# View application logs
heroku logs --tail

# AWS CloudWatch
aws logs tail /aws/lambda/connecthub-api --follow
```

## Security Checklist

- [ ] SSL/TLS enabled
- [ ] Environment variables secured
- [ ] Database backups encrypted
- [ ] Firewall rules configured
- [ ] DDoS protection enabled
- [ ] Regular security audits
- [ ] Dependency vulnerability scanning
- [ ] API rate limiting enabled
- [ ] CORS properly configured

## Post-Deployment

1. Monitor application metrics
2. Verify all features working
3. Check error logs
4. Monitor database performance
5. Send deployment notification
6. Update status page
7. Document any issues found
8. Plan follow-up improvements

## Support

For deployment issues:
- Check logs and error messages
- Review monitoring dashboards
- Consult cloud provider documentation
- Reach out to team for assistance
