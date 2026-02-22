# SmartBrain — AI Orchestration Engine

## Overview

SmartBrain is the intelligent orchestration engine powering CyberAi's automation capabilities. It coordinates multiple specialized agents to perform complex tasks like code auditing, security scanning, automated healing, and intelligent decision-making for blockchain and smart contract development.

**Current Version**: 1.0  
**Status**: ✅ Active

---

## What is SmartBrain?

SmartBrain is a **multi-agent orchestration system** that:

- 🧠 **Coordinates AI Agents**: Manages multiple specialized agents (AgentA-F, AgentX)
- 🔒 **Automates Security**: Performs automated security audits and vulnerability detection
- ⚡ **Optimizes Code**: Suggests gas optimizations and performance improvements
- 🔧 **Self-Heals**: Automatically fixes common issues and maintains system health
- 📊 **Generates Reports**: Creates comprehensive audit reports and documentation

---

## Architecture

```
┌─────────────────────────────────────────────┐
│           SmartBrain Core                    │
│         (master.sh orchestrator)             │
└───────────────┬─────────────────────────────┘
                │
        ┌───────┴────────┬──────────────┐
        │                │              │
┌───────▼──────┐  ┌─────▼─────┐  ┌────▼─────┐
│  Agent Pool  │  │  Workflow  │  │  Logging │
│  A-F, X      │  │  Engine    │  │  System  │
└──────────────┘  └────────────┘  └──────────┘
```

### Core Components

1. **Master Orchestrator** (`scripts/master.sh`)
   - Central coordination hub
   - Agent lifecycle management
   - Workflow execution
   - Error handling and recovery

2. **Agent System**
   - Specialized agents for different tasks
   - Parallel execution support
   - Result aggregation
   - Communication protocol

3. **Workflow Engine**
   - Task scheduling
   - Dependency management
   - Retry logic
   - Status tracking

4. **Logging & Monitoring**
   - Centralized logging (`SMARTBRAIN.log`)
   - Audit report generation
   - Performance metrics
   - Error tracking

---

## Agent System

### Available Agents

#### AgentA — Code Analysis
**Purpose**: Analyzes code structure, patterns, and quality

**Capabilities**:
- Pattern recognition
- Code complexity analysis
- Style consistency checking
- Dependency analysis

**Output**: Analysis report with findings and scores

---

#### AgentB — Security Scanning
**Purpose**: Identifies security vulnerabilities and risks

**Capabilities**:
- Vulnerability pattern detection
- CVE database lookup
- Exploit pattern matching
- Risk scoring

**Output**: Security findings with severity levels

---

#### AgentC — Report Generation
**Purpose**: Creates comprehensive audit reports

**Capabilities**:
- Result aggregation
- Markdown report generation
- Executive summaries
- Actionable recommendations

**Output**: `AUDIT-REPORT.md` with complete findings

---

#### AgentD — Testing & Validation
**Purpose**: Runs tests and validates functionality

**Capabilities**:
- Test execution
- Coverage analysis
- Regression detection
- Performance benchmarking

**Output**: Test results and coverage reports

---

#### AgentE — Optimization
**Purpose**: Identifies optimization opportunities

**Capabilities**:
- Gas optimization (smart contracts)
- Performance profiling
- Resource usage analysis
- Cost-benefit analysis

**Output**: Optimization recommendations with savings estimates

---

#### AgentF — Documentation
**Purpose**: Generates and improves documentation

**Capabilities**:
- Auto-documentation
- Comment quality analysis
- API documentation generation
- Readme improvements

**Output**: Documentation suggestions and generated docs

---

#### AgentX — Custom Extensions
**Purpose**: User-defined custom logic

**Capabilities**:
- Plugin system
- Custom workflows
- Third-party integrations
- Domain-specific logic

**Output**: Custom results based on implementation

---

## Commands

### Health Check

Check system health and dependencies:

```bash
./scripts/master.sh health
```

**Output**:
- Linting status
- Test results
- Type checking
- Dependency status

---

### Audit

Run comprehensive code audit:

```bash
./scripts/master.sh audit
```

**What it does**:
1. Analyzes code patterns (AgentA)
2. Scans for security issues (AgentB)
3. Generates detailed report (AgentC)
4. Creates `AUDIT-REPORT.md`

