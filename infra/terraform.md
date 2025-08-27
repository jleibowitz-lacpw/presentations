---
marp: true
theme: default
paginate: true
---

# **From ClickOps to DevOps**
## Automating Uptime Robot with Terraform

August 2025

---

## Current Challenge: ClickOps

- **Manual configuration** of Uptime Robot through web UI
- Changes require **direct human interaction**
- Limited audit trail of "who changed what and when"
- No version control for configuration changes
- Difficult to reproduce exact setups across environments
- Time-consuming and error-prone processes

---

## What is Terraform?

- **Infrastructure as Code (IaC)** tool
- Define infrastructure in declarative configuration files
- **Plan** changes before applying them
- **Apply** changes in a controlled, systematic way
- **Track** all changes in version control
- **Automate** provisioning through CI/CD pipelines

---

## What is Uptime Robot?

- External monitoring service we currently use
- Monitors our websites, services, and APIs
- Sends alerts when issues are detected
- Currently configured manually through web UI

---

## The DevOps Vision

- Code-defined infrastructure
- Version-controlled configurations
- Automated workflows
- Repeatable processes
- Self-documenting systems
- Collaborative approach

---

## Introducing: Terraform Provider for Uptime Robot

- Official provider by Uptime Robot
- GitHub: `uptimerobot/terraform-provider-uptimerobot`
- Allows managing Uptime Robot resources as code
- Seamlessly integrates with our existing Terraform workflows
- Supported by a growing community

---

## What Can We Manage with the Provider?

### Define:
**Monitor Resources:**
- HTTP(S) monitors
- Ping monitors
- Port monitors
- Keyword monitors

---
**Alert/Notification Resources:**
- Alert contacts
- Alert rules and conditions
- Notification delivery methods
- Maintenance windows

---

## Benefits

- **Consistency**: Same configuration across all environments
- **Auditability**: Git history shows who changed what and when
- **Automation**: Changes through Azure DevOps pipelines
- **Collaboration**: Multiple teams can contribute through PRs
- **Disaster Recovery**: Quickly restore monitoring if needed
- **Documentation**: Config files serve as living documentation

---

## Integration with Our Tools

**Azure DevOps:**
- Store Terraform configs in repos
- Trigger pipelines for changes
- Gate approvals for production changes
- Schedule automated runs

---

**GitHub Enterprise:**
- Version control for all changes
- Pull request workflow for reviews
- Branch protection rules
- Actions for validation (future)

---

## Proof of Concept Roadmap

1. **Setup**: Install provider and basic configuration
2. **Import**: Bring existing monitors under management
3. **Teamwork**: Define collaboration workflow
4. **CI Integration**: Setup Azure DevOps pipelines
5. **Documentation**: Create internal knowledge base
6. **Expansion**: Add more monitoring resources

---

## From Manual to Automated

| ClickOps (Current) | DevOps (Future) |
|--------------------|-----------------|
| Manual UI changes | Code changes in repositories |
| No clear audit trail | Complete history in Git |
| Tribal knowledge | Self-documenting configs |
| One person at a time | Collaborative reviews |
| Easy to make mistakes | Validation before apply |
| Slow, repetitive work | Fast, automated processes |

---

## Security & Compliance Benefits

- **Least privilege access** model
- **Approval workflows** for sensitive changes
- **Encrypted** secrets management
- **Audit logs** for compliance reporting
- **Consistent** security practices
- **Standardized** configuration policies

---

## Real-World Example: Monitor Lifecycle

Without showing code, here's what the workflow looks like:

1. Engineer creates PR with new monitor definition
2. Team reviews configuration in Azure DevOps
3. Approval triggers pipeline execution
4. Terraform creates resources in Uptime Robot
5. Changes and results are documented automatically
6. Everything is tracked for future reference

---

## Next Steps

1. Schedule initial POC workshop
2. Set up sandbox environment
3. Import a subset of existing monitors
4. Create first Azure DevOps pipeline
5. Develop team workflow guidelines
6. Present results to management

---

# Questions?

**Resources:**
- Provider Documentation: https://registry.terraform.io/providers/uptimerobot/uptimerobot/latest/docs
- Terraform Learning: https://learn.hashicorp.com/terraform

---

# Thank You!
