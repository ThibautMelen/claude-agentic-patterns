<div align="center">

[🏠 Home](../../README.md) • [🔧 Implementation](../README.md) • **📦 Components**

</div>

---

# Claude Code Components

> The 4 abstractions to organize agent capabilities

---

## Components Overview

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart LR
    classDef subagent fill:#ec4899,stroke:#db2777,stroke-width:2px,color:#ffffff
    classDef command fill:#6366f1,stroke:#4f46e5,stroke-width:2px,color:#ffffff
    classDef skill fill:#8b5cf6,stroke:#7c3aed,stroke-width:2px,color:#ffffff
    classDef hook fill:#10b981,stroke:#059669,stroke-width:2px,color:#ffffff

    SA["🐦 Subagent<br/><small>agents/*.md</small>"]:::subagent
    CMD["🦴 Command<br/><small>commands/*.md</small>"]:::command
    SKL["📚 Skill<br/><small>skills/*/</small>"]:::skill
    HK["🪝 Hook<br/><small>settings.json</small>"]:::hook

    SA ~~~ CMD ~~~ SKL ~~~ HK
```

---

## Component Index

| Component | Emoji | File | Purpose |
|-----------|-------|------|---------|
| **Subagent** | 🐦 | [subagent.md](subagent.md) | Autonomous execution |
| **Slash Command** | 🦴 | [slash-command.md](slash-command.md) | User-invoked workflows |
| **Skill** | 📚 | [skill.md](skill.md) | Reusable patterns |
| **Hook** | 🪝 | [hook.md](hook.md) | Automated triggers |

---

## Components Comparison

| Aspect | 🐦 Subagent | 🦴 Slash Command | 📚 Skill | 🪝 Hook |
|--------|-------------|------------------|----------|---------|
| **Invoked by** | Task (🪺) | 🙋‍♀️ User (`/`) | Context | Events |
| **Autonomy** | High | Low | Medium | Auto |
| **Context** | Isolated | Main | Main | System |
| **Spawn subagents** | ❌ | Via 🐔 | Via 🐔 | ❌ |
| **Location** | `agents/*.md` | `commands/*.md` | `skills/*/` | `settings.json` |

---

## Component Relationships

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart TB
    classDef user fill:#6366f1,stroke:#4f46e5,stroke-width:2px,color:#ffffff
    classDef main fill:#8b5cf6,stroke:#7c3aed,stroke-width:2px,color:#ffffff
    classDef subagent fill:#ec4899,stroke:#db2777,stroke-width:2px,color:#ffffff
    classDef skill fill:#8b5cf6,stroke:#7c3aed,stroke-width:2px,color:#ffffff
    classDef builtinTool fill:#64748b,stroke:#475569,stroke-width:2px,color:#ffffff

    subgraph Input["🙋‍♀️ USER INPUT"]
        SLASH["🦴 /command"]:::user
        PROMPT["🙋‍♀️📥 Prompt"]:::user
    end

    subgraph Orchestration["🐔 ORCHESTRATION"]
        MA["🐔💭 Main Agent"]:::main
        SKL["📚 Skills"]:::skill
    end

    subgraph Execution["⚡ EXECUTION"]
        SA["🐦 Subagents"]:::subagent
        TOOLS["🔧 Tools"]:::builtinTool
    end

    SLASH --> MA
    PROMPT --> MA
    MA --> SKL
    MA -->|"🪺 Task"| SA
    SA --> TOOLS

    classDef inputBox fill:#e0e7ff,stroke:#6366f1,stroke-width:2px,color:#3730a3
    classDef orchestrationBox fill:#f3e8ff,stroke:#8b5cf6,stroke-width:2px,color:#5b21b6
    classDef executionBox fill:#fce7f3,stroke:#ec4899,stroke-width:2px,color:#9d174d

    Input:::inputBox
    Orchestration:::orchestrationBox
    Execution:::executionBox
```

---

## File Location Reference

```
.claude/
├── agents/                    # 🐦 Subagent definitions
│   └── *.md                   # One file per subagent type
├── commands/                  # 🦴 Slash Command definitions
│   └── *.md                   # One file per command (name from filename)
├── skills/                    # 📚 Skill definitions
│   └── skill-name/            # One directory per skill (name from dir)
│       └── SKILL.md           # Skill content
└── settings.json              # 🪝 Hooks and configuration
```

---

<div align="center">

**━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━**

[🔧 Implementation](../README.md) • [🏛️ Architecture](../architecture/)

</div>
