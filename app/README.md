# CyberAi Application Layer

## Overview

The CyberAi application layer provides the core business logic and services for the CyberAi platform. This includes bot orchestration, user management, repository integration, and feature coordination across all CyberAi components.

**Status**: 🔄 In Development

---

## Architecture

```
┌─────────────────────────────────────────┐
│         Application Layer                │
├─────────────────────────────────────────┤
│                                          │
│  ┌──────────┐  ┌──────────┐  ┌────────┐│
│  │  Core    │  │  Service │  │  API   ││
│  │  Engine  │  │  Layer   │  │ Gateway││
│  └────┬─────┘  └────┬─────┘  └───┬────┘│
│       │             │             │     │
│       └─────────────┴─────────────┘     │
│                    ↓                     │
│          ┌─────────────────┐            │
│          │  Data Layer     │            │
│          └─────────────────┘            │
└─────────────────────────────────────────┘
```

---

## Core Components

### 1. Application Core

**Purpose**: Central orchestration and business logic

**Responsibilities**:
- Bot lifecycle management
- Event processing
- State management
- Feature coordination
- Error handling and recovery

**Key Modules**:
```
app/
├── core/
│   ├── orchestrator.js      # Main orchestration engine
│   ├── bot-manager.js        # Bot lifecycle
│   ├── event-dispatcher.js   # Event routing
│   └── state-manager.js      # Application state
```

---

### 2. Service Layer

**Purpose**: Business services and domain logic

**Services**:

#### Repository Service
- Repository registration
- Configuration management
- Access control
- Usage tracking

#### Audit Service
- Audit scheduling
- Result aggregation
- Report generation
- Historical tracking

#### User Service
- User authentication
- Profile management
- Preferences
- Notifications

#### Billing Service
- Subscription management
- Usage metering
- Invoice generation
- Payment processing

**Module Structure**:
```
app/
├── services/
│   ├── repository.service.js
│   ├── audit.service.js
│   ├── user.service.js
│   └── billing.service.js
```

---

### 3. Integration Layer

**Purpose**: External system integrations

**Integrations**:

#### GitHub Integration
- GitHub App authentication
- Webhook processing
- API calls (REST & GraphQL)
- Permission management

#### SmartBrain Integration
- Agent coordination
- Result processing
- Workflow execution
- Status monitoring

#### Payment Integration
- Stripe checkout
- Subscription webhooks
- Usage billing
- Refund processing

**Module Structure**:
```
app/
├── integrations/
│   ├── github/
│   │   ├── app.js
│   │   ├── webhooks.js
│   │   └── api-client.js
│   ├── smartbrain/
│   │   ├── orchestrator.js
│   │   └── agent-pool.js
│   └── stripe/
│       ├── checkout.js
│       └── webhooks.js
```

---

### 4. Data Layer

**Purpose**: Data access and persistence

**Components**:

#### Models
- Repository
- User
- Audit
- Subscription
- Webhook

#### Repositories (Data Access)
- CRUD operations
- Query builders
- Caching layer
- Transaction management

**Module Structure**:
```
app/
├── models/
│   ├── repository.model.js
│   ├── user.model.js
│   ├── audit.model.js
│   └── subscription.model.js
├── repositories/
│   └── base.repository.js
└── database/
    ├── connection.js
    └── migrations/
```

---

## Application Flow

### 1. GitHub Webhook Flow

```
GitHub Event
    ↓
Webhook Receiver (app/integrations/github/webhooks.js)
    ↓
Event Dispatcher (app/core/event-dispatcher.js)
    ↓
Service Layer (app/services/*.service.js)
    ↓
SmartBrain Orchestrator (if needed)
    ↓
Response to GitHub
```

### 2. Terminal Command Flow

```
PR Comment: /terminal merge
    ↓
GitHub Webhook: issue_comment
    ↓
App: Parse command
    ↓
Bot Manager: Route to Terminal Bot
    ↓
Terminal Bot: Execute merge
    ↓
GitHub API: Merge PR
    ↓
Response: Post result comment
```

### 3. Audit Flow

```
Trigger: Manual or Scheduled
    ↓
Audit Service: Create audit job
    ↓
SmartBrain Orchestrator: Run audit
    ↓
Agents: Execute analysis
    ↓
Audit Service: Aggregate results
    ↓
Report Generator: Create report
    ↓
Notification: Notify stakeholders
```

---

## Configuration

### Environment Variables

```bash
# Application
NODE_ENV=production
PORT=3000
LOG_LEVEL=info

# Database
DATABASE_URL=postgresql://user:pass@host:5432/cyberai
REDIS_URL=redis://localhost:6379

# GitHub
GITHUB_APP_ID=123456
GITHUB_PRIVATE_KEY=path/to/key.pem
GITHUB_WEBHOOK_SECRET=your-secret

# SmartBrain
SMARTBRAIN_ENABLED=true
SMARTBRAIN_API_KEY=sb-key-xxx

# Stripe
STRIPE_SECRET_KEY=sk_live_xxx
STRIPE_WEBHOOK_SECRET=whsec_xxx

# OpenAI (for AI features)
OPENAI_API_KEY=sk-xxx

# Features
ENABLE_TERMINAL=true
ENABLE_AUTO_AUDIT=true
ENABLE_AI_REVIEW=false
```