**Options**:
```bash
# Dry run (no modifications)
DRY_RUN=true ./scripts/master.sh audit

# Production mode
DRY_RUN=false ./scripts/master.sh audit
```

---

### Heal

Auto-heal and optimize the system:

```bash
./scripts/master.sh heal
```

**What it does**:
1. Cleans hanging ports
2. Runs UI healers
3. Fixes common issues
4. Optimizes performance

**Healing Agents**:
- `mega-neo-self-healer-v5.sh` — UI component healing
- `castquest-mega-selfheal.sh` — General healing

---

### Integrity

Validate code integrity and consistency:

```bash
./scripts/master.sh integrity
```

**What it checks**:
- ABI ↔ SDK consistency
- Type definitions
- Contract interfaces
- Data integrity

---

### Scan

Run security scan:

```bash
./scripts/master.sh scan
```

**What it scans**:
- Suspicious file patterns
- Dangerous commands
- Archive files
- Potential malware

**Output**: `.quarantine/` directory with flagged files

---

## Workflow Examples

### Example 1: Full Audit Workflow

```bash
# Step 1: Check system health
./scripts/master.sh health

# Step 2: Run comprehensive audit
./scripts/master.sh audit

# Step 3: Review report
cat AUDIT-REPORT.md

# Step 4: Apply fixes if needed
./scripts/master.sh heal
```

### Example 2: Security-Focused Workflow

```bash
# Step 1: Security scan
./scripts/master.sh scan

# Step 2: Review quarantine
cat .quarantine/suspicious-files.txt

# Step 3: Full audit
./scripts/master.sh audit

# Step 4: Check integrity
./scripts/master.sh integrity
```

### Example 3: Continuous Integration

```yaml
# .github/workflows/smartbrain.yml
name: SmartBrain Audit
on: [push, pull_request]

jobs:
  audit:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Run SmartBrain Health
        run: ./scripts/master.sh health
      
      - name: Run SmartBrain Audit
        run: DRY_RUN=true ./scripts/master.sh audit
      
      - name: Upload Report
        uses: actions/upload-artifact@v3
        with:
          name: audit-report
          path: AUDIT-REPORT.md
```

---

## Configuration

### Environment Variables

```bash
# Core Settings
DRY_RUN=true                    # Safe mode (no modifications)
PNPM=pnpm                       # Package manager
LOG_LEVEL=INFO                  # Logging verbosity
SMARTBRAIN_LOG=SMARTBRAIN.log   # Log file path

# Port Management
CLEAN_PORTS="3000,3001,4000"    # Ports to clean

# Timeouts
HEALTH_CHECK_TIMEOUT=30         # Seconds
AUDIT_TIMEOUT=300               # Seconds

# Features
ENABLE_AUTO_HEAL=true           # Enable auto-healing
ENABLE_ANTIVIRUS=true           # Enable security scanning
```

### Custom Agent Configuration

```bash
# scripts/master.sh
# Customize agent behavior

# Define ports to clean
local ports=(3000 3001 3002 3003 3004 3005 3006 3007 3008 3009 3010 4000)

# Define file patterns to scan
local patterns=(
  "*.json" "*.js" "*.jsx" "*.ts" "*.tsx"
  "*.sol" "*.yml" "*.yaml"
)

# Configure agent execution
AGENT_A_ENABLED=true
AGENT_B_ENABLED=true
AGENT_C_ENABLED=true
```

---

## Integration

### GitHub Actions

SmartBrain integrates seamlessly with GitHub Actions:

```yaml
# .github/workflows/git-antivirus.yml
name: GitAntivirus
on: [push, pull_request]

jobs:
  scan:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: GitAntivirus Scan
        run: |
          chmod +x scripts/*.sh
          ./scripts/master.sh scan
```

### Terminal Integration

SmartBrain powers Terminal AI commands:

```bash
# PR Comment triggers SmartBrain
/terminal review  → SmartBrain audit
/terminal fix     → SmartBrain heal
/terminal audit   → SmartBrain full scan
```

### API Integration

```javascript
// Call SmartBrain via API (planned)
const result = await cyberai.smartbrain.audit({
  repository: 'owner/repo',
  type: 'full',
  agents: ['AgentA', 'AgentB', 'AgentC']
});

console.log(result.report);
```

