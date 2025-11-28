<div align="center">

[🏠 Home](../README.md) › [📖 Reference](./) › **Visual Standards**

[← Glossary](glossary.md) ━━━━━━━━━━━━━━━━━●━━━━━━━━━━━━━━━━━━ [Built-in Subagents →](built-in-subagents.md)

</div>

---

# Visual Standards

> WHO does WHAT — colors, emojis, and diagram standards

---

## ACTEUR + ACTION System

Visual language answering: **WHO does WHAT?**

---

## Acteurs (WHO)

| Acteur | Emoji | Color | Description |
|--------|-------|-------|-------------|
| **User (neutral)** | 🙆‍♀️ | Indigo `#6366f1` | Human idle state |
| **User (input)** | 🙋‍♀️ | Indigo `#6366f1` | Human sends input |
| **User (output)** | 💁‍♀️ | Indigo `#6366f1` | Human receives output |
| **Main Agent** | 🐔 | Purple `#8b5cf6` | Claude Code orchestrator |
| **Subagent** | 🐦 | Pink `#ec4899` | Delegated worker |

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  THE POULTRY FAMILY                                                         │
│                                                                             │
│  USER STATES:           AGENTS:                                             │
│  🙆‍♀️ neutral (idle)      🐔 Main Agent → orchestrates (can spawn 🐦)        │
│  🙋‍♀️ gives (input)       🐦 Subagent   → executes (cannot spawn other 🐦)   │
│  💁‍♀️ receives (output)                                                      │
│                                                                             │
│  HIERARCHY: 🙋‍♀️📥 → 🐔 → 🐦 → 📤💁‍♀️                                           │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Actions (WHAT)

| Action | Emoji | Description | Example |
|--------|-------|-------------|---------|
| **Input** | 📥 | Data enters | 🙋‍♀️📥 |
| **Output** | 📤 | Data exits | 🐔📤, 📤💁‍♀️ |
| **Thinking** | 💭 | Reasons/prompts | 🐔💭 |
| **Routing** | 🚦 | Decides direction | 🐔🚦 |
| **Spawn** | 🪺 | Creates subagent | 🐔🪺 |
| **Execute** | ⚡ | Runs task | 🐦⚡ |
| **Observe** | 👀 | Reads | 🐔👀 |
| **Write** | ✏️ | Modifies | 🐦✏️ |
| **Validate** | ✅ | Approves | 🙆‍♀️✅ |
| **Question** | ❓ | Asks | 🐔❓ |
| **Split** | 🔀 | Divides task | 🐔🔀 |
| **Merge** | 🌀 | Combines results | 🐔🌀 |
| **Plan** | 📋 | Creates plan | 🐔📋 |
| **Adjust** | 🔄 | Loops/iterates | 🐔🔄 |
| **Continue** | ▶️ | Resumes | 🐔▶️ |
| **Idle** | 💤 | Not chosen | 🐦💤 |

> **📥/📤 Position Rule:** `ACTEUR📥` = sends in, `ACTEUR📤` = produces, `📤ACTEUR` = receives

---

## Combinations Matrix

### USER 🙆‍♀️🙋‍♀️💁‍♀️

| Combo | Meaning |
|-------|---------|
| 🙆‍♀️ | Idle state |
| 🙋‍♀️📥 | Sends input |
| 🙆‍♀️✅ | Validates |
| 🙆‍♀️❓ | Questions |
| 📤💁‍♀️ | Receives output |

### MAIN AGENT 🐔

| Combo | Meaning |
|-------|---------|
| 🐔💭 | Thinks |
| 🐔🚦 | Routes |
| 🐔🪺 | Spawns |
| 🐔🔀 | Splits |
| 🐔🌀 | Merges |
| 🐔📋 | Plans |
| 🐔📤 | Outputs |
| 🐔⚡ | Executes |
| 🐔👀 | Observes |
| 🐔✏️ | Writes |
| 🐔🔄 | Loops |
| 🐔▶️ | Continues |

### SUBAGENT 🐦

