<div align="center">

[🏠 Home](../../README.md) • [📚 Concepts](../README.md) • **⚙️ Workflows**

</div>

---

# Workflows

> **Definition (Anthropic):** Systems where LLMs and tools are orchestrated through **predefined code paths**.
>
> — [Building Effective Agents](https://www.anthropic.com/engineering/building-effective-agents), December 2024

**Key characteristic:** The **CODE** controls the flow, not the LLM

---

## Decision Tree

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart TD
    classDef question fill:#f59e0b,stroke:#d97706,stroke-width:2px,color:#ffffff
    classDef workflow fill:#8b5cf6,stroke:#7c3aed,stroke-width:2px,color:#ffffff
    classDef simple fill:#64748b,stroke:#475569,stroke-width:2px,color:#ffffff

    START["🙋‍♀️📥 Task Received"] --> Q1{"Single step?"}:::question

    Q1 -->|Yes| P1["🏎️ Direct Execution"]:::simple
    Q1 -->|No| Q2{"Steps dependent?"}:::question

    Q2 -->|Yes, sequential| P2["⛓️ Prompt Chaining"]:::workflow
    Q2 -->|No, parallel| Q3{"Same or different tasks?"}:::question

    Q3 -->|Same task, different data| P4["🛤️ Parallelization"]:::workflow
    Q3 -->|Different tasks| P5["🦑 Orchestrator-Workers"]:::workflow

    Q2 -->|Need classification first| P3["🚦 Routing"]:::workflow

    START --> Q4{"Quality critical?"}:::question
    Q4 -->|Yes, needs iteration| P6["🩻 Evaluator-Optimizer"]:::workflow
```

---

## Workflow Index

| # | Pattern | Emoji | File | Complexity |
|---|---------|-------|------|:----------:|
| — | Building Block | 🧱 | [00-building-block.md](00-building-block.md) | Foundation |
| 0 | Baseline (Direct) | 🏎️ | [01-baseline.md](01-baseline.md) | None |
| 1 | Prompt Chaining | ⛓️ | [02-prompt-chaining.md](02-prompt-chaining.md) | Low |
| 2 | Routing | 🚦 | [03-routing.md](03-routing.md) | Low |
| 3 | Parallelization | 🛤️ | [04-parallelization.md](04-parallelization.md) | Medium |
| 4 | Orchestrator-Workers | 🦑 | [05-orchestrator-workers.md](05-orchestrator-workers.md) | High |
| 5 | Evaluator-Optimizer | 🩻 | [06-evaluator-optimizer.md](06-evaluator-optimizer.md) | Medium |

---

## Workflow Summary

```
┌──────────────────────────┬─────────────┬─────────────┬──────────────┬───────────┐
│ Pattern                  │ Complexity  │ Parallelism │ Human-Loop   │ Iteration │
├──────────────────────────┼─────────────┼─────────────┼──────────────┼───────────┤
│ 0. 🏎️ Baseline           │ None        │ None        │ None         │ None      │
├──────────────────────────┼─────────────┼─────────────┼──────────────┼───────────┤
│ 1. ⛓️ Prompt Chaining     │ Low         │ None        │ Optional     │ Linear    │
│ 2. 🚦 Routing             │ Low         │ None        │ None         │ None      │
│ 3. 🛤️ Parallelization     │ Medium      │ High        │ Optional     │ None      │
│ 4. 🦑 Orchestrator-Workers│ High        │ High        │ Optional     │ As needed │
│ 5. 🩻 Evaluator-Optimizer │ Medium      │ Optional    │ Optional     │ Loop      │
└──────────────────────────┴─────────────┴─────────────┴──────────────┴───────────┘
```

---

## Workflow Variants (Claude Code specific)

> ⚠️ These are patterns we've identified in Claude Code usage, not official Anthropic terminology.

| Variant | Parent | Emoji | Description |
|---------|--------|-------|-------------|
| **Wizard Workflow** | ⛓️ Prompt Chaining | 🧙 | Human checkpoints via AskUserQuestion |
| **Parallel Tool Calling** | 🛤️ Parallelization | 🚂 | Multiple tools in single response |
| **Master-Clone** | 🛤️ Parallelization | 🧬 | Same agent, parallel instances |

→ Variants are documented within their parent workflow files.

---

## Flow Examples

```
⛓️ PROMPT CHAINING
🙋‍♀️📥 ──► 🐔💭 ──► 🐔📤 ──► 🐔💭 ──► 🐔📤 ──► 🐔💭 ──► 🐔📤 ──► 📤💁‍♀️
Input     Step 1    (chain)   Step 2    (chain)   Step 3    Output    User

🦑 ORCHESTRATOR-WORKERS
🙋‍♀️📥 ──► 🐔🔀 ──┬──► 🐦⚡ ──► 🐦📤 ──┐
                ├──► 🐦⚡ ──► 🐦📤 ──┼──► 🐔🌀 ──► 🐔📤 ──► 📤💁‍♀️
                └──► 🐦⚡ ──► 🐦📤 ──┘

🧙 WIZARD WORKFLOW (Human-in-the-Loop)
🙋‍♀️📥 ──► 🐔📋 ──► 🐔📤 ──► 📤💁‍♀️ ──► 🙆‍♀️✅ ──► 🐔▶️ ──► 🐔⚡ ──► 📤💁‍♀️
Request    Plan      Show      User      User      🐔        Execute   Done
                     plan      reviews   approves  continues
```

---

## Anthropic's Progression

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart LR
    classDef block fill:#3b82f6,stroke:#2563eb,stroke-width:2px,color:#ffffff
    classDef workflow fill:#8b5cf6,stroke:#7c3aed,stroke-width:2px,color:#ffffff
    classDef agent fill:#f59e0b,stroke:#d97706,stroke-width:2px,color:#ffffff

    A["🧱 Augmented LLM<br/><i>Building block</i>"]:::block
    W["⚙️ Workflows<br/><i>Composed blocks</i>"]:::workflow
    AG["🐉 Autonomous Agents<br/><i>Loops + feedback</i>"]:::agent

    A -->|"compose"| W
    W -->|"add autonomy"| AG
```

---

<div align="center">

**━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━**

[📚 Concepts](../README.md) • [Agents](../agents/)

</div>
