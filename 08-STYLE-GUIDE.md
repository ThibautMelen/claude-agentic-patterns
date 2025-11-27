<div align="center">

[🏠 Home](README.md) • [📖 Overview](00-OVERVIEW.md) • **08 Style Guide**

━━━━━━━━━━━━━━●━━━━━━━━━━━━━━━━ `8/8`

[← 07 Glossary](07-MAPPING-GLOSSARY.md) • [🏠 Back to Home](README.md)

</div>

---

# Style Guide: ACTEUR + ACTION System

> Standardized visual language for all Mermaid diagrams using **WHO does WHAT**

## 📑 Table of Contents

| # | Section | Description |
|---|---------|-------------|
| 1 | [Core Concept](#core-concept) | ACTEUR + ACTION explained |
| 2 | [Acteurs](#acteurs) | Who does the action |
| 3 | [Actions](#actions) | What is being done |
| 4 | [Tools](#tools) | What they use |
| 5 | [Combinations](#combinations) | ACTEUR + ACTION examples |
| 6 | [Other Elements](#other-elements) | Status, Triggers, Patterns |
| 7 | [Color Palette](#color-palette) | Hex codes |
| 8 | [Mermaid Classes](#mermaid-class-definitions) | Copy-paste blocks |
| 9 | [Rules](#rules) | Do's and Don'ts |

---

## Core Concept

Every element in a diagram answers: **WHO does WHAT?**

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         ACTEUR + ACTION SYSTEM                              │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  FORMAT: 🐔💭 = Main Agent (WHO) + Réflexion (WHAT)                         │
│                                                                             │
│  EXAMPLES:                                                                  │
│  ┌─────────┬─────────┬──────────────────────────────────────────────────┐  │
│  │ Combo   │ Meaning │ Description                                      │  │
│  ├─────────┼─────────┼──────────────────────────────────────────────────┤  │
│  │ 🙆‍♀️      │ User    │ User (neutral/idle state)                        │  │
│  │ 🙋‍♀️📥    │ User    │ User sends input                                 │  │
│  │ 💁‍♀️📤    │ User    │ User receives output                             │  │
│  │ 🐔💭    │ Main    │ Main Agent thinks/reasons                        │  │
│  │ 🐔🚦    │ Main    │ Main Agent routes/decides                        │  │
│  │ 🐔🪺    │ Main    │ Main Agent spawns Subagent (via Task tool)       │  │
│  │ 🐔🔀    │ Main    │ Main Agent splits task                           │  │
│  │ 🐔🌀    │ Main    │ Main Agent merges results                        │  │
│  │ 🐔🔧    │ Main    │ Main Agent uses Native tool                      │  │
│  │ 🐦⚡    │ Sub     │ Subagent executes task                           │  │
│  │ 🐦📤    │ Sub     │ Subagent returns result                          │  │
│  │ 🐦💤    │ Sub     │ Subagent idle/not chosen (Routing)               │  │
│  │ 🐔💤    │ Main    │ Main Agent idle/not chosen (Routing)             │  │
│  └─────────┴─────────┴──────────────────────────────────────────────────┘  │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Acteurs

**WHO does the action?**

| Acteur | Emoji | Color | Hex | Description |
|--------|-------|-------|-----|-------------|
| **User (neutral)** | 🙆‍♀️ | Indigo | `#6366f1` | The human (idle state) |
| **User (gives)** | 🙋‍♀️ | Indigo | `#6366f1` | The human sends input |
| **User (receives)** | 💁‍♀️ | Indigo | `#6366f1` | The human receives output |
| **Main Agent** | 🐔 | Purple | `#8b5cf6` | Claude Code orchestrator (the hen) |
| **Subagent** | 🐦 | Pink | `#ec4899` | Delegated worker (the bird) |

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  THE POULTRY FAMILY                                                         │
│                                                                             │
│  USER STATES:                                                               │
│  🙆‍♀️ User (neutral)  → Idle, waiting                                        │
│  🙋‍♀️ User (gives)    → Sends input to system                                │
│  💁‍♀️ User (receives) → Receives output from system                          │
│                                                                             │
│  AGENTS:                                                                    │
│  🐔 Main Agent  → The hen that orchestrates (can spawn 🐦)                  │
│  🐦 Subagent    → The bird that executes (cannot spawn other 🐦)            │
│                                                                             │
│  HIERARCHY: 🙋‍♀️📥 → 🐔 → 🐦 → 💁‍♀️📤                                           │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Actions

**WHAT is being done?**

| Action | Emoji | Description | Used with |
|--------|-------|-------------|-----------|
| **Input** | 📥 | Receives/Sends data | 🙋‍♀️📥 (user sends) |
| **Output** | 📤 | Produces/Returns result | 🐔📤, 🐦📤, 💁‍♀️📤 (user receives) |
| **Réflexion** | 💭 | Thinks/Reasons/Prompts | 🐔💭, 🐦💭 |
| **Routing** | 🚦 | Decides direction | 🐔🚦 |
| **Spawn** | 🪺 | Creates/Spawns subagent | 🐔🪺 |
| **Exécution** | ⚡ | Executes task | 🐔⚡, 🐦⚡ |
| **Observation** | 👀 | Reads/Observes | 🐔👀, 🐦👀 |
| **Écriture** | ✏️ | Writes/Modifies | 🐔✏️, 🐦✏️ |
| **Validation** | ✅ | Validates/Approves | 🙆‍♀️✅, 🐔✅ |
| **Question** | ❓ | Asks | 🙆‍♀️❓, 🐔❓ |
| **Split** | 🔀 | Divides/Splits task | 🐔🔀 |
| **Merge** | 🌀 | Combines results | 🐔🌀 |
| **Plan** | 📋 | Creates plan | 🐔📋 |
| **Adjust** | 🔄 | Adjusts/Loops | 🐔🔄 |
| **Continue** | ▶️ | Continues execution | 🐔▶️ |
| **Idle/Sleep** | 💤 | Not chosen/Inactive | 🐦💤, 🐔💤 |

---

## Tools

**WHAT do they use?** (3 types)

| Tool Type | Emoji | Color | Hex | Examples |
|-----------|-------|-------|-----|----------|
| **Native** | 🔧 | Slate | `#64748b` | Read, Write, Edit, Bash, Glob, Grep |
| **MCP** | 🔌 | Amber | `#f59e0b` | Context7, Perplexity, Firecrawl |
| **User Interaction** | 💁‍♀️ | Teal | `#14b8a6` | AskUserQuestion, TodoWrite |

### Native Tool Sub-categories (optional precision)

| Sub-category | Combo | Tools |
|--------------|-------|-------|
| Read Operations | 🔧👀 | Read, Glob, Grep |
| Write Operations | 🔧✏️ | Write, Edit, NotebookEdit |
| System Operations | 🔧💻 | Bash, BashOutput, KillShell |
| Web Operations | 🔧🌐 | WebFetch, WebSearch |

---

## Combinations

### ACTEUR + ACTION

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  USER (3 states: 🙆‍♀️ 🙋‍♀️ 💁‍♀️)                                                 │
│  ────────────────────────────────────────────────────────────────────────── │
│  🙆‍♀️      User (neutral/idle state)                                         │
│  🙋‍♀️📥    User sends input                                                   │
│  🙆‍♀️✅    User validates (approves)                                          │
│  🙆‍♀️❓    User questions                                                     │
│  💁‍♀️📤    User receives output                                               │
├─────────────────────────────────────────────────────────────────────────────┤
│  MAIN AGENT 🐔                                                              │
│  ────────────────────────────────────────────────────────────────────────── │
│  🐔💭   Main Agent thinks/reasons                                           │
│  🐔🚦   Main Agent routes/decides                                           │
│  🐔🪺   Main Agent spawns Subagent (Task tool)                              │
│  🐔🔀   Main Agent splits task                                              │
│  🐔🌀   Main Agent merges results                                           │
│  🐔📋   Main Agent plans (Pattern 6: Autonomous)                            │
│  🐔📤   Main Agent outputs result                                           │
│  🐔⚡   Main Agent executes                                                 │
│  🐔👀   Main Agent observes/reads                                           │
│  🐔✏️   Main Agent writes                                                   │
│  🐔✅   Main Agent validates                                                │
│  🐔🔄   Main Agent adjusts/loops                                            │
├─────────────────────────────────────────────────────────────────────────────┤
│  SUBAGENT 🐦                                                                │
│  ────────────────────────────────────────────────────────────────────────── │
│  🐦💭   Subagent thinks/reasons                                             │
│  🐦⚡   Subagent executes                                                   │
│  🐦👀   Subagent observes/reads                                             │
│  🐦✏️   Subagent writes                                                     │
│  🐦📤   Subagent returns result                                             │
│  🐦✅   Subagent validates                                                  │
│  🐦💤   Subagent idle/not chosen                                            │
├─────────────────────────────────────────────────────────────────────────────┤
│  IDLE (for Routing pattern)                                                 │
│  ────────────────────────────────────────────────────────────────────────── │
│  🐔💤   Main Agent idle/not chosen                                          │
│  🐦💤   Subagent idle/not chosen                                            │
└─────────────────────────────────────────────────────────────────────────────┘
```

### ACTEUR + TOOL

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  MAIN AGENT 🐔 + TOOLS                                                      │
│  ────────────────────────────────────────────────────────────────────────── │
│  🐔🔧      Main Agent uses Native tool                                      │
│  🐔🔧👀    Main Agent reads (Read, Glob, Grep)                              │
│  🐔🔧✏️    Main Agent writes (Write, Edit)                                  │
│  🐔🔧💻    Main Agent bash                                                  │
│  🐔🔧🌐    Main Agent web (WebFetch, WebSearch)                             │
│  🐔🔌      Main Agent uses MCP tool                                         │
│  🐔💁‍♀️     Main Agent user interaction                                      │
├─────────────────────────────────────────────────────────────────────────────┤
│  SUBAGENT 🐦 + TOOLS                                                        │
│  ────────────────────────────────────────────────────────────────────────── │
│  🐦🔧      Subagent uses Native tool                                        │
│  🐦🔧👀    Subagent reads                                                   │
│  🐦🔧✏️    Subagent writes                                                  │
│  🐦🔧💻    Subagent bash                                                    │
│  🐦🔌      Subagent uses MCP tool                                           │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Other Elements

### Triggers & Components

| Element | Emoji | Color | Hex | Description |
|---------|-------|-------|-----|-------------|
| **Hook** | 🪝 | Emerald | `#10b981` | Automatic trigger |
| **Slash Command** | 🦴 | Indigo | `#6366f1` | User entry point |
| **Skill** | 📚 | Purple | `#8b5cf6` | Loaded knowledge |
| **State/Data** | 💾 | Emerald | `#10b981` | Persisted data |
| **Task tool** | 📤 | Pink | `#ec4899` | Delegation (spawns 🐦) |

### Status

| Status | Emoji | Color | Hex |
|--------|-------|-------|-----|
| **Success** | ✅ | Emerald | `#10b981` |
| **Error** | ❌ | Red | `#ef4444` |
| **Warning** | ⚠️ | Amber | `#f59e0b` |
| **In Progress** | 🔄 | Blue | `#3b82f6` |
| **Pending** | ⏳ | Slate | `#64748b` |
| **Skip** | ⏭️ | Slate | `#64748b` |

### Patterns (for titles only)

**Anthropic Research Patterns:**

| Pattern | Emoji |
|---------|-------|
| Prompt Chaining | ⛓️ |
| Routing | 🚦 |
| Parallelization | 🛤️ |
| Orchestrator-Workers | 🎭 |
| Evaluator-Optimizer | 🩻 |
| Autonomous Agents | 🐉 |

**Claude Code Implementation Patterns:**

| Pattern | Emoji | Color | Hex |
|---------|-------|-------|-----|
| Direct Execution | 🏎️ | Slate | `#64748b` |
| Subagent Orchestration | 🎪 | Pink | `#ec4899` |
| Parallel Tool Calling | 🚂 | Blue | `#3b82f6` |
| Master-Clone | 🧬 | Amber | `#f59e0b` |
| Wizard Workflow | 🧙 | Teal | `#14b8a6` |
| Multi-Window Context | 🖥️ | Blue | `#3b82f6` |
| Progressive Skills | 🎓 | Emerald | `#10b981` |
| Programmatic Orchestration | 🎛️ | Indigo | `#6366f1` |

### Phases (generation order)

| Phase | Emoji | Description |
|-------|-------|-------------|
| **Phase 1** | 🏗️ | Foundation |
| **Phase 2** | 🔗 | Formatting |
| **Phase 3** | 📝 | Content |
| **Phase 4** | 🔮 | Synthesis |

---

## Quick Reference Card

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                      EMOJI QUICK REFERENCE v2                               │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  ACTEURS              ACTIONS              TOOLS                            │
│  ────────             ───────              ─────                            │
│  🙆‍♀️ User (neutral)   📥 Input             🔧 Native                        │
│  🙋‍♀️ User (gives)     📤 Output            🔌 MCP                           │
│  💁‍♀️ User (receives)  💭 Réflexion         💁‍♀️ User Interaction              │
│  🐔 Main Agent        🚦 Routing                                            │
│  🐦 Subagent          🪺 Spawn             NATIVE DETAIL                    │
│                       ⚡ Exécution         ─────────────                    │
│                       👀 Observation       🔧👀 Read ops                     │
│                       ✏️ Écriture          🔧✏️ Write ops                    │
│                       ✅ Validation        🔧💻 Bash ops                     │
│                       ❓ Question          🔧🌐 Web ops                      │
│                       🔀 Split             📋 Plan                          │
│                       🌀 Merge             🔄 Adjust                         │
│                       💤 Idle/Sleep                                         │
├─────────────────────────────────────────────────────────────────────────────┤
│  TRIGGERS             STATUS               COMPOSANTS                       │
│  ────────             ──────               ──────────                       │
│  🪝 Hook              ✅ Success           🦴 Slash Command                 │
│                       ❌ Error             📚 Skill                         │
│                       ⚠️ Warning           💾 State                         │
│                       🔄 Progress          📤 Task tool                     │
│                       ⏳ Pending                                            │
│                       ⏭️ Skip                                               │
├─────────────────────────────────────────────────────────────────────────────┤
│  PATTERNS ANTHROPIC                PATTERNS CLAUDE CODE                     │
│  ─────────────────                 ────────────────────                     │
│  ⛓️ Prompt Chaining                🏎️ Direct Execution                      │
│  🚦 Routing                        🎪 Subagent Orchestration                │
│  🛤️ Parallelization                🚂 Parallel Tool Calling                 │
│  🎭 Orchestrator-Workers           🧬 Master-Clone                          │
│  🩻 Evaluator-Optimizer           🧙 Wizard Workflow                       │
│  🐉 Autonomous Agents              🖥️ Multi-Window Context                  │
│                                    🎓 Progressive Skills                    │
│                                    🎛️ Programmatic Orchestration            │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Color Palette

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         STANDARD COLOR PALETTE                              │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  🟣 #6366f1 (Indigo)    → User 🙆‍♀️🙋‍♀️💁‍♀️, Slash Commands 🦴                   │
│  🟣 #8b5cf6 (Purple)    → Main Agent 🐔, Skills 📚                          │
│  🩷 #ec4899 (Pink)      → Subagent 🐦, Task tool 📤                         │
│  🟠 #f59e0b (Amber)     → MCP Tools 🔌, Master-Clone 🧬                     │
│  🟢 #10b981 (Emerald)   → State 💾, Success ✅, Hook 🪝                     │
│  🔵 #3b82f6 (Blue)      → Parallel 🚂, Multi-Window 🖥️, Progress 🔄        │
│  🔴 #ef4444 (Red)       → Errors ❌                                        │
│  🩶 #64748b (Slate)     → Native Tools 🔧, Neutral, Skip ⏭️                 │
│  🩶 #94a3b8 (Slate-400) → Idle/Not chosen 💤                                │
│  🩵 #14b8a6 (Teal)      → User Interaction 💁‍♀️, Wizard 🧙                   │
│  🩵 #06b6d4 (Cyan)      → Data flow                                        │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Mermaid Class Definitions

### Standard classDef Block

Copy this block at the start of every Mermaid diagram:

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart TB
    %% Acteurs
    classDef user fill:#6366f1,stroke:#4f46e5,stroke-width:2px,color:#ffffff
    classDef main fill:#8b5cf6,stroke:#7c3aed,stroke-width:2px,color:#ffffff
    classDef subagent fill:#ec4899,stroke:#db2777,stroke-width:2px,color:#ffffff

    %% Tools
    classDef nativeTool fill:#64748b,stroke:#475569,stroke-width:2px,color:#ffffff
    classDef mcpTool fill:#f59e0b,stroke:#d97706,stroke-width:2px,color:#ffffff
    classDef userInteraction fill:#14b8a6,stroke:#0d9488,stroke-width:2px,color:#ffffff

    %% Other
    classDef state fill:#10b981,stroke:#059669,stroke-width:2px,color:#ffffff
    classDef wizard fill:#14b8a6,stroke:#0d9488,stroke-width:2px,color:#ffffff
    classDef parallel fill:#3b82f6,stroke:#2563eb,stroke-width:2px,color:#ffffff
    classDef error fill:#ef4444,stroke:#dc2626,stroke-width:2px,color:#ffffff
    classDef neutral fill:#64748b,stroke:#475569,stroke-width:2px,color:#ffffff
    classDef data fill:#06b6d4,stroke:#0891b2,stroke-width:2px,color:#ffffff
    classDef idle fill:#94a3b8,stroke:#64748b,stroke-width:2px,color:#ffffff
```

### Subgraph Styles

```mermaid
    %% Layer Subgraph Styles
    style L1 fill:#e0e7ff,stroke:#6366f1,stroke-width:2px
    style L2 fill:#f3e8ff,stroke:#8b5cf6,stroke-width:2px
    style L3 fill:#fce7f3,stroke:#ec4899,stroke-width:2px
    style L4 fill:#fef3c7,stroke:#f59e0b,stroke-width:2px
    style L5 fill:#ecfdf5,stroke:#10b981,stroke-width:2px
```

---

## Example: Complete Diagram

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart TB
    classDef user fill:#6366f1,stroke:#4f46e5,stroke-width:2px,color:#ffffff
    classDef main fill:#8b5cf6,stroke:#7c3aed,stroke-width:2px,color:#ffffff
    classDef subagent fill:#ec4899,stroke:#db2777,stroke-width:2px,color:#ffffff
    classDef mcpTool fill:#f59e0b,stroke:#d97706,stroke-width:2px,color:#ffffff
    classDef state fill:#10b981,stroke:#059669,stroke-width:2px,color:#ffffff
    classDef wizard fill:#14b8a6,stroke:#0d9488,stroke-width:2px,color:#ffffff

    subgraph L1["🙋‍♀️ LAYER 1: USER"]
        CMD["🦴 /generate fr-FR"]:::user
    end

    subgraph L2["🐔 LAYER 2: MAIN AGENT"]
        MA["🐔💭 Main Agent"]:::main
        WIZ["🧙 Wizard Workflow"]:::wizard
        MA --> WIZ
    end

    subgraph L3["🔀 LAYER 3: DELEGATION"]
        SA1["🐦⚡ core-identity"]:::subagent
        SA2["🐦⚡ core-formatting"]:::subagent
    end

    subgraph L4["⚡ LAYER 4: EXECUTION"]
        T1["🔌 Context7"]:::mcpTool
        T2["🔌 Perplexity"]:::mcpTool
    end

    subgraph L5["💾 LAYER 5: STATE"]
        S1["✅ Files written"]:::state
    end

    CMD --> MA
    WIZ -->|"🙆‍♀️✅ User approves"| SA1 & SA2
    SA1 & SA2 --> T1 & T2
    T1 & T2 --> S1

    style L1 fill:#e0e7ff,stroke:#6366f1,stroke-width:2px
    style L2 fill:#f3e8ff,stroke:#8b5cf6,stroke-width:2px
    style L3 fill:#fce7f3,stroke:#ec4899,stroke-width:2px
    style L4 fill:#fef3c7,stroke:#f59e0b,stroke-width:2px
    style L5 fill:#ecfdf5,stroke:#10b981,stroke-width:2px
```

---

## Example: Prompt Chaining Flow

```
🙋‍♀️📥 ──► 🐔💭 ──► 🐔📤 ──► 🐔💭 ──► 🐔📤 ──► 🐔💭 ──► 🐔📤 ──► 💁‍♀️📤
Input     Step 1    (internal)  Step 2    (internal)  Step 3     Output    User
```

## Example: Orchestrator-Workers Flow

```
🙋‍♀️📥 ──► 🐔🔀 ──┬──► 🐦⚡ ──► 🐦📤 ──┐
                ├──► 🐦⚡ ──► 🐦📤 ──┼──► 🐔🌀 ──► 🐔📤 ──► 💁‍♀️📤
                └──► 🐦⚡ ──► 🐦📤 ──┘
```

## Example: Autonomous Agent Flow (Pattern 6: 🐉)

```
🙋‍♀️📥 ──► 🐔📋 ──► 🐔⚡ ──► 🐔👀 ──► 🐔💭 ──┬──► 🐔🔄 ──► 🐔📋 (loop)
Goal       Plan      Act      Observe   Reflect │
                                                └──► 🐔📤 ──► 💁‍♀️📤 (done)
```

---

## Rules

### Do's

1. **Always use ACTEUR + ACTION** - Every node should show WHO does WHAT
2. **Use classDef** - Never inline styles
3. **Consistent colors** - Same color = same acteur/tool everywhere
4. **White text on dark fills** - `color:#ffffff` for readability
5. **2px stroke-width** - Standard border thickness
6. **Subgraph backgrounds** - Use lighter versions of layer colors

### Don'ts

1. **Don't mix emoji meanings** - 🐔 is always Main Agent, never Subagent
2. **Don't use random colors** - Stick to the palette
3. **Don't skip emojis** - They aid quick scanning
4. **Don't use dark backgrounds with dark text**
5. **Don't create new emojis without documenting**
6. **Don't use 🧠 for Main Agent** - Use 🐔 (deprecated)
7. **Don't use 🤖 for Subagent** - Use 🐦 (deprecated)
8. **Don't use 👤 for User** - Use 🙋‍♀️ (deprecated)

---

## Migration Guide (Old → New)

| Old | New | Element |
|-----|-----|---------|
| 👤 | 🙆‍♀️/🙋‍♀️/💁‍♀️ | User (3 states) |
| 🧠 | 🐔 | Main Agent |
| 🤖 | 🐦 | Subagent |
| 🛠️ | 🔧 | Native Tool |
| 🖐️ | 💁‍♀️ | User Interaction Tool |

> **Note:** 🐉 is only used for Pattern 6 title "🐉 Autonomous Agents", not as an acteur in diagrams.

---

## CSS Variables (for web implementations)

```css
:root {
  /* Acteur Colors */
  --color-user: #6366f1;
  --color-main-agent: #8b5cf6;
  --color-subagent: #ec4899;

  /* Tool Colors */
  --color-native-tool: #64748b;
  --color-mcp-tool: #f59e0b;
  --color-user-interaction: #14b8a6;

  /* Other */
  --color-state: #10b981;
  --color-wizard: #14b8a6;
  --color-parallel: #3b82f6;
  --color-data: #06b6d4;

  /* Status Colors */
  --color-success: #10b981;
  --color-error: #ef4444;
  --color-warning: #f59e0b;
  --color-neutral: #64748b;
  --color-idle: #94a3b8;

  /* Border Colors (darker variants) */
  --border-user: #4f46e5;
  --border-main-agent: #7c3aed;
  --border-subagent: #db2777;
  --border-state: #059669;
  --border-native-tool: #475569;
  --border-mcp-tool: #d97706;
  --border-user-interaction: #0d9488;

  /* Background Colors (lighter variants for subgraphs) */
  --bg-user: #e0e7ff;
  --bg-main-agent: #f3e8ff;
  --bg-subagent: #fce7f3;
  --bg-tool: #fef3c7;
  --bg-state: #ecfdf5;
}
```

---

<div align="center">

**━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━**

[← 07 Glossary](07-MAPPING-GLOSSARY.md) • [🏠 Home](README.md) • [📖 Overview](00-OVERVIEW.md)

</div>
