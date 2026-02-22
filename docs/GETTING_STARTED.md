# Getting Started with CyberAi

Welcome to **CyberAi** — an AI-powered smart contract security and orchestration platform. This guide will help you get up and running quickly.

---

## 🚀 Quick Start (5 Minutes)

### Step 1: Prerequisites

Before you begin, ensure you have:

- **Git** 2.x or higher
- **Node.js** 24.x or higher
- **pnpm** 8.x or higher (or npm/yarn)
- **Bash** 4.x or higher
- **Operating System**: Linux, macOS, or WSL2 on Windows

### Step 2: Clone the Repository

```bash
git clone https://github.com/SMSDAO/CyberAi-1.git
cd CyberAi-1
```

### Step 3: Install Dependencies

```bash
# Using npm
npm install

# Or using pnpm (recommended)
pnpm install
```

### Step 4: Configure Environment

```bash
# Copy the environment template
cp .env.example .env

# Edit the configuration (start with defaults)
nano .env
```

**Important settings**:
```bash
DRY_RUN=true              # Start in safe mode
PNPM=pnpm                 # Your package manager
LOG_LEVEL=INFO            # Logging verbosity
```

### Step 5: Make Scripts Executable

```bash
chmod +x scripts/*.sh
```

### Step 6: Run Health Check

```bash
./scripts/master.sh health
```

If everything is set up correctly, you should see health check results.

**✅ Congratulations!** You're ready to use CyberAi.

---

## 📚 Next Steps

### Explore Core Features

#### 1. Run Your First Audit

```bash
# Run in safe mode (no modifications)
DRY_RUN=true ./scripts/master.sh audit

# View the audit report
cat AUDIT-REPORT.md
```

#### 2. Try Auto-Healing

```bash
# Auto-heal and optimize
./scripts/master.sh heal
```

#### 3. Run Security Scan

```bash
# Scan for security issues
./scripts/master.sh scan

# Review findings
cat .quarantine/suspicious-files.txt
```

#### 4. Check Integrity

```bash
# Validate code consistency
./scripts/master.sh integrity
```

---

## 🧠 Understanding SmartBrain

SmartBrain is the AI orchestration engine that powers CyberAi. It coordinates multiple agents to perform complex tasks.

### Available Commands

| Command | Purpose | Safety |
|---------|---------|--------|
| `health` | Check system health | ✅ Safe |
| `audit` | Run comprehensive audit | ✅ Safe (dry-run) |
| `heal` | Auto-heal and optimize | ⚠️ Use with DRY_RUN=true first |
| `integrity` | Validate consistency | ✅ Safe |
| `scan` | Security scan | ✅ Safe |

### Command Structure

```bash
./scripts/master.sh <command>
```

**With dry-run**:
```bash
DRY_RUN=true ./scripts/master.sh <command>
```

---

## 🔒 Security Best Practices

### 1. Always Start with Dry-Run

```bash
# Test first
DRY_RUN=true ./scripts/master.sh heal

# Review the logs
cat SMARTBRAIN.log

# Then apply if safe
DRY_RUN=false ./scripts/master.sh heal
```

### 2. Never Commit Secrets

```bash
# Make sure .env is in .gitignore
echo ".env" >> .gitignore
echo "*.key" >> .gitignore
```

### 3. Review Quarantined Files

```bash
# Check what was flagged
cat .quarantine/suspicious-files.txt

# Review each file before taking action
```

### 4. Monitor Logs

```bash
# Tail the log in real-time
tail -f SMARTBRAIN.log

# Search for warnings
grep "WARN" SMARTBRAIN.log

# Check for errors
grep "ERROR" SMARTBRAIN.log
```

---

## 🏗️ Project Structure

