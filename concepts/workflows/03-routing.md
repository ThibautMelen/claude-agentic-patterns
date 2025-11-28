<div align="center">

[🏠 Home](../../README.md) • [📚 Concepts](../README.md) • [⚙️ Workflows](./) • **🚦 Routing**

</div>

---

# 2. 🚦 Routing

> **Definition:** Classify an input and direct it to a specialized followup task. This allows separation of concerns and more specialized prompts.

---

## Diagram

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart TB
    classDef user fill:#6366f1,stroke:#4f46e5,stroke-width:2px,color:#ffffff
    classDef main fill:#8b5cf6,stroke:#7c3aed,stroke-width:2px,color:#ffffff
    classDef subagent fill:#ec4899,stroke:#db2777,stroke-width:2px,color:#ffffff
    classDef idle fill:#94a3b8,stroke:#64748b,stroke-width:2px,color:#ffffff

    INPUT["🙋‍♀️📥 User Request"]:::user --> ROUTER{"🐔🚦 Classify & Route"}:::main

    ROUTER -.->|"Type A"| HA["🐦💤 Handler A"]:::idle
    ROUTER -->|"🐔🪺 Type B"| HB["🐦⚡ Handler B"]:::subagent
    ROUTER -.->|"Type C"| HC["🐦💤 Handler C"]:::idle
    ROUTER -.->|"Unknown"| DEFAULT["🐔💤 Default"]:::idle

    HB -->|"🐦📤"| FINAL["💁‍♀️📤 User Receives"]:::user
```

---

## Key Insight

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  🚦 ROUTING: Choose ONE branch                                              │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  Logic: if/else, switch/case                                               │
│  Question: "Where should I send this?"                                      │
│  Result: Single output from chosen handler                                  │
│                                                                             │
│  Analogy: Train switch → One train takes ONE track                         │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Characteristics

| Property | Value |
|----------|-------|
| **Complexity** | Low |
| **Parallelism** | None |
| **Human-Loop** | None |
| **Iteration** | None |

---

## When to use this workflow

Routing works well for complex tasks where there are distinct categories that are better handled separately, and where classification can be handled accurately.

---

## Examples where routing is useful

| Use Case | Routes |
|----------|--------|
| Customer support | Bug → Tech Team, Billing → Finance, General → FAQ |
| Code tasks | Bug fix → Debugger, New feature → Builder |
| Model routing | Easy → Claude Haiku 4.5, Hard → Claude Sonnet 4.5 |
| Content | Question → Q&A handler, Task → Executor |

---

## When NOT to use

- All inputs require same processing
- Classification is unreliable
- Categories overlap significantly

---

<div align="center">

**━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━**

[← 02 Prompt Chaining](02-prompt-chaining.md) • [⚙️ Workflows](./) • [04 Parallelization →](04-parallelization.md)

</div>
