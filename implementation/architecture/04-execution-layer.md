<div align="center">

[🏠 Home](../../README.md) • [🔧 Implementation](../README.md) • [🏛️ Architecture](./) • **⚡ Layer 4: Execution**

</div>

---

# ⚡ Layer 4: Execution Layer

> Where actual work happens - code execution, file operations, API calls.

---

## Purpose

The Execution Layer performs the actual work. It contains all the tools and subagents that carry out tasks delegated by the 🐔 Main Agent.

---

## Components

| Component | Emoji | Function | Spawned By |
|-----------|-------|----------|------------|
| **Subagents** | 🐦 | Autonomous task execution | Task tool (🪺 spawn) |
| **Built-in Tools** | 🔧 | Core operations (Read, Write, Bash...) | 🐔 Main Agent / 🐦 Subagents |
| **MCP Tools** | 🔌 | External services (Context7, Perplexity...) | 🐔 Main Agent / 🐦 Subagents |
| **User Interaction** | 💁‍♀️ | Human-in-the-loop (❓ AskUser, 📋 Todo) | 🐔 Main Agent / 🐦 Subagents |

---

## 🐦 Subagent Lifecycle

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
stateDiagram-v2
    [*] --> Spawned: 🪺 Task tool called
    Spawned --> Executing: Receives prompt
    Executing --> Working: Uses 🔧 🔌 💁‍♀️ tools
    Working --> Working: Iterates
    Working --> Completed: ✅ Task done
    Completed --> [*]: Returns result

    note right of Working
        🐦 Cannot spawn
        other subagents
    end note
```

---

## Tool Categories

```mermaid
mindmap
    root(("⚡ Execution"))
        🔧 Built-in Tools
            🔧👀 Read file
                Read
            🔧🔍 Search content
                Grep
            🔧🗂️ Search files
                Glob
            🔧✏️ Write ops
                Write
                Edit
            🔧📟 Shell ops
                Bash
            🔧🌐 Web ops
                WebFetch
                WebSearch
        🔌 External MCP
            Context7
            Perplexity
            Firecrawl
            Custom MCPs
        💁‍♀️ User Interaction
            ❓ AskUserQuestion
            📋 TodoWrite
        🪺 Task spawn
            Spawns 🐦 Subagents
```

---

## 🔧 Built-in Tools Reference

| Tool | Emoji | Operation |
|------|-------|-----------|
| `Read` | 🔧👀 | Read file contents |
| `Write` | 🔧✏️ | Create/overwrite files |
| `Edit` | 🔧✏️ | Modify existing files |
| `Glob` | 🔧🗂️ | Search files by pattern |
| `Grep` | 🔧🔍 | Search content in files |
| `Bash` | 🔧📟 | Execute shell commands |
| `WebFetch` | 🔧🌐 | Fetch URL content |
| `WebSearch` | 🔧🌐 | Search the web |

---

## 🔌 MCP Tools (External)

| Tool | Purpose |
|------|---------|
| **Context7** | Up-to-date library documentation |
| **Perplexity** | AI-powered web search |
| **Firecrawl** | Web scraping and crawling |
| **Custom MCPs** | Project-specific integrations |

---

## 💁‍♀️ User Interaction Tools

| Tool | Emoji | Purpose |
|------|-------|---------|
| `AskUserQuestion` | ❓ | Request clarification |
| `TodoWrite` | 📋 | Track task progress |

---

## 🚂 Parallel Execution

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart TB
    classDef main fill:#8b5cf6,stroke:#7c3aed,stroke-width:2px,color:#ffffff
    classDef subagent fill:#ec4899,stroke:#db2777,stroke-width:2px,color:#ffffff
    classDef state fill:#10b981,stroke:#059669,stroke-width:2px,color:#ffffff

    MA["🐔 Main Agent"]:::main

    MA -->|🪺 Task| SA1["🐦 Subagent 1"]:::subagent
    MA -->|🪺 Task| SA2["🐦 Subagent 2"]:::subagent
    MA -->|🪺 Task| SA3["🐦 Subagent 3"]:::subagent

    SA1 --> R1[Result 1]
    SA2 --> R2[Result 2]
    SA3 --> R3[Result 3]

    R1 --> MERGE["✅ Merge Results"]:::state
    R2 --> MERGE
    R3 --> MERGE

    MERGE --> MA
```

### Parallel Execution Rules

1. **Independence**: Tasks must not depend on each other
2. **No Cross-Communication**: 🐦 Subagents cannot communicate directly
3. **Single Orchestrator**: Only 🐔 Main Agent coordinates
4. **Result Aggregation**: All results flow back to 🐔 Main Agent

---

## Critical Rule

> **🐦 Subagents CANNOT spawn other 🐦 Subagents.**
>
> All delegation must flow through the 🐔 Main Agent.

### ❌ Wrong Pattern

```
🐔 Main Agent → 🐦 Subagent 1 → 🐦 Subagent 2  ❌ INVALID
```

### ✅ Correct Pattern

```
🐔 Main Agent → 🐦 Subagent 1
              → 🐦 Subagent 2
              → 🐦 Subagent 3
```

---

## Layer Position

```
┌─────────────────────────────────────────────────────┐
│  🔀 LAYER 3: DELEGATION LAYER                       │
│  🦴 Slash Commands, 📚 Skills - workflow definition │
└─────────────────────────┬───────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────┐
│  ⚡ LAYER 4: EXECUTION LAYER  ◄─── YOU ARE HERE    │
│  🐦 Subagents, 🔧 Built-in, 🔌 External, 💁‍♀️ User   │
└─────────────────────────┬───────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────┐
│  💾 LAYER 5: STATE LAYER                            │
│  Memory, Files, Context - persistence               │
└─────────────────────────────────────────────────────┘
```

---

<div align="center">

**━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━**

[← 🔀 Delegation Layer](03-delegation-layer.md) • [🏛️ Architecture](./) • [💾 State Layer →](05-state-layer.md)

</div>
