<div align="center">

[🏠 Home](../../README.md) • [📚 Concepts](../README.md) • [⚙️ Workflows](./) • **🦑 Orchestrator-Workers**

</div>

---

# 4. 🦑 Orchestrator-Workers

> **Definition:** A central LLM dynamically breaks down tasks, delegates them to worker LLMs, and synthesizes their results.

---

## Diagram

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {'lineColor': '#64748b'}}}%%
flowchart TB
    classDef user fill:#6366f1,stroke:#4f46e5,stroke-width:2px,color:#ffffff
    classDef main fill:#8b5cf6,stroke:#7c3aed,stroke-width:2px,color:#ffffff
    classDef subagent fill:#ec4899,stroke:#db2777,stroke-width:2px,color:#ffffff

    INPUT["🙋‍♀️📥 Review this PR"]:::user --> ORCH["🐔 Main Agent"]:::main

    ORCH -->|"🐔🪺 Check vulns"| W1["🐦🔒 Security Expert"]:::subagent
    ORCH -->|"🐔🪺 Check perf"| W2["🐦⚡ Performance Expert"]:::subagent
    ORCH -->|"🐔🪺 Check style"| W3["🐦🎨 Style Expert"]:::subagent

    W1 -->|"🐦📤 2 SQLi found"| SYNTH["🐔🌀 Synthesize"]:::main
    W2 -->|"🐦📤 O(n²) loop"| SYNTH
    W3 -->|"🐦📤 3 violations"| SYNTH

    SYNTH -->|"🐔📤"| OUTPUT["💁‍♀️📤 Final Report"]:::user
```

---

## Key Insight

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  🦑 ORCHESTRATOR-WORKERS: Different specialists                             │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  Each 🐦 subagent has a DIFFERENT expertise and does a DIFFERENT task.     │
│                                                                             │
│  Key difference from 🛤️ Parallelization: subtasks aren't pre-defined,      │
│  but determined by the orchestrator based on the specific input.            │
│                                                                             │
│  Analogy: Hospital team → Different experts collaborate                     │
│           (Chef + Pastry + Sommelier, not 3 cooks making same recipe)      │
│                                                                             │
│  Compare:                                                                   │
│  - 🛤️ Parallelization: Same worker + Different data (assembly line)        │
│  - 🦑 Orchestration: Different workers + Same data (expert team)           │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Characteristics

| Property | Value |
|----------|-------|
| **Complexity** | High |
| **Parallelism** | High |
| **Human-Loop** | Optional |
| **Iteration** | As needed |

---

## When to use this workflow

This workflow is well-suited for complex tasks where you can't predict the subtasks needed. The key difference from parallelization is its flexibility—subtasks aren't pre-defined, but determined by the orchestrator based on the specific input.

---

## Examples where orchestrator-workers is useful

| Use Case | Orchestration |
|----------|---------------|
| Coding products | Make complex changes to multiple files dynamically |
| Search tasks | Gather and analyze from multiple sources |
| PR Review | Security + Performance + Style experts |

---

## 🐔 Main Agent Responsibilities

| Responsibility | Description |
|----------------|-------------|
| **Decomposition** | Break complex task into subtasks |
| **Assignment** | Route subtasks to appropriate 🐦 subagents |
| **Monitoring** | Track 🐦 subagent progress |
| **Synthesis** | Combine results into coherent output |

---

## 🐦 Subagent Definition

```markdown
# .claude/agents/code-reviewer.md

---
name: code-reviewer
description: Reviews code for quality, security, and best practices. Use for PR reviews, code audits, and quality checks.
tools: Read, Grep, Glob
model: sonnet
permissionMode: plan
---

You are a senior code reviewer with expertise in security, performance, and maintainability.

## Your Task

Review the provided code and produce a structured report.

## Review Checklist

1. **Security** - SQL injection, XSS, secrets exposure, auth bypasses
2. **Performance** - O(n²) loops, memory leaks, unnecessary computations
3. **Code Quality** - DRY violations, dead code, unclear naming
4. **Best Practices** - Error handling, logging, testing coverage

## Output Format

Return your review as:

## Summary
[1-2 sentence overview]

## Issues Found

### ❌ CRITICAL (must fix before merge)
- [file:line] Issue description
  Recommendation: ...

### ⚠️ WARNING (should address)
- [file:line] Issue description
  Recommendation: ...

### ℹ️ SUGGESTIONS (nice to have)
- [file:line] Issue description
  Recommendation: ...

## Verdict
[ ] ✅ APPROVED - Ready to merge
[ ] ⚠️ APPROVED WITH COMMENTS - Minor issues
[ ] ❌ CHANGES REQUESTED - Must address critical issues
```

---

## Full Orchestration Example

```python
# 🐔 Main Agent orchestrates PR review with specialists

# Step 1: Decompose - identify what experts are needed
changed_files = get_pr_diff()  # ["auth.py", "api.py", "styles.css"]

# Step 2: Assign - spawn appropriate specialists
Task(
    subagent_type="security-reviewer",
    prompt=f"Review these files for security: {changed_files}"
)

Task(
    subagent_type="performance-reviewer",
    prompt=f"Review these files for performance: {changed_files}"
)

Task(
    subagent_type="style-reviewer",
    prompt=f"Review these files for style/quality: {changed_files}"
)

# Step 3: Monitor - wait for all subagents to complete
# (handled automatically by Task tool)

# Step 4: Synthesize - combine into final report
"""
## PR Review: #123 - Add user authentication

### Security Review (🐦 security-reviewer)
❌ CRITICAL: SQL injection in auth.py:45
⚠️ WARNING: Weak password policy

### Performance Review (🐦 performance-reviewer)
⚠️ WARNING: O(n²) loop in api.py:78

### Style Review (🐦 style-reviewer)
ℹ️ INFO: Consider extracting duplicate code

### Final Verdict: ❌ CHANGES REQUESTED
Must fix SQL injection before merge.
"""
```

---

## Critical Rules

| Rule | Explanation |
|------|-------------|
| **No nested subagents** | 🐦 Subagents cannot spawn other 🐦 subagents |
| **Isolated context** | Each 🐦 subagent starts fresh, no shared memory |
| **Report to orchestrator** | Results flow back to 🐔 Main Agent only |

---

## When NOT to use

- Simple tasks not worth decomposition overhead
- Workers need heavy inter-communication

---

<div align="center">

**━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━**

[← 04 Parallelization](04-parallelization.md) • [⚙️ Workflows](./) • [06 Evaluator-Optimizer →](06-evaluator-optimizer.md)

</div>
