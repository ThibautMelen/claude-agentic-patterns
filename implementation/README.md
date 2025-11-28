<div align="center">

[🏠 Home](../README.md) • **🔧 Implementation**

</div>

---

# Implementation

> How Claude Code implements agentic patterns through components and architecture

---

## Components vs Building Block

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                                                                             │
│  🧱 BUILDING BLOCK (Anthropic)         COMPONENTS (Claude Code)            │
│  ─────────────────────────────         ────────────────────────            │
│                                                                             │
│  Augmented LLM                         🐦 Subagent                         │
│  (LLM + Retrieval + Tools + Memory)    🦴 Slash Command                    │
│                                         📚 Skill                            │
│  → Foundation concept                   🪝 Hook                             │
│                                                                             │
│  Each Component internally uses         → Abstractions that organize        │
│  the Building Block to function         agent capabilities                  │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Navigation

| Section | Description |
|---------|-------------|
| [components/](components/) | 🐦 Subagent, 🦴 Slash Command, 📚 Skill, 🪝 Hook |
| [architecture/](architecture/) | 5-Layer system architecture |

---

## Quick Reference

### Components Overview

| Component | Emoji | Invocation | Location |
|-----------|-------|------------|----------|
| **Subagent** | 🐦 | Task tool (🪺) | `.claude/agents/*.md` |
| **Slash Command** | 🦴 | User `/command` | `.claude/commands/*.md` |
| **Skill** | 📚 | Context-based | `.claude/skills/*/SKILL.md` |
| **Hook** | 🪝 | Event-driven | `.claude/settings.json` |

### Architecture Overview

| Layer | Emoji | Role |
|-------|-------|------|
| **User Layer** | 🙋‍♀️ | Entry point |
| **Main Agent Layer** | 🐔 | Orchestration |
| **Delegation Layer** | 🔀 | Workflow definition |
| **Execution Layer** | ⚡ | Actual work |
| **State Layer** | 💾 | Persistence |

---

## File Structure

```
.claude/
├── agents/                    # 🐦 Subagent definitions
│   └── *.md                   # One file per subagent type
├── commands/                  # 🦴 Slash Command definitions
│   └── *.md                   # One file per command
├── skills/                    # 📚 Skill definitions
│   └── skill-name/            # One directory per skill
│       └── SKILL.md           # Skill content
└── settings.json              # 🪝 Hooks and configuration
```

---

<div align="center">

**━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━**

[🏠 Home](../README.md) • [📚 Concepts](../concepts/)

</div>
