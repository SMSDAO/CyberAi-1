# CyberAi API Documentation

## Overview

The CyberAi API provides programmatic access to CyberAi Platform features, including SmartBrain orchestration, security auditing, and repository automation. This API enables integrations with external tools, custom workflows, and partner applications.

**Status**: 🔄 In Development (Planned for v1.0)

---

## API Architecture

### Base URL
```
https://api.cyberai.network/v1
```

### Authentication
```http
Authorization: Bearer YOUR_API_TOKEN
```

### API Versioning
- Current: `v1`
- Format: `/v{version}/{endpoint}`
- Version specified in URL path

---

## Core Endpoints

### 1. Repository Management

#### List Repositories
```http
GET /repositories
```

**Response**:
```json
{
  "repositories": [
    {
      "id": "repo_123",
      "owner": "username",
      "name": "my-repo",
      "private": false,
      "smartbrain_enabled": true,
      "last_scan": "2026-02-07T12:00:00Z"
    }
  ],
  "total": 10,
  "page": 1,
  "per_page": 20
}
```

#### Get Repository Details
```http
GET /repositories/:owner/:repo
```

**Response**:
```json
{
  "id": "repo_123",
  "owner": "username",
  "name": "my-repo",
  "private": false,
  "smartbrain_enabled": true,
  "features": {
    "auto_heal": true,
    "security_scan": true,
    "gas_optimization": true
  },
  "statistics": {
    "total_scans": 45,
    "issues_found": 12,
    "issues_resolved": 10
  }
}
```

---

### 2. SmartBrain Operations

#### Trigger Audit
```http
POST /repositories/:owner/:repo/audit
```

**Request Body**:
```json
{
  "type": "full",
  "options": {
    "include_tests": true,
    "check_gas": true,
    "security_level": "high"
  }
}
```

**Response**:
```json
{
  "audit_id": "audit_456",
  "status": "running",
  "started_at": "2026-02-07T12:00:00Z",
  "estimated_completion": "2026-02-07T12:05:00Z"
}
```

#### Get Audit Status
```http
GET /audits/:audit_id
```

**Response**:
```json
{
  "audit_id": "audit_456",
  "status": "completed",
  "started_at": "2026-02-07T12:00:00Z",
  "completed_at": "2026-02-07T12:04:30Z",
  "results": {
    "score": 85,
    "issues": [
      {
        "severity": "medium",
        "type": "security",
        "message": "Potential reentrancy vulnerability",
        "file": "contracts/Token.sol",
        "line": 42,
        "suggestion": "Use ReentrancyGuard"
      }
    ],
    "gas_analysis": {
      "total_gas": 245000,
      "optimizations": 3
    }
  }
}
```

#### Run Healing
```http
POST /repositories/:owner/:repo/heal
```

**Request Body**:
```json
{
  "dry_run": false,
  "targets": ["ports", "ui", "dependencies"]
}
```

**Response**:
```json
{
  "healing_id": "heal_789",
  "status": "completed",
  "actions_taken": [
    "Cleaned port 3000",
    "Fixed UI component",
    "Updated 3 dependencies"
  ]
}
```

---

### 3. Security Scanning

#### Run Security Scan
```http
POST /repositories/:owner/:repo/scan
```

**Request Body**:
```json
{
  "scan_type": "antivirus",
  "patterns": ["*.sol", "*.js"],
  "exclude_paths": ["node_modules/", "test/"]
}
```

**Response**:
```json
{
  "scan_id": "scan_101",
  "status": "completed",
  "threats_found": 2,
  "quarantined": 1,
  "results": [
    {
      "file": "suspicious-file.js",
      "threat": "Obfuscated code pattern",
      "action": "quarantined",
      "severity": "high"
    }
  ]
}
```

---

### 4. Workflow Management

#### List Workflows
```http
GET /repositories/:owner/:repo/workflows
```

**Response**:
```json
{
  "workflows": [
    {
      "id": "workflow_1",
      "name": "Smart Audit",
      "enabled": true,
      "triggers": ["push", "pull_request"],
      "last_run": "2026-02-07T11:00:00Z"
    }
  ]
}
```

#### Execute Workflow
```http
POST /repositories/:owner/:repo/workflows/:workflow_id/execute
```

**Request Body**:
```json
{
  "inputs": {
    "branch": "main",
    "environment": "staging"
  }
}
```

---

### 5. Terminal Commands

#### Execute Terminal Command
```http
POST /terminal/execute
```

**Request Body**:
```json
{
  "repository": "owner/repo",
  "pr_number": 42,
  "command": "status"
}
```

**Response**:
```json
{
  "command_id": "cmd_202",
  "result": {
    "status": "success",
    "output": "PR #42 is ready to merge\n✅ All checks passed\n✅ Approved by 2 reviewers",
    "executed_at": "2026-02-07T12:00:00Z"
  }
}
```

---

### 6. Analytics & Metrics

#### Get Repository Metrics
```http
GET /repositories/:owner/:repo/metrics
```

**Query Parameters**:
- `period`: `day`, `week`, `month`, `year`
- `metrics`: Comma-separated list of metrics

**Response**:
```json
{
  "period": "week",
  "metrics": {
    "scans_run": 15,
    "issues_found": 8,
    "issues_fixed": 6,
    "gas_saved": 25000,
    "commands_executed": 42
  },
  "trend": {
    "scans": "+20%",
    "issues": "-15%"
  }
}
```

