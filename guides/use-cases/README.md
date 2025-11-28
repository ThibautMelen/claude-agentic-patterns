<div align="center">

[🏠 Home](../../README.md) • [📖 Guides](../README.md) • **📋 Use Cases**

</div>

---

# Real-World Use Cases

> Validated use cases from Anthropic Engineering and production systems

---

## Quick Reference

| Use Case | Pattern | Components |
|----------|---------|------------|
| Multi-Agent Research | 🦑 Orchestrator-Workers | 🐔 Main Agent → Parallel 🐦 Subagents → Synthesis |
| Code Review Pipeline | 🚂 Parallel + 🦑 Subagent | Security, Performance, Style reviewers |
| Multi-Locale Generation | 🧬 Master-Clone + 🧙 Wizard | Primary → Variants in isolation |
| Personal Assistant | 📚 Progressive Skills | Calendar, Email, Tasks routing |
| Customer Support | 🚦 Routing + 🦑 Subagent | Triage → Specialized handlers |
| Data Migration | 🧙 Wizard + 🖥️ Multi-Window | Phased with checkpoints |

---

## Use Case Index

| # | Use Case | File | Patterns |
|---|----------|------|----------|
| 1 | Multi-Agent Research | [multi-agent-research.md](multi-agent-research.md) | 🦑 + 🚂 |
| 2 | Code Review Pipeline | [production-code-review.md](production-code-review.md) | 🚂 + 🦑 |
| 3 | Multi-Locale Generation | [multi-locale-generation.md](multi-locale-generation.md) | 🧬 + 🧙 |
| 4 | Personal Assistant | [intelligent-personal-assistant.md](intelligent-personal-assistant.md) | 📚 |
| 5 | Customer Support | [customer-support-automation.md](customer-support-automation.md) | 🚦 + 🦑 |
| 6 | Data Migration | [data-pipeline-migration.md](data-pipeline-migration.md) | 🧙 + 🖥️ |

---

## Pattern Selection by Use Case

| If your use case involves... | Use Pattern |
|------------------------------|-------------|
| Multiple independent searches | 🚂 Parallel Tool Calling |
| Specialized domain knowledge | 🦑 Orchestrator-Workers |
| Same task on different data | 🧬 Master-Clone |
| Critical/destructive operations | 🧙 Wizard Workflows |
| Long-running workflows (>10 min) | 🖥️ Multi-Window Context |
| External system orchestration | 🎛️ Programmatic Orchestration |
| Intent-based capability loading | 📚 Progressive Skills |

---

<div align="center">

**━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━**

[📖 Guides](../README.md)

</div>
