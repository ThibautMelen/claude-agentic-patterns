<div align="center">

[🏠 Home](../README.md) › [📖 Reference](./) › **Built-in Subagents**

[← Visual Standards](visual-standards.md) ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━●━━ [Reference →](./)

</div>

---

# Built-in Subagents

> Pre-configured subagents available out of the box in Claude Code

---

## Overview

Claude Code includes pre-configured subagents that can be invoked immediately without custom definitions.

| Subagent | Model | Tools | Purpose |
|----------|-------|-------|---------|
| **General-purpose** | Sonnet | All tools | Complex multi-step tasks requiring exploration and action |
| **Plan** | Sonnet | Read, Glob, Grep, Bash | Research in plan mode (read-only exploration) |
| **Explore** | Haiku | Glob, Grep, Read, Bash (read-only) | Fast codebase searching and analysis |

---

## General-purpose Subagent

Used when tasks require both exploration and modification. Handles:

- Complex reasoning to interpret search results
- Multiple strategies if initial searches fail
- Multi-step operations with dependencies

### When to Use

- Complex multi-step tasks
- Tasks requiring both reading and writing
- When flexibility is needed

### Example

```python
Task(
    subagent_type="general-purpose",
    prompt="Refactor the authentication module to use JWT tokens"
)
```

---

## Plan Subagent

Specialized for plan mode research. Automatically invoked when Claude needs to understand codebase before creating a plan.

### Key Characteristics

- Read-only access
- Cannot make modifications
- Prevents infinite nesting (subagents cannot spawn other subagents)

### When to Use

- Codebase exploration before planning
- Research without modification risk
- Understanding existing architecture

### Example

```python
Task(
    subagent_type="Plan",
    prompt="Analyze the current database schema and identify optimization opportunities"
)
```

---

## Explore Subagent

Fast, lightweight agent optimized for read-only codebase exploration.

### Thoroughness Levels

| Level | Use Case | Speed | Coverage |
|-------|----------|-------|----------|
| `quick` | Basic searches, simple lookups | Fastest | Limited |
| `medium` | Moderate exploration, balanced | Moderate | Good |
| `very thorough` | Comprehensive analysis | Slowest | Complete |

### When to Use

- Finding specific code patterns
- Quick codebase navigation
- Answering "where is X?" questions

### Example Interaction

```
User: "Where are errors from the client handled?"

Claude: [Invokes Explore subagent with "medium" thoroughness]
→ Searches for error handling patterns
→ Examines promising files
→ Returns: "Client errors are handled in src/services/process.ts:712..."
```

### Example Code

```python
Task(
    subagent_type="Explore",
    prompt="Find all authentication-related files and describe the auth flow",
    model="haiku"  # Uses Haiku for speed
)
```

---

## Comparison Table

| Aspect | General-purpose | Plan | Explore |
|--------|-----------------|------|---------|
| **Model** | Sonnet | Sonnet | Haiku |
| **Speed** | Moderate | Moderate | Fast |
| **Can Write** | ✅ | ❌ | ❌ |
| **Can Spawn** | ❌ | ❌ | ❌ |
| **Best For** | Complex tasks | Research | Quick search |
| **Tool Access** | All | Read-only | Read-only |

---

## Real-World Usage Examples

### Example 1: Research Before Implementation

```python
# User: "Add dark mode to the app"

# Step 1: Explore - understand current styling
Task(
    subagent_type="Explore",
    prompt="Find all CSS/styling files and identify the current theming approach. Look for: 1) CSS variables 2) Theme providers 3) Color constants",
    description="Explore theming approach"
)
# Returns: "Found Tailwind config at tailwind.config.js, CSS variables in globals.css..."

# Step 2: Plan - design the implementation
Task(
    subagent_type="Plan",
    prompt="Based on the Tailwind setup found, create a plan to implement dark mode using CSS variables and Tailwind's dark: variant",
    description="Plan dark mode implementation"
)
# Returns detailed implementation plan

# Step 3: Implement - make the changes
Task(
    subagent_type="general-purpose",
    prompt="Implement dark mode following the plan. Create theme toggle component, update Tailwind config, add dark variants to key components.",
    description="Implement dark mode"
)
```

### Example 2: Code Investigation

```python
# User: "Why is the API slow?"

# Quick search for performance issues
Task(
    subagent_type="Explore",
    prompt="Search for potential performance issues: 1) N+1 queries 2) Missing indexes 3) Synchronous operations that should be async 4) Large data fetches without pagination. Thoroughness: very thorough",
    description="Performance investigation"
)
# Returns: "Found N+1 query in users.py:45, missing index on orders.created_at..."
```

### Example 3: Multi-File Refactoring

```python
# User: "Rename UserService to AccountService across the codebase"

# First explore the scope
Task(
    subagent_type="Explore",
    prompt="Find all files referencing UserService - imports, instantiations, type annotations, tests",
    description="Find UserService references"
)
# Returns: "Found 23 references in 12 files..."

# Then execute the refactoring
Task(
    subagent_type="general-purpose",
    prompt="Rename UserService to AccountService in all 12 files identified. Update: class name, file name, imports, type hints, and test references. Ensure tests still pass.",
    description="Execute rename refactoring"
)
```

### Example 4: Documentation Generation

```python
# User: "Generate API documentation for the auth module"

# Research the module structure
Task(
    subagent_type="Plan",
    prompt="Analyze src/auth/ module: identify all public functions, classes, their parameters, return types, and existing docstrings. Create an outline for comprehensive API docs.",
    description="Analyze auth module for docs"
)
# Returns structured analysis

# Generate the documentation
Task(
    subagent_type="general-purpose",
    prompt="Generate API documentation for src/auth/ based on the analysis. Include: function signatures, parameter descriptions, return values, usage examples, and error handling.",
    description="Generate API docs"
)
```

---

## Selection Guide

```
Need to modify files?
├─ Yes → General-purpose
└─ No
    ├─ Need deep analysis? → Plan
    └─ Quick lookup? → Explore
```

---

## Usage in Task Tool

```python
# General-purpose - full capabilities
Task(
    subagent_type="general-purpose",
    prompt="Implement the new feature",
    model="sonnet"
)

# Plan - research mode
Task(
    subagent_type="Plan",
    prompt="Analyze the codebase architecture"
)

# Explore - fast search
Task(
    subagent_type="Explore",
    prompt="Find all API endpoints",
    description="Quick codebase exploration"
)
```

---

## Critical Rule

> **🐦 Built-in subagents CANNOT spawn other subagents.**
>
> All delegation must flow through the 🐔 Main Agent.

---

<div align="center">

[← Visual Standards](visual-standards.md) ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━●━━ [Reference →](./)

</div>
