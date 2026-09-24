# Environment Variables Reference

## Overview

This document lists all environment variables used across IKEA-Centiro Integration services, with a focus on newly added variables for attachment processing.

**Last Updated:** 2025-12-05

---

## Table of Contents

- [ikea_api_listener](#ikea_api_listener)
- [ikea_api_consumer](#ikea_api_consumer)
- [Common Variables](#common-variables)
- [Quick Setup Guide](#quick-setup-guide)

---

## ikea_api_listener

### MongoDB Configuration

| Variable | Description | Required | Default | Example |
|----------|-------------|----------|---------|---------|
| `MONGODB_CONNECT` | MongoDB connection string | ✅ Yes | - | `mongodb://localhost:27017/zuper_centiro_data` |
| `MONGODB_DATABASE_NAME` | Database name | ✅ Yes | - | `zuper_centiro_data` |

### Server Configuration

| Variable | Description | Required | Default | Example |
|----------|-------------|----------|---------|---------|
| `PORT` | HTTP server port | ✅ Yes | - | `4004` |
| `NODE_ENV` | Environment mode | ❌ No | `development` | `production` |

### RabbitMQ Configuration

| Variable | Description | Required | Default | Example |
|----------|-------------|----------|---------|---------|
| `MQ_HOST` | RabbitMQ host | ✅ Yes | - | `localhost` |
| `MQ_PORT` | RabbitMQ port | ✅ Yes | - | `5672` |
| `MQ_USERNAME` | RabbitMQ username | ✅ Yes | - | `admin` |
| `MQ_PASSWORD` | RabbitMQ password | ✅ Yes | - | `admin` |

### Queue Names

| Variable | Description | Required | Default | Example |
|----------|-------------|----------|---------|---------|
| `MQ_INCOMING_QUEUE` | Main jobs queue | ✅ Yes | - | `ikea_direct_jobs_queue` |
| `MQ_INCOMING_QUEUE_LOG` | Logs queue | ✅ Yes | - | `logs_update_from_party_staging` |
| `MQ_ZUPER_EVENTS_QUEUE` | Zuper webhooks queue | ❌ No | - | `zuper_events_queue_staging` |
| `MQ_ATTACHMENTS_QUEUE` | **NEW:** Attachments queue | ✅ Yes | - | `ikea_direct_attachments_queue` |

### AWS S3 Configuration (NEW)

| Variable | Description | Required | Default | Example |
|----------|-------------|----------|---------|---------|
| `AWS_ACCESS_KEY_ID` | **NEW:** AWS access key | ✅ Yes | - | `AKIAIOSFODNN7EXAMPLE` |
| `AWS_SECRET_ACCESS_KEY` | **NEW:** AWS secret key | ✅ Yes | - | `wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY` |
| `AWS_REGION` | **NEW:** AWS region | ✅ Yes | - | `ap-south-1` |
| `AWS_BUCKET_NAME` | **NEW:** S3 bucket name | ✅ Yes | - | `ps-staging-ap-south-1` |
| `AWS_IKEA_ATTACHMENT_FOLDER` | **NEW:** S3 folder prefix | ❌ No | `ikea_attachments` | `ikea_attachments` |

### Logging

| Variable | Description | Required | Default | Example |
|----------|-------------|----------|---------|---------|
| `LOG_LEVEL` | Log level | ❌ No | `info` | `debug` |

---

## ikea_api_consumer

### MongoDB Configuration

| Variable | Description | Required | Default | Example |
|----------|-------------|----------|---------|---------|
| `MONGODB_CONNECT` | MongoDB connection string | ✅ Yes | - | `mongodb://localhost:27017/zuper_centiro_data` |
| `MONGODB_DATABASE_NAME` | Database name | ✅ Yes | - | `zuper_centiro_data` |

### Server Configuration

| Variable | Description | Required | Default | Example |
|----------|-------------|----------|---------|---------|
| `PORT` | HTTP server port | ✅ Yes | - | `5000` |
| `NODE_ENV` | Environment mode | ❌ No | `development` | `production` |

### RabbitMQ Configuration

| Variable | Description | Required | Default | Example |
|----------|-------------|----------|---------|---------|
| `MQ_HOST` | RabbitMQ host | ✅ Yes | - | `localhost` |
| `MQ_PORT` | RabbitMQ port | ✅ Yes | - | `5672` |
| `MQ_USERNAME` | RabbitMQ username | ✅ Yes | - | `admin` |
| `MQ_PASSWORD` | RabbitMQ password | ✅ Yes | - | `admin` |

### Queue Names

| Variable | Description | Required | Default | Example |
|----------|-------------|----------|---------|---------|
| `MQ_INCOMING_QUEUE` | Main jobs queue | ✅ Yes | - | `ikea_direct_jobs_queue` |
| `MQ_INCOMING_QUEUE_LOG` | Logs queue | ✅ Yes | - | `logs_update_from_party_staging` |
| `MQ_ZUPER_EVENTS_QUEUE` | Zuper webhooks queue | ❌ No | - | `zuper_events_queue_staging` |
| `MQ_ATTACHMENTS_QUEUE` | **NEW:** Attachments main queue | ✅ Yes | - | `ikea_direct_attachments_queue` |

### Dead Letter Queue (DLX) Configuration (NEW)

| Variable | Description | Required | Default | Example |
|----------|-------------|----------|---------|---------|
| `MQ_ATTACHMENTS_DLX_QUEUE` | **NEW:** Dead letter queue name | ✅ Yes | - | `ikea_direct_attachments_dlx_queue` |
| `MQ_ATTACHMENTS_DLX_EXCHANGE` | **NEW:** Dead letter exchange name | ❌ No | `{dlx_queue}_exchange` | `ikea_direct_attachments_dlx_exchange` |
| `MQ_ATTACHMENTS_DLX_TTL_MS` | **NEW:** Retry delay in milliseconds | ❌ No | `30000` | `30000` (30 seconds) |
| `MAX_ATTACHMENT_DLX_RETRIES` | **NEW:** Maximum retry attempts | ❌ No | `10` | `10` |

**DLX Retry Schedule:**
- TTL = 30 seconds
- Max retries = 10
- Total retry time = 5 minutes

### AWS S3 Configuration (NEW)

| Variable | Description | Required | Default | Example |
|----------|-------------|----------|---------|---------|
| `AWS_ACCESS_KEY_ID` | **NEW:** AWS access key | ✅ Yes | - | `AKIAIOSFODNN7EXAMPLE` |
| `AWS_SECRET_ACCESS_KEY` | **NEW:** AWS secret key | ✅ Yes | - | `wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY` |
| `AWS_REGION` | **NEW:** AWS region | ✅ Yes | - | `ap-south-1` |
| `AWS_BUCKET_NAME` | **NEW:** S3 bucket name | ✅ Yes | - | `ps-staging-ap-south-1` |

### Logging

| Variable | Description | Required | Default | Example |
|----------|-------------|----------|---------|---------|
| `LOG_LEVEL` | Log level | ❌ No | `info` | `debug` |

---

## Common Variables

These variables are used across multiple services:

### MongoDB

**Purpose:** Database connection for storing orders, logs, configs, and mappings

**Format:**
- Local: `mongodb://localhost:27017/database_name`
- Atlas: `mongodb+srv://username:password@cluster.mongodb.net/database_name`

**Example:**
```bash
MONGODB_CONNECT=mongodb://localhost:27017/zuper_centiro_data
MONGODB_DATABASE_NAME=zuper_centiro_data
```

### RabbitMQ

**Purpose:** Message queue for asynchronous processing

**Ports:**
- AMQP: `5672`
- Management UI: `15672`

**Example:**
```bash
MQ_HOST=localhost
MQ_PORT=5672
MQ_USERNAME=admin
MQ_PASSWORD=admin
```

### AWS S3

**Purpose:** File storage for attachments

**Required Permissions:**
- `s3:PutObject` (for uploads)
- `s3:GetObject` (for downloads)

**Example:**
```bash
AWS_ACCESS_KEY_ID=AKIAIOSFODNN7EXAMPLE
AWS_SECRET_ACCESS_KEY=wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
AWS_REGION=ap-south-1
AWS_BUCKET_NAME=ps-staging-ap-south-1
```

---

## Quick Setup Guide

### 1. Copy Example Files

```bash
# Listener
cp ikea_api_listener/.env.example ikea_api_listener/.env

# Consumer
cp ikea_api_consumer/.env.example ikea_api_consumer/.env
```

### 2. Configure Required Variables

**Minimum Required:**

```bash
# Both services
MONGODB_CONNECT=mongodb://localhost:27017/zuper_centiro_data
MQ_HOST=localhost
MQ_USERNAME=admin
MQ_PASSWORD=admin

# Attachment support (NEW)
AWS_ACCESS_KEY_ID=your_access_key
AWS_SECRET_ACCESS_KEY=your_secret_key
AWS_BUCKET_NAME=your_bucket_name

# Consumer only (DLX)
MQ_ATTACHMENTS_DLX_QUEUE=ikea_direct_attachments_dlx_queue
```

### 3. Verify Configuration

```bash
# Start listener
cd ikea_api_listener
npm run dev

# Start consumer (different terminal)
cd ikea_api_consumer
npm run dev
```

**Check logs for:**
- ✅ MongoDB connected
- ✅ RabbitMQ connected
- ✅ Queues asserted
- ✅ DLX setup complete (consumer only)

---

## Environment-Specific Configurations

### Development (Local)

```bash
NODE_ENV=development
MONGODB_CONNECT=mongodb://localhost:27017/zuper_centiro_data
MQ_HOST=localhost
AWS_BUCKET_NAME=ps-staging-ap-south-1
```

### Staging

```bash
NODE_ENV=staging
MONGODB_CONNECT=mongodb+srv://user:pass@staging-cluster.mongodb.net/zuper_centiro_data
MQ_HOST=staging-rabbitmq.example.com
AWS_BUCKET_NAME=ps-staging-ap-south-1
MQ_INCOMING_QUEUE=jobs_update_from_party_staging
MQ_ATTACHMENTS_QUEUE=ikea_direct_attachments_queue
```

### Production

```bash
NODE_ENV=production
MONGODB_CONNECT=mongodb+srv://user:pass@prod-cluster.mongodb.net/zuper_centiro_data
MQ_HOST=prod-rabbitmq.example.com
AWS_BUCKET_NAME=ps-production-ap-south-1
MQ_INCOMING_QUEUE=jobs_update_from_party
MQ_ATTACHMENTS_QUEUE=ikea_direct_attachments_queue_prod
```

---

## Security Best Practices

### 1. Never Commit .env Files

```bash
# .gitignore should include:
.env
.env.local
.env.*.local
```

### 2. Use Secrets Management

**Recommended Tools:**
- AWS Secrets Manager
- HashiCorp Vault
- Kubernetes Secrets
- Docker Secrets

**Example with AWS Secrets Manager:**
```javascript
const AWS = require('aws-sdk');
const secretsManager = new AWS.SecretsManager();

async function getSecret(secretName) {
  const data = await secretsManager.getSecretValue({ SecretId: secretName }).promise();
  return JSON.parse(data.SecretString);
}
```

### 3. Rotate Credentials Regularly

- AWS Keys: Every 90 days
- Database Passwords: Every 30 days
- RabbitMQ Passwords: Every 30 days

### 4. Use IAM Roles (AWS)

Instead of access keys, use IAM roles when running on AWS:

```javascript
// No need for AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY
// AWS SDK automatically uses IAM role credentials
AWS.config.update({ region: process.env.AWS_REGION });
```

---

## Troubleshooting

### Missing Environment Variable

**Error:**
```
Error: Missing required environment variable: AWS_ACCESS_KEY_ID
```

**Solution:**
1. Check `.env` file exists
2. Verify variable is set
3. Restart service (environment variables loaded on startup)

### Invalid AWS Credentials

**Error:**
```
AccessDenied: User is not authorized to perform: s3:PutObject
```

**Solution:**
1. Verify IAM permissions
2. Check access key is valid
3. Ensure bucket policy allows access

### RabbitMQ Connection Failed

**Error:**
```
Failed to setup RabbitMQ: Error: connect ECONNREFUSED
```

**Solution:**
1. Check RabbitMQ is running: `sudo systemctl status rabbitmq-server`
2. Verify `MQ_HOST` and `MQ_PORT`
3. Check credentials: `MQ_USERNAME` and `MQ_PASSWORD`

### MongoDB Connection Failed

**Error:**
```
MongoNetworkError: connect ECONNREFUSED
```

**Solution:**
1. Check MongoDB is running: `sudo systemctl status mongod`
2. Verify connection string format
3. Check network firewall rules

---

## Migration Guide

### Upgrading from Previous Version

If you're upgrading from a version without attachment support:

**1. Add New Variables to .env:**

```bash
# ikea_api_listener/.env
AWS_ACCESS_KEY_ID=your_access_key
AWS_SECRET_ACCESS_KEY=your_secret_key
AWS_REGION=ap-south-1
AWS_BUCKET_NAME=ps-staging-ap-south-1
AWS_IKEA_ATTACHMENT_FOLDER=ikea_attachments
MQ_ATTACHMENTS_QUEUE=ikea_direct_attachments_queue

# ikea_api_consumer/.env (additional DLX vars)
MQ_ATTACHMENTS_DLX_QUEUE=ikea_direct_attachments_dlx_queue
MQ_ATTACHMENTS_DLX_EXCHANGE=ikea_direct_attachments_dlx_exchange
MQ_ATTACHMENTS_DLX_TTL_MS=30000
MAX_ATTACHMENT_DLX_RETRIES=10
```

**2. Restart Services:**

```bash
# Stop services
pm2 stop ikea_api_listener ikea_api_consumer

# Start services
pm2 start ikea_api_listener ikea_api_consumer

# Check logs
pm2 logs
```

**3. Verify DLX Setup:**

Check consumer logs for:
```
✓ Dead Letter Exchange setup complete for attachments
  Flow: ikea_direct_attachments_queue → (NACK) → ikea_direct_attachments_dlx_queue (wait 30000ms) → ikea_direct_attachments_queue
```

---

## Validation Checklist

Use this checklist to verify your configuration:

### ikea_api_listener

- [ ] `MONGODB_CONNECT` - Can connect to database
- [ ] `MQ_HOST`, `MQ_USERNAME`, `MQ_PASSWORD` - Can connect to RabbitMQ
- [ ] `MQ_INCOMING_QUEUE` - Queue exists and accessible
- [ ] `MQ_ATTACHMENTS_QUEUE` - Queue exists
- [ ] `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY` - Valid credentials
- [ ] `AWS_BUCKET_NAME` - Bucket exists and accessible
- [ ] Service starts without errors

### ikea_api_consumer

- [ ] `MONGODB_CONNECT` - Can connect to database
- [ ] `MQ_HOST`, `MQ_USERNAME`, `MQ_PASSWORD` - Can connect to RabbitMQ
- [ ] `MQ_INCOMING_QUEUE` - Queue exists and consuming
- [ ] `MQ_ATTACHMENTS_QUEUE` - Queue exists and consuming
- [ ] `MQ_ATTACHMENTS_DLX_QUEUE` - DLX queue created
- [ ] `MQ_ATTACHMENTS_DLX_EXCHANGE` - DLX exchange created
- [ ] `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY` - Valid credentials
- [ ] Service starts without errors
- [ ] DLX setup logs appear

### Testing

- [ ] Can publish order to queue
- [ ] Can upload attachment
- [ ] Attachment stored in S3
- [ ] Attachment queued to RabbitMQ
- [ ] Consumer processes attachment
- [ ] DLX retry works when job not found
- [ ] Attachment uploaded to Zuper
- [ ] Note created in Zuper job

---

## Related Documentation

- **Attachment Flow:** `ATTACHMENT_FLOW_IMPLEMENTATION.md`
- **DLX Implementation:** `ATTACHMENT_DLX_IMPLEMENTATION.md`
- **Architecture:** `CLAUDE.md`
- **Implementation Guide:** `IMPLEMENTATION_GUIDE.md`

---

## Support

For issues or questions:
1. Check logs: `npm run dev` or `pm2 logs`
2. Verify environment variables: `printenv | grep MQ_`
3. Check RabbitMQ UI: `http://localhost:15672`
4. Check MongoDB: `mongosh` or MongoDB Compass
5. Review documentation above

---

**Author:** Claude Code
**Last Updated:** 2025-12-05
**Version:** 2.0 (Attachment Support with DLX)
