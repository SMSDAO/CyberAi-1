# Organization Structure — CyberAi + SmartBrain

## Overview

The CyberAi ecosystem is built on a clear organizational structure that separates concerns and enables scalable, modular development.

## Organizational Hierarchy

```
┌─────────────────────────────────────────────┐
│            SolanaRemix Org                   │
│         (Parent Organization)                │
└────────────────┬────────────────────────────┘
                 │
        ┌────────┴────────┐
        │                 │
┌───────▼────────┐  ┌────▼──────────────┐
│   CyberAi      │  │ SmartContract     │
│   Platform     │  │ Audit             │
└───────┬────────┘  └───────────────────┘
        │
   ┌────┴────┬──────────┬────────┐
   │         │          │        │
┌──▼──┐  ┌──▼────┐  ┌──▼────┐  ┌▼────┐
│Core │  │Smart  │  │Term   │  │Web  │
│API  │  │Brain  │  │inal   │  │UI   │
└─────┘  └───────┘  └───────┘  └─────┘
```

## Component Breakdown

### 1. CyberAi (Parent Platform)

**Purpose**: Enterprise automation and orchestration platform for blockchain development

**Key Responsibilities**:
- Overall platform architecture
- Multi-bot coordination
- DAO governance infrastructure
- Partner program management
- Enterprise features and scaling

**Technology Stack**:
- Node.js/TypeScript for backend services
- Shell scripting for automation
- GitHub Actions for CI/CD
- Smart contract integration layer

---

### 2. SmartBrain (AI Engine)

**Purpose**: AI-powered decision engine and automation orchestrator

**Key Responsibilities**:
- Multi-agent coordination (`master.sh`)
- Automated security auditing
- Self-healing and optimization
- Pattern recognition and analysis
- Workflow orchestration

**Technology Stack**:
- Bash scripting for orchestration
- OpenAI integration for AI capabilities
- Custom agent system (AgentA-F, AgentX)
- GitAntivirus security scanning

**Components**:
```
SmartBrain/
├── master.sh              # Central orchestrator
├── audit.sh               # Security audit agent
├── mega-neo-self-healer-v5.sh  # UI healing
├── castquest-mega-selfheal.sh  # Component healing
└── SmartBrainConflictResolver  # Merge conflict resolution
```

**Integration Points**:
- Terminal commands (`/terminal ai`)
- GitHub Actions workflows
- DAO automation
- Partner deployments

---

### 3. Terminal (First Product)

**Purpose**: GitHub mobile terminal for repository control via PR comments

**Target Users**: 
- Mobile developers
- On-the-go maintainers
- Teams needing quick PR operations

**Key Features**:
- Command-based PR interaction
- Mobile-first interface
- SmartBrain integration
- Squash merge automation
- CI/CD triggering

**Command Structure**:
```bash
/terminal help      # Show available commands
/terminal status    # Check PR state
/terminal merge     # Squash merge PR
/terminal tag       # Tag latest commit
/terminal scan      # Run CI scan
/terminal ai        # SmartBrain operations (v0.2+)
```

**Roadmap**:
- **v0.1**: Core terminal commands (status, merge, tag)
- **v0.2**: SmartBrain AI integration (review, fix, audit)
- **v1.0**: Multi-agent orchestration, enterprise features

---

### 4. Web Interface

**Purpose**: Dashboard and web-based control interface

**Key Components**:
- Billing and subscription management
- Analytics and reporting
- Partner portal
- Documentation viewer
- Marketplace integration

**Files**:
```
web/
├── index.html     # Main dashboard
├── billing.html   # Stripe integration
└── audit/         # Audit reports viewer
```

---

### 5. API Layer

**Purpose**: RESTful and webhook API for integrations

**Planned Features**:
- Bot configuration API
- Webhook receivers
- Status and metrics endpoints
- Partner API access

**Current Status**: Placeholder for future development

---

### 6. Dashboard

**Purpose**: Real-time monitoring and control dashboard

**Planned Features**:
- Repository health monitoring
- Audit report aggregation
- DAO governance dashboard
- Partner analytics

**Current Status**: Placeholder for future development

---

## Organizational Principles

### Separation of Concerns

1. **CyberAi (Platform)**: High-level orchestration and business logic
2. **SmartBrain (Engine)**: AI decision-making and automation
3. **Terminal (Product)**: User-facing interface and commands
4. **Components (Modules)**: Specialized functionality (API, Web, Dashboard)

### Integration Model

```
User Request
    ↓
Terminal Command (/terminal ai)
    ↓
CyberAi Platform (routing)
    ↓
SmartBrain Engine (AI processing)
    ↓
Action Execution (scripts/agents)
    ↓
Response to User
```

### Development Workflow

1. **Feature Development**: Start in appropriate component
2. **SmartBrain Integration**: Add AI automation if needed
3. **Terminal Exposure**: Create user-facing commands
4. **API Integration**: Enable external access
5. **Dashboard Visualization**: Add monitoring/control

---

## Team Structure

### Core Maintainers
- Platform architecture
- Security and audits
- Release management
- Governance decisions

### Contributors
- Feature development
- Documentation
- Testing and QA
- Community support

### Partners
- Integration development
- Custom deployments
- Co-marketing initiatives
- Feedback and requirements

See [GOVERNANCE.md](../../GOVERNANCE.md) for decision-making processes.

---

## Repository Organization

### Primary Repository: SmartContractAudit
- Core security infrastructure
- SmartBrain orchestrator
- Base automation scripts
- Documentation
- DAO governance code

### Companion Repository: CyberAi.git
- Advanced bot orchestration
- Production deployments
- Web interfaces
- Partner integrations

See [CYBERAI_ARCHITECTURE.md](../audit/CYBERAI_ARCHITECTURE.md) for detailed architecture.

---

## Naming Conventions

### Branding
- **Organization**: CyberAi (preferred)
- **Legacy Name**: CuberAi (being phased out)
- **AI Engine**: SmartBrain
- **First Product**: Terminal (or "GitHub Mobile Terminal")

### Code Conventions
- **Bot handles**: `@SmartBrain`, `@CyberAi`
- **Command prefix**: `/terminal`
- **Script names**: kebab-case (e.g., `master.sh`)
- **Components**: PascalCase (e.g., `SmartBrainConflictResolver`)

---

## Growth Strategy

### Phase 1: Foundation (Current)
- Core infrastructure
- SmartBrain orchestrator
- Terminal MVP
- Documentation
- DAO planning

### Phase 2: Product Launch
- Terminal v0.1 release
- GitHub Marketplace listing
- Partner onboarding
- SmartBrain AI integration

### Phase 3: Expansion
- Terminal v1.0 with full AI
- API public release
- Dashboard deployment
- Enterprise features
- Multi-chain support

### Phase 4: Ecosystem
- Plugin marketplace
- Third-party integrations
- DAO token launch
- Community governance

---

## Contact & Resources

**Project Organization**: SolanaRemix  
**Primary Repository**: [github.com/SMSDAO/CyberAi-1](https://github.com/SMSDAO/CyberAi-1)  
**Documentation**: [docs/README.md](../README.md)  
**Governance**: [GOVERNANCE.md](../../GOVERNANCE.md)  

For organizational questions, see [partners/contact.md](../partners/contact.md).

---

**Last Updated**: 2026-02-07  
**Document Version**: 1.0
