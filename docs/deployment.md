# Deployment Guide

## Prerequisites

- Docker 20.10+ installed
- Access to production environment
- Valid credentials

## Environment Variables

The following environment variables must be set before deployment:

| Variable | Description | Required |
|----------|-------------|----------|
| `DATABASE_URL` | PostgreSQL connection string | Yes |
| `API_SECRET_KEY` | Secret key for JWT signing | Yes |
| `REDIS_URL` | Redis connection string | Yes |
| `LOG_LEVEL` | Logging level (info, warn, error) | No |

## Deployment Steps

1. **Build the application**
   ```bash
   docker build -t test-app:latest .
   ```

2. **Push to registry**
   ```bash
   docker push registry.example.com/test-app:latest
   ```

3. **Deploy to production**
   ```bash
   kubectl apply -f k8s/production.yaml
   ```

## Configuration

Production configuration is stored in `config/production.yaml`.

Key differences from development:
- SSL enabled
- Rate limiting active
- Increased connection pool
- File-based logging

## Rollback

To rollback to a previous version:
```bash
kubectl rollout undo deployment/test-app
```

## Monitoring

Check deployment status:
```bash
kubectl get pods -l app=test-app
```