| Combo | Meaning |
|-------|---------|
| 🐦💭 | Thinks |
| 🐦⚡ | Executes |
| 🐦👀 | Observes |
| 🐦✏️ | Writes |
| 🐦📤 | Returns |
| 🐦✅ | Validates |
| 🐦💤 | Idle |

---

## Status & Triggers

### Status Indicators

| Status | Emoji | Color | Use Case |
|--------|-------|-------|----------|
| **Success** | ✅ | Emerald `#10b981` | Task completed |
| **Error** | ❌ | Red `#ef4444` | Failure |
| **Warning** | ⚠️ | Amber `#f59e0b` | Caution needed |
| **In Progress** | 🔄 | Blue `#3b82f6` | Currently running |
| **Pending** | ⏳ | Slate `#64748b` | Waiting |
| **Skip** | ⏭️ | Slate `#64748b` | Bypassed |

### Triggers & State

| Element | Emoji | Color | Description |
|---------|-------|-------|-------------|
| **Hook** | 🪝 | Emerald `#10b981` | Event-driven automation |
| **State/Data** | 💾 | Emerald `#10b981` | Persisted data |

### Hook Events

| Event | Trigger | Use Case |
|-------|---------|----------|
| `PreToolUse` | Before tool execution | Validation, blocking |
| `PostToolUse` | After tool completion | Cleanup, formatting |
| `PermissionRequest` | Permission dialogs | Auto-allow/deny |
| `UserPromptSubmit` | Before processing input | Pre-processing |
| `SessionStart` | Session starts/resumes | Environment setup |
| `SessionEnd` | Session ends | Cleanup |
| `Stop` | Claude finishes | Post-response actions |
| `SubagentStop` | Subagent completes | Subagent cleanup |
| `PreCompact` | Before compact | Lifecycle management |
| `Notification` | Notifications sent | Custom notifications |

---

## Tools

### By Source

| Source | Emoji | Color | Description |
|--------|-------|-------|-------------|
| **Built-in** | 🔧 | Slate `#64748b` | Native Claude Code tools |
| **External (MCP)** | 🔌 | Amber `#f59e0b` | Model Context Protocol servers |

### Built-in Tools 🔧

| Category | Combo | Tools |
|----------|-------|-------|
| Read File | 🔧👀 | Read |
| Search Content | 🔧🔍 | Grep |
| Search Files | 🔧🗂️ | Glob |
| Write Ops | 🔧✏️ | Write, Edit, NotebookEdit |
| Shell Ops | 🔧📟 | Bash, BashOutput, KillShell |
| Web Ops | 🔧🌐 | WebFetch, WebSearch |
| User Interaction | 🔧❓ | AskUserQuestion |
| Planning | 🔧📋 | TodoWrite |
| Spawn | 🪺 | Task (spawns 🐦 Subagent) |

---

## Color Palette

| Color | Hex | Usage |
|-------|-----|-------|
| 🟣 Indigo | `#6366f1` | User 🙋‍♀️, Slash Commands 🦴 |
| 🟣 Purple | `#8b5cf6` | Main Agent 🐔, Skills 📚 |
| 🩷 Pink | `#ec4899` | Subagent 🐦 |
| 🟠 Amber | `#f59e0b` | MCP Tools 🔌, Warning ⚠️ |
| 🟢 Emerald | `#10b981` | State 💾, Success ✅, Hook 🪝 |
| 🔵 Blue | `#3b82f6` | Parallel 🛤️, Progress 🔄 |
| 🔴 Red | `#ef4444` | Errors ❌ |
| 🩶 Slate | `#64748b` | Built-in 🔧, Neutral |
| 🩶 Slate-400 | `#94a3b8` | Idle 💤 |
| 🩵 Teal | `#14b8a6` | Wizard 🧙 |
| 🩵 Cyan | `#06b6d4` | Data flow |

---