---

### 7. Webhook Management

#### List Webhooks
```http
GET /webhooks
```

#### Create Webhook
```http
POST /webhooks
```

**Request Body**:
```json
{
  "url": "https://your-app.com/webhook",
  "events": ["audit.completed", "scan.threat_found"],
  "secret": "your-webhook-secret"
}
```

---

## Webhook Events

### Event Structure
```json
{
  "event": "audit.completed",
  "timestamp": "2026-02-07T12:00:00Z",
  "data": {
    "audit_id": "audit_456",
    "repository": "owner/repo",
    "status": "completed",
    "results": { ... }
  }
}
```

### Available Events

- `audit.started` - Audit begins
- `audit.completed` - Audit finishes
- `audit.failed` - Audit encounters error
- `scan.started` - Security scan begins
- `scan.completed` - Security scan completes
- `scan.threat_found` - Threat detected
- `heal.completed` - Healing operation completes
- `workflow.executed` - Workflow runs
- `terminal.command` - Terminal command executed

---

## Rate Limits

### Tier-Based Limits

| Tier | Requests/Hour | Burst | Concurrent |
|------|---------------|-------|------------|
| **Free** | 60 | 10 | 1 |
| **Pro** | 600 | 50 | 5 |
| **Team** | 3,000 | 100 | 10 |
| **Enterprise** | Custom | Custom | Custom |

### Rate Limit Headers
```http
X-RateLimit-Limit: 600
X-RateLimit-Remaining: 595
X-RateLimit-Reset: 1643990400
```

---

## Error Handling

### Error Response Format
```json
{
  "error": {
    "code": "invalid_request",
    "message": "Repository not found",
    "details": {
      "parameter": "owner",
      "value": "nonexistent-user"
    }
  }
}
```

### HTTP Status Codes

- `200` - Success
- `201` - Created
- `400` - Bad Request
- `401` - Unauthorized
- `403` - Forbidden
- `404` - Not Found
- `429` - Rate Limit Exceeded
- `500` - Internal Server Error
- `503` - Service Unavailable

---

## SDK & Client Libraries

### JavaScript/TypeScript
```bash
npm install @cyberai/sdk
```

```javascript
import { CyberAi } from '@cyberai/sdk';

const client = new CyberAi({
  apiKey: process.env.CYBERAI_API_KEY
});

// Run audit
const audit = await client.repositories.audit('owner/repo', {
  type: 'full',
  options: { check_gas: true }
});

console.log(audit.results);
```

### Python
```bash
pip install cyberai
```

```python
from cyberai import CyberAi

client = CyberAi(api_key=os.env['CYBERAI_API_KEY'])

# Run audit
audit = client.repositories.audit('owner/repo', 
    type='full',
    options={'check_gas': True}
)

print(audit.results)
```

### Go
```bash
go get github.com/cyberai/cyberai-go
```

```go
import "github.com/cyberai/cyberai-go"

client := cyberai.NewClient(os.Getenv("CYBERAI_API_KEY"))

// Run audit
audit, err := client.Repositories.Audit("owner/repo", &cyberai.AuditOptions{
    Type: "full",
    CheckGas: true,
})
```

---

## Authentication & Security

### API Key Management

1. **Generate API Key**:
   - Go to Settings → API Keys
   - Click "Generate New Key"
   - Save securely (shown only once)

2. **Key Types**:
   - **Read-Only**: View data only
   - **Read-Write**: Full access
   - **Admin**: All operations including key management

3. **Best Practices**:
   - Rotate keys regularly
   - Use environment variables
   - Never commit keys to git
   - Use read-only keys when possible

### OAuth 2.0 (Coming Soon)

For user-facing applications:
```
Authorization Code Flow
```

---

## Pagination

### Request
```http
GET /repositories?page=2&per_page=20
```

### Response Headers
```http
Link: <https://api.cyberai.network/v1/repositories?page=3>; rel="next",
      <https://api.cyberai.network/v1/repositories?page=1>; rel="prev",
      <https://api.cyberai.network/v1/repositories?page=10>; rel="last"
```

---

## Filtering & Sorting

### Query Parameters
```http
GET /repositories?
  status=active&
  smartbrain_enabled=true&
  sort=last_scan&
  order=desc
```

---

## API Versioning & Deprecation

### Version Support
- Current: v1 (stable)
- Beta: v2 (preview)
- Deprecated: None yet

### Deprecation Policy
1. **6 months notice** via:
   - API documentation
   - Email notifications
   - Deprecation headers

2. **Sunset Header**:
```http
Sunset: Sat, 01 Aug 2026 00:00:00 GMT
```

---

## Resources & Support

**API Documentation**: https://docs.cyberai.network/api  
**API Status**: https://status.cyberai.network  
**SDKs**: https://github.com/cyberai  
**Support**: api-support@cyberai.example

**Community**:
- GitHub Discussions
- Discord: #api-help channel
- Stack Overflow: `cyberai-api` tag

---

## Changelog

### v1.0 (Planned Q2 2026)
- Initial API release
- Core repository operations
- SmartBrain integration
- Webhook support
- Rate limiting

### Future Releases
- OAuth 2.0 support
- GraphQL API
- WebSocket streaming
- Batch operations
- Advanced analytics

---

**Last Updated**: 2026-02-07  
**API Version**: v1 (planned)  
**Status**: In Development
