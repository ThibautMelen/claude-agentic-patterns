<div align="center">

[🏠 Home](../../README.md) • [📚 Concepts](../README.md) • **Agents**

</div>

---

# Agents

> **Definition (Anthropic):** Systems where LLMs **dynamically direct their own processes and tool usage**, maintaining control over how they accomplish tasks.
>
> — [Building Effective Agents](https://www.anthropic.com/engineering/building-effective-agents), December 2024

**Key characteristic:** The **LLM** controls the flow, not the code

---

## Workflows vs Agents

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    WORKFLOWS vs AGENTS — Key Distinction                    │
├────────────────────────────────────┬────────────────────────────────────────┤
│            WORKFLOWS               │              AGENTS                     │
├────────────────────────────────────┼────────────────────────────────────────┤
│  CODE controls the flow            │  LLM controls the flow                 │
│  Predefined paths                  │  Dynamic decisions                     │
│  Predictable execution             │  Adaptive behavior                     │
│  Lower autonomy                    │  Higher autonomy                       │
│  Lower risk                        │  Higher risk (need guardrails)         │
│  Faster, cheaper                   │  Slower, more expensive                │
│                                    │                                        │
│  → Use for WELL-DEFINED tasks      │  → Use for OPEN-ENDED problems         │
└────────────────────────────────────┴────────────────────────────────────────┘
```

---

## Agent Index

| # | Agent | Emoji | File | Description |
|---|-------|-------|------|-------------|
| 6 | Autonomous Agents | 🐉 | [autonomous-agents.md](autonomous-agents.md) | Self-directed with feedback |
| — | Multi-Window Context | 🖥️ | [multi-window-context.md](multi-window-context.md) | State persistence across sessions |

---

## Agent Summary

```
┌──────────────────────────┬─────────────┬─────────────┬──────────────┬───────────┐
│ Agent                    │ Complexity  │ Parallelism │ Human-Loop   │ Iteration │
├──────────────────────────┼─────────────┼─────────────┼──────────────┼───────────┤
│ 🐉 Autonomous Agent      │ Very High   │ Variable    │ Recommended  │ Adaptive  │
└──────────────────────────┴─────────────┴─────────────┴──────────────┴───────────┘
```

---

## Comparison with Workflows

| Aspect | ⚙️ Workflows | 🐉 Autonomous Agents |
|--------|-------------|-----------|
| **Control** | Code-directed | LLM-directed |
| **Path** | Predefined | Dynamic |
| **Steps** | Known upfront | Discovered at runtime |
| **Complexity** | Low to High | Very High |
| **Cost** | Lower, predictable | Higher, variable |
| **Risk** | Lower | Higher (needs guardrails) |
| **Use Case** | Well-defined tasks | Open-ended problems |

---

## Flow Examples

```
🐉 AUTONOMOUS AGENTS
🙋‍♀️📥 ──► 🐔📋 ──► 🐔⚡ ──► 🐔👀 ──► 🐔💭 ──┬──► 🐔🔄 ──► 🐔📋 (loop)
Goal       Plan      Act      Observe   Reflect │
                                                └──► 🐔📤 ──► 📤💁‍♀️ (done)

🖥️ MULTI-WINDOW CONTEXT
Session 1: 🙋‍♀️📥 ──► 🐔📋 ──► 🐔⚡ ──► 🖥️💾 ──► [Context Limit]
                                      ↓
Session 2: 🖥️💾 ──► 🐔⚡ ──► 🐔👀 ──► 🐔💭 ──► 💁‍♀️📤
```

---

<div align="center">

**━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━**

[📚 Concepts](../README.md) • [⚙️ Workflows](../workflows/)

</div>