## Mermaid Class Definitions

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart TB
    %% Acteurs
    classDef user fill:#6366f1,stroke:#4f46e5,stroke-width:2px,color:#ffffff
    classDef main fill:#8b5cf6,stroke:#7c3aed,stroke-width:2px,color:#ffffff
    classDef subagent fill:#ec4899,stroke:#db2777,stroke-width:2px,color:#ffffff
    classDef skill fill:#8b5cf6,stroke:#7c3aed,stroke-width:2px,color:#ffffff

    %% Tools (by source)
    classDef builtinTool fill:#64748b,stroke:#475569,stroke-width:2px,color:#ffffff
    classDef mcpTool fill:#f59e0b,stroke:#d97706,stroke-width:2px,color:#ffffff

    %% Other
    classDef state fill:#10b981,stroke:#059669,stroke-width:2px,color:#ffffff
    classDef wizard fill:#14b8a6,stroke:#0d9488,stroke-width:2px,color:#ffffff
    classDef parallel fill:#3b82f6,stroke:#2563eb,stroke-width:2px,color:#ffffff
    classDef error fill:#ef4444,stroke:#dc2626,stroke-width:2px,color:#ffffff
    classDef idle fill:#94a3b8,stroke:#64748b,stroke-width:2px,color:#ffffff
```

---

## Subgraph Styles

```
style L1 fill:#e0e7ff,stroke:#6366f1,stroke-width:2px  %% User Layer
style L2 fill:#f3e8ff,stroke:#8b5cf6,stroke-width:2px  %% Main Agent
style L3 fill:#fce7f3,stroke:#ec4899,stroke-width:2px  %% Subagent
style L4 fill:#fef3c7,stroke:#f59e0b,stroke-width:2px  %% Tools
style L5 fill:#ecfdf5,stroke:#10b981,stroke-width:2px  %% State
```

---

## Symbol Key (for Diagrams)

| Symbol | Meaning |
|--------|---------|
| `[Rectangle]` | Process/Component |
| `{Diamond}` | Decision point |
| `((Circle))` | Start/End |
| `-->` | Sequential flow |
| `-.->` | Optional/async flow |
| `-->│` | Parallel flow |

---

## Rules

| ✅ Do | ❌ Don't |
|-------|---------|
| Always use ACTEUR + ACTION | 🧠 for Main Agent (use 🐔) |
| Use classDef (never inline) | 🤖 for Subagent (use 🐦) |
| White text on dark fills | 👤 for User (use 🙋‍♀️) |
| 2px stroke-width | Random colors |

---

## Official Terms

| ✅ Correct | ❌ Avoid |
|------------|----------|
| 🐦 Subagent | Sub-agent, child agent |
| 🦴 Slash Command | Command, slash-command |
| 📚 Skill | Capability, ability |
| 🪝 Hook | Trigger, event handler |
| 🐔 Main Agent | Parent agent, orchestrator |
| Task (🪺 spawn) | Task tool, delegate |
| 🙋‍♀️ User (input) | 👤 User |
| 🔧 Built-in | Native Tool, 🛠️ Tool |
| 🔌 External (MCP) | API tool |

---

## In Documentation

```markdown
# ✅ Good
The 🐔 Main Agent 🪺 spawns a 🐦 Subagent via the Task tool.
🙋‍♀️ Users invoke /generate to trigger the workflow.

# ❌ Avoid
The parent spawns a child agent.
Users run the generate command.
```

---

## Pattern Emoji Reference

| Emoji | Pattern | Type |
|-------|---------|------|
| 🏎️ | Direct Execution | Baseline (#0) |
| ⛓️ | Prompt Chaining | Workflow (#1) |
| 🚦 | Routing | Workflow (#2) |
| 🛤️ | Parallelization | Workflow (#3) |
| 🦑 | Orchestrator-Workers | Workflow (#4) |
| 🩻 | Evaluator-Optimizer | Workflow (#5) |
| 🐉 | Autonomous Agents | Agent (#6) |
| 🧙 | Wizard Workflows | Variant |
| 🚂 | Parallel Tool Calling | Variant |
| 🧬 | Master-Clone | Variant |
| 🖥️ | Multi-Window Context | Variant |
| 📚 | Progressive Skills | Mechanism |
| 🎛️ | Programmatic Orchestration | Mechanism |

---

<div align="center">

[← Glossary](glossary.md) ━━━━━━━━━━━━━━━━━●━━━━━━━━━━━━━━━━━━ [Built-in Subagents →](built-in-subagents.md)

</div>
