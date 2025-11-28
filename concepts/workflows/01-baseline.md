<div align="center">

[🏠 Home](../../README.md) • [📚 Concepts](../README.md) • [⚙️ Workflows](./) • **🏎️ Baseline**

</div>

---

# 0. 🏎️ Baseline (Direct Execution)

> **Definition:** Single augmented LLM call without orchestration — the foundation before adding workflow complexity. Not counted as a workflow by Anthropic, but included here to show the full progression.

---

## Diagram

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart LR
    classDef user fill:#6366f1,stroke:#4f46e5,stroke-width:2px,color:#ffffff
    classDef main fill:#8b5cf6,stroke:#7c3aed,stroke-width:2px,color:#ffffff

    USER["🙋‍♀️📥 User Request"]:::user --> MA["🐔💭 Main Agent"]:::main
    MA -->|"🐔📤"| OUT["💁‍♀️📤 User Receives"]:::user
```

---

## Characteristics

| Property | Value |
|----------|-------|
| **Complexity** | None |
| **Parallelism** | None |
| **Human-Loop** | None |
| **Iteration** | None |

---

## When to use this workflow

- Simple, single-step tasks
- No need for specialization
- Quick operations (file read, simple edit, search)

---

## Examples where direct execution is useful

- "What's in the config.json file?"
- "Add a console.log statement to this function"
- "Search for usages of `useState`"

---

## When NOT to use

- Complex multi-step workflows
- Tasks requiring multiple specializations
- Large-scale operations

---

<div align="center">

**━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━**

[← 00 Building Block](00-building-block.md) • [⚙️ Workflows](./) • [02 Prompt Chaining →](02-prompt-chaining.md)

</div>