### Configuration Files

```javascript
// config/default.js
module.exports = {
  app: {
    name: 'CyberAi',
    version: '1.0.0',
    port: process.env.PORT || 3000
  },
  github: {
    appId: process.env.GITHUB_APP_ID,
    privateKey: process.env.GITHUB_PRIVATE_KEY,
    webhookSecret: process.env.GITHUB_WEBHOOK_SECRET
  },
  features: {
    terminal: {
      enabled: true,
      commands: ['help', 'status', 'merge', 'tag', 'scan']
    },
    smartbrain: {
      enabled: process.env.SMARTBRAIN_ENABLED === 'true',
      agents: ['AgentA', 'AgentB', 'AgentC']
    }
  }
};
```

---

## API Endpoints (Internal)

### Health Check
```http
GET /health
```

### Metrics
```http
GET /metrics
```

### Webhooks
```http
POST /webhooks/github
POST /webhooks/stripe
```

---

## Development

### Setup

```bash
# Install dependencies
npm install

# Copy environment template
cp .env.example .env

# Edit configuration
nano .env

# Run migrations
npm run migrate

# Start development server
npm run dev
```

### Testing

```bash
# Run all tests
npm test

# Run unit tests
npm run test:unit

# Run integration tests
npm run test:integration

# Watch mode
npm run test:watch

# Coverage
npm run test:coverage
```

### Linting

```bash
# Lint code
npm run lint

# Fix auto-fixable issues
npm run lint:fix
```

---

## Deployment

### Build

```bash
# Production build
npm run build

# Output: dist/
```

### Docker

```dockerfile
# Dockerfile
FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
RUN npm ci --only=production

COPY . .

EXPOSE 3000

CMD ["node", "dist/index.js"]
```

```bash
# Build image
docker build -t cyberai-app .

# Run container
docker run -p 3000:3000 --env-file .env cyberai-app
```

---

## Monitoring & Logging

### Logging

```javascript
// Using Winston
const logger = require('./lib/logger');

logger.info('Audit started', { auditId, repository });
logger.error('Audit failed', { auditId, error });
```

### Metrics

- Request rate
- Response time
- Error rate
- Active connections
- Queue depth

### Alerting

- Error rate > 5%
- Response time > 2s
- Queue depth > 100
- Service unavailable

---

## Security

### Best Practices

1. **Secret Management**:
   - Use environment variables
   - Never commit secrets
   - Rotate keys regularly

2. **API Security**:
   - Validate all inputs
   - Rate limiting
   - Authentication required
   - HTTPS only

3. **Webhook Security**:
   - Verify signatures
   - Replay protection
   - IP whitelisting (optional)

4. **Database Security**:
   - Parameterized queries
   - Least privilege access
   - Encrypted connections
   - Regular backups

---

## Troubleshooting

### Common Issues

#### App Won't Start
```bash
# Check logs
tail -f logs/app.log

# Verify database connection
npm run db:check

# Check environment
npm run env:validate
```

#### Webhook Not Working
```bash
# Verify webhook secret
npm run webhook:test

# Check webhook deliveries in GitHub
# Settings → Developer settings → GitHub Apps → Advanced
```

#### High Memory Usage
```bash
# Check memory usage
npm run memory:profile

# Restart workers
pm2 restart cyberai-app
```

---

## Performance Optimization

### Caching Strategy

```javascript
// Redis caching
const cache = require('./lib/cache');

// Cache audit results
await cache.set(`audit:${id}`, results, 3600);

// Retrieve from cache
const cached = await cache.get(`audit:${id}`);
```

### Queue Processing

```javascript
// Bull queue for async jobs
const auditQueue = require('./queues/audit.queue');

// Add job
await auditQueue.add('audit', { 
  repository: 'owner/repo' 
});

// Process jobs
auditQueue.process('audit', async (job) => {
  // Run audit
});
```

---

## Scaling

### Horizontal Scaling

- Load balancer (nginx, AWS ALB)
- Multiple app instances
- Shared Redis cache
- Distributed queue

### Vertical Scaling

- Increase CPU/memory
- Optimize database queries
- Enable caching
- Connection pooling

---

## Resources

**Documentation**:
- [API Documentation](../api/README.md)
- [SmartBrain Integration](../smartbrain/README.md)
- [Terminal Documentation](../docs/terminal/)

**Code Examples**:
- [Bot Templates](../templates/)
- [Integration Examples](./examples/)

**External**:
- [GitHub Apps Docs](https://docs.github.com/en/apps)
- [Node.js Best Practices](https://github.com/goldbergyoni/nodebestpractices)

---

## Contributing

See [CONTRIBUTING.md](../CONTRIBUTING.md) for:
- Code style guidelines
- Testing requirements
- PR process
- Development workflow

---

**Last Updated**: 2026-02-07  
**Status**: In Development  
**Target Release**: Q2 2026