```
CyberAi-1/
├── api/                 # API layer (planned)
├── app/                 # Application logic
├── dashboard/           # Web dashboard (planned)
├── dao/                 # DAO governance code
├── docs/                # Documentation
│   ├── audit/           # Audit docs
│   ├── dao/             # DAO docs
│   ├── partners/        # Partnership info
│   ├── smartbrain/      # SmartBrain docs
│   └── terminal/        # Terminal docs
├── scripts/             # SmartBrain scripts
│   ├── master.sh        # Main orchestrator ⭐
│   ├── audit.sh         # Audit agent
│   └── *-healer*.sh     # Healing agents
├── smartbrain/          # SmartBrain components
├── terminal/            # Terminal interface
├── templates/           # Bot templates
├── web/                 # Web interface
├── .env.example         # Environment template
├── package.json         # Dependencies
└── README.md            # Project overview
```

---

## 📖 Essential Documentation

### Core Guides

1. **[Full Setup Guide](cuberai-setup.md)** - Comprehensive installation and configuration
2. **[Architecture Overview](audit/CYBERAI_ARCHITECTURE.md)** - System architecture explained
3. **[SmartBrain Comparison](smartbrain/COMPARISON.md)** - How SmartBrain compares to other tools

### Component Documentation

1. **[Terminal Guide](terminal/index.md)** - GitHub mobile terminal
2. **[DAO Overview](dao/README.md)** - Governance and token distribution
3. **[Partner Program](partners/README.md)** - Partnership opportunities

### For Contributors

1. **[Contributing Guide](../CONTRIBUTING.md)** - How to contribute
2. **[Code of Conduct](../CODE_OF_CONDUCT.md)** - Community standards
3. **[Governance](../GOVERNANCE.md)** - Decision-making process

---

## 🎯 Common Use Cases

### Use Case 1: Smart Contract Auditing

**Goal**: Audit a Solidity smart contract for security issues

```bash
# 1. Place your contract in the repository
cp ~/MyToken.sol contracts/

# 2. Run full audit
./scripts/master.sh audit

# 3. Review the report
cat AUDIT-REPORT.md

# 4. Check for security issues
grep "security" AUDIT-REPORT.md
```

### Use Case 2: Automated PR Management

**Goal**: Manage PRs from mobile using Terminal commands

```bash
# In a GitHub PR comment, type:
/terminal status     # Check PR state
/terminal merge      # Merge the PR
/terminal tag v1.0.0 # Tag the release
```

**Note**: Requires Terminal to be installed as a GitHub App (coming soon).

### Use Case 3: Continuous Integration

**Goal**: Run SmartBrain audits in CI/CD

```yaml
# .github/workflows/audit.yml
name: SmartBrain Audit
on: [push, pull_request]

jobs:
  audit:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Setup
        run: |
          chmod +x scripts/*.sh
          cp .env.example .env
      
      - name: Run Audit
        run: DRY_RUN=true ./scripts/master.sh audit
      
      - name: Upload Report
        uses: actions/upload-artifact@v3
        with:
          name: audit-report
          path: AUDIT-REPORT.md
```

---

## 🔧 Configuration Options

### Environment Variables

```bash
# Core Settings
DRY_RUN=true                    # Safe mode (recommended for testing)
PNPM=pnpm                       # Package manager
LOG_LEVEL=INFO                  # DEBUG, INFO, WARN, ERROR
SMARTBRAIN_LOG=SMARTBRAIN.log   # Log file location

# Port Management
CLEAN_PORTS="3000,3001,4000"    # Ports to clean during heal

# Timeouts (seconds)
HEALTH_CHECK_TIMEOUT=30
AUDIT_TIMEOUT=300

# Feature Flags
ENABLE_AUTO_HEAL=true
ENABLE_ANTIVIRUS=true
```

### Customizing Scripts

Edit `scripts/master.sh` to customize behavior:

```bash
# Define which ports to clean
local ports=(3000 3001 3002 3003 3004 4000)

# Define file patterns to scan
local patterns=(
  "*.json" "*.js" "*.jsx" "*.ts" "*.tsx"
  "*.sol" "*.yml" "*.yaml"
)
```

---

