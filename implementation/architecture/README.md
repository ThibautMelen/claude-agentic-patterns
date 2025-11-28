<div align="center">

[🏠 Home](../../README.md) • [🔧 Implementation](../README.md) • **🏛️ Architecture**

</div>

---

# Layer Architecture

> Understanding the 5-layer system architecture of Claude Code agentic systems

---

## Overview

Claude Code operates through a layered architecture where each layer has specific responsibilities and communication patterns.

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         5-LAYER ARCHITECTURE                                │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │  🙋‍♀️ LAYER 1: USER LAYER                                            │   │
│  │  Human input, 🦴 /commands, natural language prompts                │   │
│  └────────────────────────────────┬────────────────────────────────────┘   │
│                                   │                                         │
│                                   ▼                                         │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │  🐔 LAYER 2: MAIN AGENT LAYER                                       │   │
│  │  Claude Code - orchestration, decision-making, routing              │   │
│  └────────────────────────────────┬────────────────────────────────────┘   │
│                                   │                                         │
│                    ┌──────────────┼──────────────┐                         │
│                    ▼              ▼              ▼                          │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │  🔀 LAYER 3: DELEGATION LAYER                                       │   │
│  │  🦴 Slash Commands, 📚 Skills - workflow definition                 │   │
│  └────────────────────────────────┬────────────────────────────────────┘   │
│                                   │                                         │
│                                   ▼                                         │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │  ⚡ LAYER 4: EXECUTION LAYER                                        │   │
│  │  🐦 Subagents, 🔧 Built-in, 🔌 External (MCP), 💁‍♀️ Interaction        │   │
│  └────────────────────────────────┬────────────────────────────────────┘   │
│                                   │                                         │
│                                   ▼                                         │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │  💾 LAYER 5: STATE LAYER                                            │   │
│  │  Memory, Files, Context - persistence and state management          │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Layer Index

| # | Layer | Emoji | File | Role |
|---|-------|-------|------|------|
| 1 | User Layer | 🙋‍♀️ | [01-user-layer.md](01-user-layer.md) | Entry point |
| 2 | Main Agent Layer | 🐔 | [02-main-agent-layer.md](02-main-agent-layer.md) | Orchestration |
| 3 | Delegation Layer | 🔀 | [03-delegation-layer.md](03-delegation-layer.md) | Workflow definition |
| 4 | Execution Layer | ⚡ | [04-execution-layer.md](04-execution-layer.md) | Actual work |
| 5 | State Layer | 💾 | [05-state-layer.md](05-state-layer.md) | Persistence |

---

## Layer Responsibilities Matrix

| Layer | Emoji | Input | Process | Output |
|-------|-------|-------|---------|--------|
| **User** | 🙋‍♀️ | Human action | Normalize | Prompt/Command |
| **Main Agent** | 🐔 | Prompt | Orchestrate | Delegation calls |
| **Delegation** | 🔀 | Command/Context | Define workflow | Structured task |
| **Execution** | ⚡ | Task | Execute (🔧🔌💁‍♀️) | Results |
| **State** | 💾 | Data | Persist | Stored state |

---

## Complete Layer Interaction

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
sequenceDiagram
    participant U as 🙋‍♀️ User Layer
    participant MA as 🐔 Main Agent Layer
    participant DL as 🔀 Delegation Layer
    participant EL as ⚡ Execution Layer
    participant SL as 💾 State Layer

    U->>MA: 🙋‍♀️📥 🦴 /generate fr-FR

    MA->>DL: Load 🦴 command
    DL-->>MA: Expanded prompt

    MA->>SL: Load 📋 CLAUDE.md context
    SL-->>MA: Project instructions

    MA->>EL: 🐔🪺 Task(🐦 subagent)
    EL->>SL: Read source files
    SL-->>EL: File contents
    EL->>SL: Write output files
    EL-->>MA: ✅ Completion report

    MA->>SL: Save 🖥️ checkpoint
    MA-->>U: "✅ Generated 9 files for fr-FR"
```

---

## Anti-Patterns

### ❌ Wrong: 🐦 Subagent Spawning 🐦 Subagent

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart LR
    classDef error fill:#ef4444,stroke:#dc2626,stroke-width:2px,color:#ffffff
    classDef main fill:#8b5cf6,stroke:#7c3aed,stroke-width:2px,color:#ffffff

    MA["🐔 Main Agent"]:::main --> SA1["🐦 Subagent 1"]:::error
    SA1 -->|"❌ WRONG"| SA2["🐦 Subagent 2"]:::error
```

### ✅ Correct: 🐔 Main Agent Orchestrates All

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart TB
    classDef main fill:#8b5cf6,stroke:#7c3aed,stroke-width:2px,color:#ffffff
    classDef subagent fill:#ec4899,stroke:#db2777,stroke-width:2px,color:#ffffff

    MA["🐔 Main Agent"]:::main

    MA -->|🪺 Task| SA1["🐦 Subagent 1"]:::subagent
    MA -->|🪺 Task| SA2["🐦 Subagent 2"]:::subagent

    SA1 -->|Result| MA
    SA2 -->|Result| MA
```

---

## Critical Rule

> **The 🐔 Main Agent is the ONLY entity that can spawn 🐦 Subagents.**
>
> 🐦 Subagents cannot spawn other subagents. All delegation flows through the 🐔 Main Agent.

---

<div align="center">

**━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━**

[🔧 Implementation](../README.md) • [📦 Components](../components/)

</div>
