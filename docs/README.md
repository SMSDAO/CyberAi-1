# CyberAi Documentation

Welcome to the comprehensive documentation for **CyberAi** (formerly CuberAi) - an AI-powered smart contract security and orchestration platform for blockchain development.

## 📚 Table of Contents

### 🚀 Getting Started
- [Quick Start Guide](#quick-start)
- [Installation & Setup](cuberai-setup.md)
- [Architecture Overview](audit/CYBERAI_ARCHITECTURE.md)
- [Contributing Guidelines](../CONTRIBUTING.md)

### 🏗️ Core Components

#### SmartBrain Orchestrator
- [Setup & Configuration](cuberai-setup.md) - Complete installation and configuration guide
- [Comparison with Other Tools](smartbrain/COMPARISON.md) - Feature comparison with SunkBot and Dependabot
- [Architecture](audit/CYBERAI_ARCHITECTURE.md) - System architecture and component overview

#### Terminal
- [Terminal Overview](terminal/index.md) - GitHub mobile terminal interface
- [SmartBrain Integration](terminal/smartbrain.md) - AI-powered terminal commands
- [Branding Guidelines](terminal/branding.md) - Brand architecture and guidelines
- [Marketplace](terminal/marketplace.md) - GitHub marketplace integration
- [Organization Structure](terminal/org-structure.md) - CyberAi organizational structure

### 🔒 Security & Auditing
- [Security Policy](../SECURITY.md) - Vulnerability reporting and security practices
- [Audit Workflows](audit/) - Security scanning and audit processes
- [Quick Reference](audit/CYBERAI_QUICKREF.md) - Quick command reference
- [PR Merge Guide](audit/CYBERAI_PR_MERGE_GUIDE.md) - Safe PR merging practices

### 🏛️ DAO & Governance
- [DAO Overview](dao/README.md) - Introduction to the SmartContractAudit DAO
- [Eligibility Criteria](dao/eligibility.md) - Who can participate
- [Scoring System](dao/scoring.md) - How contributions are valued
- [Snapshot Process](dao/snapshot.md) - Taking periodic snapshots
- [Merkle Distribution](dao/merkle.md) - Token distribution mechanism
- [Claiming Tokens](dao/claiming.md) - How to claim your tokens
- [Governance](../GOVERNANCE.md) - Project governance structure

### 🤝 Partnerships & Community
- [Partner Program](partners/README.md) - Partnership opportunities
- [Sponsorship Tiers](partners/sponsorship_tiers.md) - Support the project
- [Technical Onboarding](partners/technical_onboarding.md) - Partner integration guide
- [Use Cases](partners/use_cases.md) - Real-world applications
- [Data Privacy](partners/data_privacy.md) - Privacy policy and data handling
- [SLA & Support](partners/sla_and_support.md) - Service level agreements
- [Contact Information](partners/contact.md) - Get in touch
- [Press Kit](partners/press_kit.md) - Media resources

### 📦 Release Management
- [Release Process](release-process.md) - Complete release workflow
- [Release Checklist](../RELEASE.md) - Pre-release verification
- [Migration Guide](../MIGRATION.md) - Version migration instructions

### 📋 Policies & Guidelines
- [Code of Conduct](../CODE_OF_CONDUCT.md) - Community standards
- [Privacy Policy](../PRIVACY.md) - How we handle user data
- [Data Retention](../DATA_RETENTION.md) - Data storage and retention policies
- [License](../LICENSE) - Apache 2.0 License

### 📝 Additional Resources
- [Followup Notes](followup/) - Development followup documentation
- [TRIO Methodology](../TRIO.md) - Development approach
- [Funding](../FUNDING.yml) - Support the project

---

## Quick Start

### Prerequisites
- **Operating System**: Linux, macOS, or WSL2 on Windows
- **Node.js**: 16.x or higher
- **pnpm**: 8.x or higher (or npm)
- **Bash**: 4.x or higher
- **Git**: 2.x or higher

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/SMSDAO/CyberAi-1.git
cd CyberAi-1

# 2. Install dependencies
npm install

# 3. Copy environment template
cp .env.example .env

# 4. Configure environment
nano .env  # Set DRY_RUN=true for testing

# 5. Make scripts executable
chmod +x scripts/*.sh

# 6. Run health check
./scripts/master.sh health
```

### First Steps

1. **Explore the Documentation**: Start with [cuberai-setup.md](cuberai-setup.md) for detailed setup
2. **Understand the Architecture**: Read [CYBERAI_ARCHITECTURE.md](audit/CYBERAI_ARCHITECTURE.md)
3. **Join the Community**: See [CONTRIBUTING.md](../CONTRIBUTING.md) to get involved
4. **Learn about DAO**: Check [dao/README.md](dao/README.md) for governance info

### Key Commands

```bash
# Run comprehensive audit
./scripts/master.sh audit

# Auto-heal and optimize
./scripts/master.sh heal

# Check integrity
./scripts/master.sh integrity

# System health check
./scripts/master.sh health

# Security scan
./scripts/master.sh scan
```

For detailed usage, see [cuberai-setup.md](cuberai-setup.md#usage).

---

## Project Structure

```
CyberAi-1/
├── api/              # API components
├── app/              # Application code
├── dashboard/        # Dashboard interface
├── dao/              # DAO-related code and tools
├── docs/             # Documentation (you are here)
│   ├── audit/        # Audit and security docs
│   ├── dao/          # DAO documentation
│   ├── partners/     # Partnership docs
│   ├── smartbrain/   # SmartBrain documentation
│   ├── terminal/     # Terminal documentation
│   └── followup/     # Development notes
├── scripts/          # Automation scripts
├── smartbrain/       # SmartBrain components
├── terminal/         # Terminal interface
├── templates/        # Bot templates
└── web/              # Web interface
```

---

## Documentation Conventions

### Placeholders
Throughout the documentation, you may see placeholder values:
- **Email addresses**: `*@cuberai.example` (replace with actual domain when deployed)
- **Domains**: Some references to future deployment domains
- **TBD/TODO**: Items marked for future completion

### Status Indicators
- ✅ **Production Ready** - Fully implemented and tested
- 🟡 **Beta/Partial** - Available but still in development
- ❌ **Not Available** - Planned for future releases
- 💎 **Crypto-Specific** - Blockchain/Web3 features
- 🔒 **Security-Focused** - Security-related features
- ⚡ **Performance** - Optimization features

---

## Contributing to Documentation

Documentation improvements are welcome! To contribute:

1. **Fix typos or errors**: Submit a PR with corrections
2. **Improve clarity**: Suggest better explanations
3. **Add examples**: Provide practical examples
4. **Update outdated info**: Keep documentation current
5. **Fill gaps**: Add missing documentation

See [CONTRIBUTING.md](../CONTRIBUTING.md) for the contribution process.

---

## Getting Help

- **GitHub Issues**: [Report bugs or request features](https://github.com/SMSDAO/CyberAi-1/issues)
- **GitHub Discussions**: [Ask questions and discuss ideas](https://github.com/SMSDAO/CyberAi-1/discussions)
- **Documentation**: Search through this documentation
- **Contact**: See [partners/contact.md](partners/contact.md) for contact options

---

## Related Repositories

**CyberAi Ecosystem**:
- **SmartContractAudit**: Core smart contract security tools (this repository)
- **CyberAi.git**: AI-powered bot orchestration (separate repository)
- Part of the **SolanaRemix** organization

See [CYBERAI_ARCHITECTURE.md](audit/CYBERAI_ARCHITECTURE.md) for details on repository separation.

---

## License

This project is licensed under the Apache License 2.0. See [LICENSE](../LICENSE) for details.

---

**Last Updated**: 2026-02-07  
**Documentation Version**: 1.0  
**Project Status**: Active Development

For the latest updates, visit [github.com/SMSDAO/CyberAi-1](https://github.com/SMSDAO/CyberAi-1)