## 🆘 Troubleshooting

### Issue: Scripts Won't Run

**Solution**:
```bash
chmod +x scripts/*.sh
```

### Issue: Permission Denied

**Solution**:
```bash
sudo chown -R $USER:$USER .
```

### Issue: PNPM Not Found

**Solution**:
```bash
npm install -g pnpm
```

### Issue: Port Already in Use

**Solution**:
```bash
./scripts/master.sh heal
```

### Getting More Help

1. **Check logs**:
   ```bash
   cat SMARTBRAIN.log | grep "ERROR"
   ```

2. **Run health check**:
   ```bash
   ./scripts/master.sh health
   ```

3. **Search issues**:
   - [GitHub Issues](https://github.com/SMSDAO/CyberAi-1/issues)
   - [GitHub Discussions](https://github.com/SMSDAO/CyberAi-1/discussions)

4. **Ask the community**:
   - Open a discussion on GitHub
   - Check existing documentation
   - Contact support (see [partners/contact.md](partners/contact.md))

---

## 🤝 Getting Involved

### Ways to Contribute

1. **Report Bugs**: Open an issue if something doesn't work
2. **Suggest Features**: Share ideas for improvements
3. **Improve Documentation**: Help make the docs better
4. **Submit PRs**: Contribute code improvements
5. **Join the DAO**: Participate in governance (see [dao/README.md](dao/README.md))

### First Contribution Ideas

- Fix typos in documentation
- Add examples to guides
- Improve error messages
- Write tests
- Translate documentation

See [CONTRIBUTING.md](../CONTRIBUTING.md) for the full contribution guide.

---

## 📊 What's Next?

### Learning Path

#### Week 1: Basics
- ✅ Complete this guide
- ✅ Run all SmartBrain commands
- ✅ Read the architecture overview
- ✅ Understand the agent system

#### Week 2: Deep Dive
- 📖 Study smart contract auditing
- 📖 Learn about the DAO system
- 📖 Explore partner program
- 📖 Review API documentation

#### Week 3: Advanced
- 🔧 Customize SmartBrain agents
- 🔧 Create custom workflows
- 🔧 Integrate with CI/CD
- 🔧 Build on the API (when released)

#### Week 4: Contribute
- 🤝 Join community discussions
- 🤝 Submit your first PR
- 🤝 Help other users
- 🤝 Participate in governance

---

## 🌟 Success Stories

> "CyberAi's SmartBrain caught a critical reentrancy vulnerability before our mainnet launch. Saved us from a potential disaster!"  
> — DeFi Protocol Developer

> "Terminal commands let me merge PRs from my phone during my commute. Total game-changer for mobile-first development."  
> — Open Source Maintainer

> "The automated audits save us 40+ hours per sprint. It's like having a senior security engineer on the team 24/7."  
> — Smart Contract Security Team

---

## 📞 Support & Resources

**Documentation**: https://docs.cyberai.network (this site)  
**GitHub Repository**: https://github.com/SMSDAO/CyberAi-1  
**Issues**: https://github.com/SMSDAO/CyberAi-1/issues  
**Discussions**: https://github.com/SMSDAO/CyberAi-1/discussions  
**Email**: support@cyberai.example

**Community**:
- Discord: [Invite Link] (coming soon)
- Twitter: [@CyberAi_Dev](https://twitter.com/cyberai_dev) (coming soon)
- YouTube: [CyberAi Channel] (coming soon)

---

## 🎉 Welcome to CyberAi!

You're now ready to start using CyberAi. Remember:

1. **Start with dry-run mode** (`DRY_RUN=true`)
2. **Review logs and reports** before taking action
3. **Ask for help** if you need it
4. **Contribute back** to make CyberAi better for everyone

Happy coding! 🚀

---

**Last Updated**: 2026-02-07  
**Version**: 1.0  
**Feedback**: [Open an issue](https://github.com/SMSDAO/CyberAi-1/issues/new) to improve this guide
