<div align="center">

[🏠 Home](../../README.md) • [📚 Concepts](../README.md) • [⚙️ Workflows](./) • **⛓️ Prompt Chaining**

</div>

---

# 1. ⛓️ Prompt Chaining

> **Definition:** Decompose a task into a sequence of steps, where each LLM call processes the output of the previous one.

---

## Diagram

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart LR
    classDef user fill:#6366f1,stroke:#4f46e5,stroke-width:2px,color:#ffffff
    classDef main fill:#8b5cf6,stroke:#7c3aed,stroke-width:2px,color:#ffffff
    classDef gate fill:#f59e0b,stroke:#d97706,stroke-width:2px,color:#ffffff
    classDef exit fill:#ef4444,stroke:#dc2626,stroke-width:2px,color:#ffffff

    USER["🙋‍♀️📥"]:::user --> P1["🐔💭 Step 1"]:::main
    P1 -->|"🐔📤"| G1{"🚧 Gate"}:::gate
    G1 -->|Pass| P2["🐔💭 Step 2"]:::main
    G1 -.->|Fail| EXIT["❌ Exit"]:::exit
    P2 -->|"🐔📤"| G2{"🚧 Gate"}:::gate
    G2 -->|Pass| P3["🐔💭 Step 3"]:::main
    G2 -.->|Fail| EXIT
    P3 -->|"🐔📤"| OUT["💁‍♀️📤"]:::user
```

---

## 🚧 Gate

> **Definition:** A checkpoint between steps that validates the output before proceeding. If validation fails, the chain exits early instead of propagating errors downstream.

**Gates can check for:**
- Output format/structure validity
- Quality thresholds (confidence scores, completeness)
- Safety checks (content moderation, guardrails)
- Business rules (required fields, constraints)

---

## Characteristics

| Property | Value |
|----------|-------|
| **Complexity** | Low |
| **Parallelism** | None |
| **Human-Loop** | Optional |
| **Iteration** | Linear |

---

## When to use this workflow

This workflow is ideal for situations where the task can be easily and cleanly decomposed into fixed subtasks. The main goal is to trade off latency for higher accuracy, by making each LLM call an easier task.

---

## Examples where prompt chaining is useful

| Use Case | Chain |
|----------|-------|
| Marketing | Generate copy → Translate to target language |
| Documents | Write outline → Validate criteria → Write document |
| Code generation | Plan → Implement → Review |
| Data transformation | Parse → Transform → Validate |

---

## Example Flow

```
Step 1: "Extract all function names from this code"
        → [list of functions]

Step 2: "For each function, identify parameters and return types"
        → [function signatures]

Step 3: "Generate documentation for each function"
        → [documented code]
```

---

## When NOT to use

- Steps can be done independently (use 🛤️ Parallelization)
- Simple single-step tasks (use 🏎️ Direct Execution)

---

## Variant: 🧙 Wizard Workflow

Multi-step process with explicit 🙆‍♀️ user confirmation at each phase using ❓ `AskUserQuestion`.

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
stateDiagram-v2
    [*] --> Analysis: 🙋‍♀️📥 User Request

    Analysis --> Confirm1: Present findings
    Confirm1 --> Planning: 🙆‍♀️✅ User approves
    Confirm1 --> Analysis: 🙆‍♀️❓ User requests changes

    Planning --> Confirm2: Present plan
    Confirm2 --> Implementation: 🙆‍♀️✅ User approves
    Confirm2 --> Planning: 🙆‍♀️❓ User requests changes

    Implementation --> Confirm3: Show changes
    Confirm3 --> Verification: 🙆‍♀️✅ User approves
    Confirm3 --> Implementation: 🙆‍♀️❓ User requests changes

    Verification --> [*]: ✅ Complete
```

**Use 🧙 Wizard for:**
- Destructive operations (migrations, deletions)
- Complex refactoring
- Multi-stakeholder decisions

---

<div align="center">

**━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━**

[← 01 Baseline](01-baseline.md) • [⚙️ Workflows](./) • [03 Routing →](03-routing.md)

</div>