---

## Logging & Monitoring

### Log File

**Location**: `SMARTBRAIN.log`

**Format**:
```
[TIMESTAMP][AGENT][LEVEL] MESSAGE
[2026-02-07T12:00:00+00:00][AgentA][INFO] Starting analysis...
[2026-02-07T12:00:05+00:00][AgentA][WARN] Potential issue found
[2026-02-07T12:00:10+00:00][AgentA][INFO] Analysis complete
```

### Viewing Logs

```bash
# Tail the log
tail -f SMARTBRAIN.log

# Search for specific agent
grep "AgentA" SMARTBRAIN.log

# Find errors
grep "ERROR" SMARTBRAIN.log

# Watch in real-time
watch -n 1 "tail -20 SMARTBRAIN.log"
```

### Audit Reports

**Location**: `AUDIT-REPORT.md`

**Contents**:
- Executive summary
- Agent findings
- Security issues
- Optimization suggestions
- TODOs and action items

---

## Advanced Features

### Custom Workflows

Create custom workflows by extending the master orchestrator:

```bash
# scripts/custom-workflow.sh
#!/usr/bin/env bash

source scripts/master.sh

custom_workflow() {
  log "INFO" "Starting custom workflow"
  
  # Call agents
  run_agent_a
  run_agent_b
  
  # Custom logic
  echo "Custom processing..."
  
  # Generate report
  run_agent_c
}

custom_workflow
```

### AI Integration

SmartBrain can integrate with AI services:

```javascript
// scripts/SmartBrainConflictResolver.mts
import { OpenAI } from 'openai';

const openai = new OpenAI({
  apiKey: process.env.OPENAI_API_KEY
});

// Use AI for conflict resolution
const analysis = await openai.chat.completions.create({
  model: 'gpt-4',
  messages: [
    { role: 'system', content: 'You are a code review expert' },
    { role: 'user', content: `Analyze this code: ${code}` }
  ]
});
```

---

## Performance

### Optimization Tips

1. **Parallel Execution**:
   ```bash
   # Run agents in parallel
   run_agent_a & run_agent_b & run_agent_c
   wait
   ```

2. **Caching**:
   ```bash
   # Cache results to avoid re-analysis
   if [[ -f ".cache/audit-$SHA" ]]; then
     cat ".cache/audit-$SHA"
     return
   fi
   ```

3. **Incremental Analysis**:
   ```bash
   # Only analyze changed files
   git diff --name-only HEAD~1 | while read file; do
     analyze_file "$file"
   done
   ```

---

## Security Considerations

### Safe Mode (DRY_RUN)

Always test in dry-run mode first:

```bash
# Test without making changes
DRY_RUN=true ./scripts/master.sh audit

# Then apply for real
DRY_RUN=false ./scripts/master.sh audit
```

### Quarantine System

Suspicious files are quarantined, not deleted:

```bash
# Review quarantined files
cat .quarantine/suspicious-files.txt

# Restore if false positive
mv .quarantine/file.js ./file.js
```

### Audit Logging

All operations are logged for transparency:

```bash
# Review all actions
cat SMARTBRAIN.log | grep "MODIFY\|DELETE\|CREATE"
```

---

## Troubleshooting

### Common Issues

**Scripts not executable**:
```bash
chmod +x scripts/*.sh
```

**Permission denied**:
```bash
sudo chown -R $USER:$USER .
```

**Agents not running**:
```bash
# Check logs
tail -f SMARTBRAIN.log

# Verify configuration
./scripts/master.sh health
```

---

## Resources

**Documentation**:
- [Setup Guide](../docs/cuberai-setup.md)
- [Comparison with Other Tools](../docs/smartbrain/COMPARISON.md)
- [Architecture Overview](../docs/audit/CYBERAI_ARCHITECTURE.md)

**Code**:
- `scripts/master.sh` - Main orchestrator
- `scripts/audit.sh` - Audit agent
- `scripts/*-healer*.sh` - Healing agents

**Community**:
- [GitHub Issues](https://github.com/SMSDAO/CyberAi-1/issues)
- [Discussions](https://github.com/SMSDAO/CyberAi-1/discussions)

---

**Last Updated**: 2026-02-07  
**Version**: 1.0  
**Maintainer**: CyberAi Team
