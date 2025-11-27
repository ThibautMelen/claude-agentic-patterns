<div align="center">

[🏠 Home](README.md) • [📖 Overview](00-OVERVIEW.md) • **03 Research Patterns**

━━━━━━━━━●━━━━━━━━━━━━━━━━━━━━━ `3/8`

[← 02 Architecture](02-LAYER-ARCHITECTURE.md) • [04 Implementation →](04-CLAUDE-CODE-PATTERNS.md)

</div>

---

# Anthropic Research Patterns

> 6 foundational patterns from Anthropic's "Building Effective Agents" paper

## 📑 Table of Contents

| # | Pattern | Description |
|---|---------|-------------|
| 1 | [⛓️ Prompt Chaining](#pattern-1-️-prompt-chaining) | Sequential steps |
| 2 | [🚦 Routing](#pattern-2--routing) | Classification & dispatch |
| 3 | [🛤️ Parallelization](#pattern-3-️-parallelization) | Concurrent execution |
| 4 | [🎭 Orchestrator-Workers](#pattern-4--orchestrator-workers) | Manager + specialists |
| 5 | [🩻 Evaluator-Optimizer](#pattern-5-️-evaluator-optimizer) | Iterative refinement |
| 6 | [🐉 Autonomous Agents](#pattern-6--autonomous-agents) | Self-directed execution |
| ⚔️ | [Pattern Comparisons](#pattern-comparisons) | Side-by-side VS diagrams |

---

## Source

These patterns come from **Anthropic's research paper "Building Effective Agents"** (December 2024), which establishes the theoretical foundation for agentic AI systems.

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    6 ANTHROPIC RESEARCH PATTERNS                            │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   1. ⛓️ Prompt Chaining       4. 🎭 Orchestrator-Workers                    │
│   2. 🚦 Routing               5. 🩻 Evaluator-Optimizer                     │
│   3. 🛤️ Parallelization       6. 🐉 Autonomous Agents                       │
│                                                                             │
│   Source: "Building Effective Agents" - Anthropic Research, Dec 2024        │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Pattern 1: ⛓️ Prompt Chaining

### Definition

Breaking a task into sequential steps where each step's output becomes the next step's input.

### Diagram

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart LR
    classDef user fill:#6366f1,stroke:#4f46e5,stroke-width:2px,color:#ffffff
    classDef main fill:#8b5cf6,stroke:#7c3aed,stroke-width:2px,color:#ffffff

    USER["🙋‍♀️📥 User Request"]:::user --> P1["🐔💭 Step 1"]:::main
    P1 -->|"🐔📤"| P2["🐔💭 Step 2"]:::main
    P2 -->|"🐔📤"| P3["🐔💭 Step 3"]:::main
    P3 -->|"🐔📤"| OUT["💁‍♀️📤 User Receives"]:::user
```

### Use Cases

| Use Case | Example |
|----------|---------|
| Document processing | Extract → Analyze → Summarize |
| Code generation | Plan → Implement → Review |
| Data transformation | Parse → Transform → Validate |

### Example Flow

```
Step 1: "Extract all function names from this code"
        → [list of functions]

Step 2: "For each function, identify parameters and return types"
        → [function signatures]

Step 3: "Generate documentation for each function"
        → [documented code]
```

### When to Use

- Tasks have clear sequential dependencies
- Each step's quality affects the next
- Need checkpoints between steps

### When NOT to Use

- Steps can be done independently (use Parallelization)
- Simple single-step tasks

---

## Pattern 2: 🚦 Routing

### Definition

Directing inputs to specialized handlers based on classification or intent.

### Diagram

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart TB
    classDef user fill:#6366f1,stroke:#4f46e5,stroke-width:2px,color:#ffffff
    classDef main fill:#8b5cf6,stroke:#7c3aed,stroke-width:2px,color:#ffffff
    classDef subagent fill:#ec4899,stroke:#db2777,stroke-width:2px,color:#ffffff
    classDef idle fill:#94a3b8,stroke:#64748b,stroke-width:2px,color:#ffffff

    INPUT["🙋‍♀️📥 User Request"]:::user --> ROUTER{"🐔🚦 Route"}:::main

    ROUTER -.->|"Type A"| HA["🐦💤 Handler A"]:::idle
    ROUTER -->|"🐔🪺 Type B"| HB["🐦⚡ Handler B"]:::subagent
    ROUTER -.->|"Type C"| HC["🐦💤 Handler C"]:::idle
    ROUTER -.->|"Unknown"| DEFAULT["🐔💤 Default"]:::idle

    HB -->|"🐦📤"| FINAL["💁‍♀️📤 User Receives"]:::user
```

### Use Cases

| Use Case | Example |
|----------|---------|
| Customer support | Bug → Tech Team, Billing → Finance |
| Code tasks | Bug fix → Debugger, New feature → Builder |
| Content | Question → Q&A, Task → Executor |

### Example Implementation

```python
# Router determines handler
def route(input):
    classification = classify(input)

    if classification == "security":
        return security_handler(input)
    elif classification == "performance":
        return performance_handler(input)
    elif classification == "feature":
        return feature_handler(input)
    else:
        return general_handler(input)
```

### When to Use

- Inputs have distinct types requiring different handling
- Specialized expertise improves quality
- Clear classification criteria exist

### When NOT to Use

- All inputs require same processing
- Classification is unreliable

---

## Pattern 3: 🛤️ Parallelization

### Definition

Executing independent tasks simultaneously and merging results.

### Core Concept

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart LR
    classDef user fill:#6366f1,stroke:#4f46e5,stroke-width:2px,color:#ffffff
    classDef main fill:#8b5cf6,stroke:#7c3aed,stroke-width:2px,color:#ffffff
    classDef parallel fill:#3b82f6,stroke:#2563eb,stroke-width:2px,color:#ffffff

    IN["🙋‍♀️📥"]:::user --> SPLIT["🐔🔀 Split"]:::main
    SPLIT -->|"🐔🪺"| A["🐦⚡"]:::parallel
    SPLIT -->|"🐔🪺"| B["🐦⚡"]:::parallel
    SPLIT -->|"🐔🪺"| C["🐦⚡"]:::parallel
    A -->|"🐦📤"| MERGE["🐔🌀 Merge"]:::main
    B -->|"🐦📤"| MERGE
    C -->|"🐦📤"| MERGE
    MERGE -->|"🐔📤"| OUT["💁‍♀️📤"]:::user
```

> **Key insight**: Run multiple tasks **simultaneously**, combine results at the end.

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  ⚠️  IMPORTANT: Parallelization vs Orchestrator-Workers                     │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  In Parallelization, all spawned subagents are IDENTICAL.                   │
│  Same prompt, same capabilities. They are INTERCHANGEABLE.                  │
│                                                                             │
│  🛤️ Parallelization:      🐦⚡ = 🐦⚡ = 🐦⚡   (clones)                       │
│  🎭 Orchestrator-Workers:  🐦🔒 ≠ 🐦⚡ ≠ 🐦🎨   (specialists)                 │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### 2 Types of Parallelization

#### Type 1: 🛤️ Sectioning (Split DATA)

Split large data into chunks, process each chunk the same way, combine all results.

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart LR
    classDef user fill:#6366f1,stroke:#4f46e5,stroke-width:2px,color:#ffffff
    classDef main fill:#8b5cf6,stroke:#7c3aed,stroke-width:2px,color:#ffffff
    classDef parallel fill:#3b82f6,stroke:#2563eb,stroke-width:2px,color:#ffffff

    S_IN["🙋‍♀️📥 100 files"]:::user --> S_SPLIT["🐔🔀"]:::main
    S_SPLIT -->|"🐔🪺"| S1["🐦⚡ Files 1-50"]:::parallel
    S_SPLIT -->|"🐔🪺"| S2["🐦⚡ Files 51-100"]:::parallel
    S1 -->|"🐦📤"| S_MERGE["🐔🌀 Combine ALL"]:::main
    S2 -->|"🐦📤"| S_MERGE
    S_MERGE -->|"🐔📤"| S_OUT["💁‍♀️📤"]:::user
```

#### Type 2: 🗳️ Voting (Same TASK, pick BEST)

Run the same task multiple times, compare results, pick the best one.

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart LR
    classDef user fill:#6366f1,stroke:#4f46e5,stroke-width:2px,color:#ffffff
    classDef main fill:#8b5cf6,stroke:#7c3aed,stroke-width:2px,color:#ffffff
    classDef parallel fill:#3b82f6,stroke:#2563eb,stroke-width:2px,color:#ffffff
    classDef wizard fill:#14b8a6,stroke:#0d9488,stroke-width:2px,color:#ffffff
    classDef success fill:#10b981,stroke:#059669,stroke-width:2px,color:#ffffff

    V_IN["🙋‍♀️📥 Write headline"]:::user --> V_COPY["🐔🧬 3 attempts"]:::main
    V_COPY -->|"🐔🪺"| V1["🐦⚡ Version A"]:::parallel
    V_COPY -->|"🐔🪺"| V2["🐦⚡ Version B"]:::parallel
    V_COPY -->|"🐔🪺"| V3["🐦⚡ Version C"]:::parallel
    V1 -->|"🐦📤"| VOTE{"🐔🗳️ Compare"}:::wizard
    V2 -->|"🐦📤"| VOTE
    V3 -->|"🐦📤"| VOTE
    VOTE -->|"🐔✅ B wins"| BEST["🏆 Best"]:::success
```

### Summary

| Type | Workers | Input | Output |
|------|---------|-------|--------|
| **🛤️ Sectioning** | IDENTICAL | Different DATA chunks | Combine ALL |
| **🗳️ Voting** | IDENTICAL | Same DATA | Pick ONE best |

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  💡 KEY: Workers are IDENTICAL, only the ARGUMENT changes                   │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  Sectioning:  Same worker + Different data    → "Analyze chunk 1", "...2"  │
│  Voting:      Same worker + Same data         → "Write headline" x3        │
│                                                                             │
│  If you need DIFFERENT workers → use 🎭 Orchestrator-Workers instead        │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### When to Use

- Tasks have no dependencies on each other
- Speed is important
- Resources allow concurrent execution

### When NOT to Use

- Tasks depend on each other's output
- Sequential order matters
- Resource constraints

---

## Pattern 4: 🎭 Orchestrator-Workers

### Definition

A central orchestrator delegates tasks to specialized workers and synthesizes results.

### Diagram

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart TB
    classDef user fill:#6366f1,stroke:#4f46e5,stroke-width:2px,color:#ffffff
    classDef main fill:#8b5cf6,stroke:#7c3aed,stroke-width:2px,color:#ffffff
    classDef subagent fill:#ec4899,stroke:#db2777,stroke-width:2px,color:#ffffff

    INPUT["🙋‍♀️📥 Review this PR"]:::user --> ORCH["🐔🎭 Orchestrator"]:::main

    ORCH -->|"🐔🪺 Check vulns"| W1["🐦🔒 Security Expert"]:::subagent
    ORCH -->|"🐔🪺 Check perf"| W2["🐦⚡ Performance Expert"]:::subagent
    ORCH -->|"🐔🪺 Check style"| W3["🐦🎨 Style Expert"]:::subagent

    W1 -->|"🐦📤 2 SQLi found"| SYNTH["🐔🌀 Synthesize"]:::main
    W2 -->|"🐦📤 O(n²) loop"| SYNTH
    W3 -->|"🐦📤 3 violations"| SYNTH

    SYNTH -->|"🐔📤"| OUTPUT["💁‍♀️📤 Final Report"]:::user
```

> **Key insight**: Each worker has a **DIFFERENT expertise** and does a **DIFFERENT task**.

### Orchestrator Responsibilities

| Responsibility | Description |
|----------------|-------------|
| **Decomposition** | Break complex task into subtasks |
| **Assignment** | Route subtasks to appropriate workers |
| **Monitoring** | Track worker progress |
| **Synthesis** | Combine results into coherent output |

### Worker Characteristics

```mermaid
%%{init: {'theme': 'base'}}%%
mindmap
    root(("🐦⚡ Workers"))
        🎯 Specialized
            Domain expert
            Single responsibility
        ⚡ Autonomous
            Independent execution
            Own tool access
        🔒 Isolated
            No direct communication
            Report to orchestrator
```

### Example: Code Review System

```
Orchestrator: "Review this PR for security, performance, and style"

    → Security Worker: "Check for SQL injection, XSS, auth issues"
      ← "Found 2 potential SQL injection points"

    → Performance Worker: "Analyze time complexity, memory usage"
      ← "O(n²) loop could be O(n)"

    → Style Worker: "Check naming, formatting, patterns"
      ← "3 naming convention violations"

Orchestrator: Synthesizes into comprehensive review
```

### When to Use

- Complex tasks require multiple specializations
- Workers can operate independently
- Need centralized coordination

### When NOT to Use

- Simple tasks not worth decomposition overhead
- Workers need heavy inter-communication

---

## Pattern 5: 🩻 Evaluator-Optimizer

### Definition

Generate candidates, evaluate them, and iteratively improve until quality threshold is met.

### Diagram

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart TB
    classDef user fill:#6366f1,stroke:#4f46e5,stroke-width:2px,color:#ffffff
    classDef data fill:#06b6d4,stroke:#0891b2,stroke-width:2px,color:#ffffff
    classDef main fill:#8b5cf6,stroke:#7c3aed,stroke-width:2px,color:#ffffff
    classDef wizard fill:#14b8a6,stroke:#0d9488,stroke-width:2px,color:#ffffff
    classDef success fill:#10b981,stroke:#059669,stroke-width:2px,color:#ffffff
    classDef error fill:#ef4444,stroke:#dc2626,stroke-width:2px,color:#ffffff

    INPUT["🙋‍♀️📥 Task"]:::user --> GEN["🐔💭 Generate"]:::main
    GEN --> CAND["🐔📤 Candidate"]:::data
    CAND --> EVAL{"🐔🩻 Evaluate"}:::wizard

    EVAL -->|"🐔✅ Pass"| OUTPUT["💁‍♀️📤 Output"]:::success
    EVAL -->|"🐔❌ Fail"| FEEDBACK["🐔🔄 Feedback"]:::error
    FEEDBACK --> GEN
```

### Detailed Flow

```mermaid
%%{init: {'theme': 'base'}}%%
sequenceDiagram
    participant U as 🙋‍♀️ User
    participant G as 🐔💭 Generator
    participant E as 🐔🩻 Evaluator

    U->>G: 🙋‍♀️📥 Request
    loop 🔄 Until quality threshold
        G->>G: 🐔💭 Generate candidate
        G->>E: 🐔📤 Submit for evaluation
        E->>E: 🐔👀 Score candidate
        alt ✅ Score >= threshold
            E->>U: 💁‍♀️📤 Accept
        else ❌ Score < threshold
            E->>G: 🐔🔄 Feedback for improvement
        end
    end
```

### Evaluation Criteria Examples

| Domain | Criteria |
|--------|----------|
| **Code** | Tests pass, linting clean, no security issues |
| **Text** | Clarity score, factual accuracy, tone match |
| **Design** | Usability score, accessibility, consistency |

### Example: Code Generation

```
Generator: Write function to parse CSV

Attempt 1: Basic implementation
Evaluator: "Missing error handling for malformed input"

Attempt 2: Added try/catch
Evaluator: "Not handling empty files"

Attempt 3: Complete implementation
Evaluator: "Pass - all criteria met"
```

### When to Use

- Quality is critical
- Clear evaluation criteria exist
- Iteration improves results

### When NOT to Use

- First attempt is usually good enough
- No clear quality metrics
- Time constraints prevent iteration

---

## Pattern 6: 🐉 Autonomous Agents

### Definition

Long-running agents that independently plan, execute, and adapt based on environment feedback.

### Diagram

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart TB
    classDef user fill:#6366f1,stroke:#4f46e5,stroke-width:2px,color:#ffffff
    classDef data fill:#06b6d4,stroke:#0891b2,stroke-width:2px,color:#ffffff
    classDef main fill:#8b5cf6,stroke:#7c3aed,stroke-width:2px,color:#ffffff
    classDef state fill:#10b981,stroke:#059669,stroke-width:2px,color:#ffffff
    classDef wizard fill:#14b8a6,stroke:#0d9488,stroke-width:2px,color:#ffffff

    GOAL["🙋‍♀️📥 Goal"]:::user --> PLAN["🐔📋 Plan"]:::main
    PLAN --> ACT["🐔⚡ Act"]:::state
    ACT --> ENV["🌍 Environment"]:::data
    ENV --> OBSERVE["🐔👀 Observe"]:::data
    OBSERVE --> REFLECT{"🐔💭 Reflect"}:::wizard

    REFLECT -->|"🐔🔄 Adjust"| PLAN
    REFLECT -->|"🐔▶️ Continue"| ACT
    REFLECT -->|"🐔✅ Done"| DONE["💁‍♀️📤 Result"]:::user
```

### Agent Loop

```mermaid
%%{init: {'theme': 'base'}}%%
stateDiagram-v2
    [*] --> Planning: 🙋‍♀️📥 Receive goal
    Planning --> Executing: 🐔📋 Create plan
    Executing --> Observing: 🐔⚡ Take action
    Observing --> Reflecting: 🐔👀 Get feedback
    Reflecting --> Planning: 🐔🔄 Adjust
    Reflecting --> Executing: 🐔▶️ Continue
    Reflecting --> [*]: 💁‍♀️📤 Goal achieved
```

### Characteristics

| Characteristic | Description |
|----------------|-------------|
| **Goal-directed** | Works toward specified objective |
| **Adaptive** | Adjusts based on feedback |
| **Self-directed** | Decides next actions independently |
| **Persistent** | Continues until goal achieved or failure |

### Example: Bug Investigation

```
Goal: "Fix the login timeout bug"

Agent:
1. PLAN: Need to find where timeout is set
2. ACT: Search codebase for "timeout" in auth
3. OBSERVE: Found 3 locations
4. REFLECT: Most likely in session config
5. ACT: Read session config file
6. OBSERVE: Default timeout is 30 minutes
7. REFLECT: User reported issue after 5 minutes
8. ACT: Check if there's an override
9. ...continues until resolved...
```

### Risk Management

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart LR
    classDef user fill:#6366f1,stroke:#4f46e5,stroke-width:2px,color:#ffffff
    classDef main fill:#8b5cf6,stroke:#7c3aed,stroke-width:2px,color:#ffffff
    classDef state fill:#10b981,stroke:#059669,stroke-width:2px,color:#ffffff
    classDef error fill:#ef4444,stroke:#dc2626,stroke-width:2px,color:#ffffff

    subgraph Guardrails["🛡️ Guardrails"]
        LIMIT["⏱️ Iteration Limit"]:::error
        APPROVAL["🙆‍♀️✅ Human Approval"]:::user
        SCOPE["🔒 Action Scope"]:::error
        ROLLBACK["↩️ Rollback Capability"]:::error
    end

    AGENT["🐔 Main Agent (autonomous)"]:::main --> Guardrails
    Guardrails --> SAFE["✅ Safe Execution"]:::state

    style Guardrails fill:#fef2f2,stroke:#ef4444,stroke-width:2px
```

### When to Use

- Open-ended exploration tasks
- Environment feedback is rich
- Human oversight is available

### When NOT to Use

- Predictable tasks with known steps
- No rollback capability
- Tight time constraints

---

## Pattern Comparison

```
┌──────────────────────────┬─────────────┬─────────────┬──────────────┬───────────┐
│ Pattern                  │ Complexity  │ Parallelism │ Human-Loop   │ Iteration │
├──────────────────────────┼─────────────┼─────────────┼──────────────┼───────────┤
│ ⛓️ Prompt Chaining        │ Low         │ None        │ Optional     │ Linear    │
│ 🚦 Routing                │ Low         │ None        │ None         │ None      │
│ 🛤️ Parallelization        │ Medium      │ High        │ Optional     │ None      │
│ 🎭 Orchestrator-Workers   │ High        │ High        │ Optional     │ As needed │
│ 🩻 Evaluator-Optimizer    │ Medium      │ Optional    │ Optional     │ Loop      │
│ 🐉 Autonomous Agent       │ Very High   │ Variable    │ Recommended  │ Adaptive  │
└──────────────────────────┴─────────────┴─────────────┴──────────────┴───────────┘
```

---

## Combining Patterns

These patterns are building blocks that combine:

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart TB
    classDef user fill:#6366f1,stroke:#4f46e5,stroke-width:2px,color:#ffffff
    classDef wizard fill:#14b8a6,stroke:#0d9488,stroke-width:2px,color:#ffffff
    classDef main fill:#8b5cf6,stroke:#7c3aed,stroke-width:2px,color:#ffffff
    classDef parallel fill:#3b82f6,stroke:#2563eb,stroke-width:2px,color:#ffffff

    subgraph Combined["🔗 Complex System"]
        R["🐔🚦 Routing"]:::wizard --> OW["🐔🎭 Orchestrator"]:::main
        OW -->|"🐔🪺"| P["🐦⚡ Parallel Workers"]:::parallel
        P -->|"🐦📤"| EO["🐔🩻 Evaluator"]:::wizard
    end

    INPUT["🙋‍♀️📥 Input"]:::user --> R
    EO -->|"🐔📤"| OUTPUT["💁‍♀️📤 Output"]:::user

    style Combined fill:#f8fafc,stroke:#e2e8f0,stroke-width:2px
```

### Example: Code Review Pipeline

1. **🚦 Routing**: Classify code change type
2. **🎭 Orchestrator-Workers**: Assign to security, perf, style workers
3. **🛤️ Parallelization**: Workers run concurrently
4. **🩻 Evaluator-Optimizer**: Iterate on feedback if issues found

---

## Pattern Comparisons

### 🚦 Routing vs 🛤️ Parallelization

These two patterns are often confused but serve fundamentally different purposes:

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart LR
    classDef user fill:#6366f1,stroke:#4f46e5,stroke-width:2px,color:#ffffff
    classDef main fill:#8b5cf6,stroke:#7c3aed,stroke-width:2px,color:#ffffff
    classDef subagent fill:#ec4899,stroke:#db2777,stroke-width:2px,color:#ffffff
    classDef parallel fill:#3b82f6,stroke:#2563eb,stroke-width:2px,color:#ffffff
    classDef idle fill:#94a3b8,stroke:#64748b,stroke-width:2px,color:#ffffff

    subgraph ROUTING["🚦 Routing: Choose ONE"]
        R_IN["🙋‍♀️📥"]:::user --> R_DECIDE{"🐔🚦"}:::main
        R_DECIDE -.-> R_A["🐦💤 A"]:::idle
        R_DECIDE --> R_B["🐦⚡ B"]:::subagent
        R_DECIDE -.-> R_C["🐦💤 C"]:::idle
        R_B --> R_OUT["💁‍♀️📤"]:::user
    end

    subgraph PARALLEL["🛤️ Parallelization: Run ALL"]
        P_IN["🙋‍♀️📥"]:::user --> P_SPLIT["🐔🔀"]:::main
        P_SPLIT --> P_A["🐦⚡ A"]:::parallel
        P_SPLIT --> P_B["🐦⚡ B"]:::parallel
        P_SPLIT --> P_C["🐦⚡ C"]:::parallel
        P_A --> P_MERGE["🐔🌀"]:::main
        P_B --> P_MERGE
        P_C --> P_MERGE
        P_MERGE --> P_OUT["💁‍♀️📤"]:::user
    end

    style ROUTING fill:#fef2f2,stroke:#ef4444,stroke-width:2px
    style PARALLEL fill:#eff6ff,stroke:#3b82f6,stroke-width:2px
```

| Aspect | 🚦 Routing | 🛤️ Parallelization |
|--------|-----------|-------------------|
| **Action** | Choose **ONE** branch | Execute **ALL** branches |
| **Logic** | `if/else`, `switch/case` | `fork/join`, `Promise.all` |
| **Question** | "Where should I send this?" | "How can I do all this at once?" |
| **Result** | Single output from chosen handler | Multiple outputs merged |

**Analogy**:
- 🚦 **Routing** = Train switch → One train takes ONE track
- 🛤️ **Parallelization** = Multiple trains → All trains run simultaneously

---

### 🛤️ Parallelization vs 🎭 Orchestrator-Workers

These two patterns both use multiple workers but for different purposes:

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart LR
    classDef user fill:#6366f1,stroke:#4f46e5,stroke-width:2px,color:#ffffff
    classDef main fill:#8b5cf6,stroke:#7c3aed,stroke-width:2px,color:#ffffff
    classDef subagent fill:#ec4899,stroke:#db2777,stroke-width:2px,color:#ffffff
    classDef parallel fill:#3b82f6,stroke:#2563eb,stroke-width:2px,color:#ffffff

    subgraph PARALLEL["🛤️ Parallelization: SAME Task"]
        P_IN["🙋‍♀️📥"]:::user --> P_SPLIT["🐔🔀"]:::main
        P_SPLIT --> P_A["🐦⚡ Chunk 1"]:::parallel
        P_SPLIT --> P_B["🐦⚡ Chunk 2"]:::parallel
        P_SPLIT --> P_C["🐦⚡ Chunk 3"]:::parallel
        P_A --> P_MERGE["🐔🌀"]:::main
        P_B --> P_MERGE
        P_C --> P_MERGE
        P_MERGE --> P_OUT["💁‍♀️📤"]:::user
    end

    subgraph ORCH["🎭 Orchestrator: DIFFERENT Tasks"]
        O_IN["🙋‍♀️📥"]:::user --> O_MAIN["🐔🎭"]:::main
        O_MAIN --> O_A["🐦🔒 Security"]:::subagent
        O_MAIN --> O_B["🐦⚡ Perf"]:::subagent
        O_MAIN --> O_C["🐦🎨 Style"]:::subagent
        O_A --> O_SYNTH["🐔🌀"]:::main
        O_B --> O_SYNTH
        O_C --> O_SYNTH
        O_SYNTH --> O_OUT["💁‍♀️📤"]:::user
    end

    style PARALLEL fill:#eff6ff,stroke:#3b82f6,stroke-width:2px
    style ORCH fill:#fdf4ff,stroke:#ec4899,stroke-width:2px
```

| Aspect | 🛤️ Parallelization | 🎭 Orchestrator-Workers |
|--------|-------------------|------------------------|
| **Workers** | **Interchangeable** (same skill) | **Specialized** (different skills) |
| **Task type** | **Identical** task on different data | **Different** tasks on same data |
| **Decision** | **Static** (predefined split) | **Dynamic** (orchestrator decides) |
| **Example** | 3 cooks make same recipe | Chef + Pastry + Sommelier |

**Analogy**:
- 🛤️ **Parallelization** = Assembly line → Same job, more workers = faster
- 🎭 **Orchestrator-Workers** = Hospital team → Different experts collaborate

---

<div align="center">

**━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━**

[← 02 Architecture](02-LAYER-ARCHITECTURE.md) • [🏠 Home](README.md) • [04 Implementation →](04-CLAUDE-CODE-PATTERNS.md)

</div>
