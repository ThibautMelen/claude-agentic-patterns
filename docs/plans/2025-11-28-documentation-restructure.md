# Documentation Restructure - Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Restructure the documentation from 8 flat files to a professional 35-file granular structure with proper hierarchy.

**Architecture:**
- 4 main directories: `concepts/`, `implementation/`, `guides/`, `reference/`
- Each directory has README.md as hub/index
- Atomic files: 1 concept = 1 file
- Johnny Decimal numbering within directories

**Tech Stack:** Markdown, Mermaid diagrams, GitHub-flavored markdown

---

## Current State → Target State

```
CURRENT (8 files flat)              TARGET (35 files hierarchical)
─────────────────────               ──────────────────────────────
README.md                     →     README.md (simplified)
00-OVERVIEW.md                →     concepts/README.md (merged)
01-OFFICIAL-TERMINOLOGY.md    →     Split into components/ + reference/
02-LAYER-ARCHITECTURE.md      →     implementation/architecture/ (split)
03-WORKFLOWS.md               →     concepts/workflows/ (split into 7)
04-AGENTS.md                  →     concepts/agents/ (split into 3)
05-USE-CASES.md               →     guides/use-cases/ (split into 7)
06-SELECTION-GUIDE.md         →     guides/selection-guide.md
07-MAPPING-GLOSSARY.md        →     reference/ (split into 3)
```

---

## Phase 1: Create Directory Structure

### Task 1.1: Create all directories

**Step 1: Create directory tree**

```bash
mkdir -p concepts/workflows concepts/agents
mkdir -p implementation/components implementation/architecture
mkdir -p guides/use-cases
mkdir -p reference
```

**Verification:** `find . -type d | grep -v ".git" | sort`

---

## Phase 2: Create Hub Files (README.md)

### Task 2.1: Create concepts/README.md (Main Hub)

**File:** `concepts/README.md`

**Content:** Hub for Agentic Systems - includes:
- What are Agentic Systems (umbrella term)
- Building Block overview
- Baseline + Workflows + Agents dispatch table
- Navigation to all concept files
- Cross-platform compatibility matrix

**Source:** Extract from:
- `00-OVERVIEW.md` (Anthropic Taxonomy section)
- `README.md` (Overview section)
- `01-OFFICIAL-TERMINOLOGY.md` (Section 0 + Section 2.1-2.2)

---

### Task 2.2: Create concepts/workflows/README.md

**File:** `concepts/workflows/README.md`

**Content:** Index for workflows:
- Decision tree flowchart
- Dispatch table (which workflow for what)
- Links to individual workflow files
- Comparison summary table

**Source:** Extract from `03-WORKFLOWS.md`:
- Table of Contents
- Decision Tree section
- Workflow Summary table

---

### Task 2.3: Create concepts/agents/README.md

**File:** `concepts/agents/README.md`

**Content:** Index for agents:
- Workflows vs Agents comparison
- When to use agents
- Links to individual agent files

**Source:** Extract from `04-AGENTS.md`:
- Workflows vs Agents section
- Table of Contents

---

### Task 2.4: Create implementation/README.md

**File:** `implementation/README.md`

**Content:** Implementation overview:
- Components vs Building Block distinction
- Architecture overview
- Links to components/ and architecture/

---

### Task 2.5: Create implementation/components/README.md

**File:** `implementation/components/README.md`

**Content:** Components comparison:
- Comparison table (invocation, location, autonomy)
- Component relationships diagram
- File location reference
- Links to individual component files

**Source:** Extract from `01-OFFICIAL-TERMINOLOGY.md`:
- Section 1 intro
- Section 8.1 Components Comparison
- Section 8.2 Component Relationships

---

### Task 2.6: Create implementation/architecture/README.md

**File:** `implementation/architecture/README.md`

**Content:** Architecture overview:
- 5-Layer diagram (ASCII + Mermaid)
- Layer responsibilities matrix
- Complete layer interaction sequence
- Anti-patterns section
- Links to individual layer files

**Source:** Extract from `02-LAYER-ARCHITECTURE.md`:
- Overview section
- Complete Layer Interaction
- Layer Responsibilities Matrix
- Anti-Patterns

---

### Task 2.7: Create guides/README.md

**File:** `guides/README.md`

**Content:** Guides index:
- Selection guide summary
- Use cases quick reference
- Links to selection-guide.md and use-cases/

---

### Task 2.8: Create guides/use-cases/README.md

**File:** `guides/use-cases/README.md`

**Content:** Use cases dispatch:
- Quick reference table (use case → patterns → link)
- Pattern selection by use case
- Links to individual use case files

**Source:** Extract from `05-USE-CASES.md`:
- Quick Reference section
- Table of Contents

---

### Task 2.9: Create reference/README.md

**File:** `reference/README.md`

**Content:** Reference index:
- Links to glossary, visual-standards, built-in-subagents
- Quick lookup tips

---

## Phase 3: Migrate Workflows Content

### Task 3.1: Create concepts/workflows/00-building-block.md

**File:** `concepts/workflows/00-building-block.md`

**Content:** The Augmented LLM foundation

**Source:** Extract from `03-WORKFLOWS.md`:
- "Building Block: The Augmented LLM" section (~30 lines)
- Mermaid diagram

---

### Task 3.2: Create concepts/workflows/01-baseline.md

**File:** `concepts/workflows/01-baseline.md`

**Content:** Direct Execution (Pattern #0)

**Source:** Extract from `03-WORKFLOWS.md`:
- "0. 🏎️ Baseline (Direct Execution)" section (~40 lines)

---

### Task 3.3: Create concepts/workflows/02-prompt-chaining.md

**File:** `concepts/workflows/02-prompt-chaining.md`

**Content:** Prompt Chaining + 🧙 Wizard variant

**Source:** Extract from `03-WORKFLOWS.md`:
- "1. ⛓️ Prompt Chaining" section (~100 lines)
- Include 🚧 Gate explanation
- Include 🧙 Wizard Workflow variant

---

### Task 3.4: Create concepts/workflows/03-routing.md

**File:** `concepts/workflows/03-routing.md`

**Content:** Routing pattern

**Source:** Extract from `03-WORKFLOWS.md`:
- "2. 🚦 Routing" section (~60 lines)

---

### Task 3.5: Create concepts/workflows/04-parallelization.md

**File:** `concepts/workflows/04-parallelization.md`

**Content:** Parallelization + variants (🚂 Parallel Tool Calling, 🧬 Master-Clone, 🗳️ Voting)

**Source:** Extract from `03-WORKFLOWS.md`:
- "3. 🛤️ Parallelization" section (~150 lines)
- Include Sectioning + Voting
- Include 🚂 and 🧬 variants

---

### Task 3.6: Create concepts/workflows/05-orchestrator-workers.md

**File:** `concepts/workflows/05-orchestrator-workers.md`

**Content:** Orchestrator-Workers pattern

**Source:** Extract from `03-WORKFLOWS.md`:
- "4. 🦑 Orchestrator-Workers" section (~120 lines)

---

### Task 3.7: Create concepts/workflows/06-evaluator-optimizer.md

**File:** `concepts/workflows/06-evaluator-optimizer.md`

**Content:** Evaluator-Optimizer + Self-Correction

**Source:** Extract from `03-WORKFLOWS.md`:
- "5. 🩻 Evaluator-Optimizer" section (~100 lines)
- Include Self-Correction Chains

---

## Phase 4: Migrate Agents Content

### Task 4.1: Create concepts/agents/autonomous-agents.md

**File:** `concepts/agents/autonomous-agents.md`

**Content:** Autonomous Agents (Pattern #6)

**Source:** Extract from `04-AGENTS.md`:
- "🐉 Autonomous Agents" section (~150 lines)
- Agent Loop
- Characteristics
- Examples
- Risk Management

---

### Task 4.2: Create concepts/agents/multi-window-context.md

**File:** `concepts/agents/multi-window-context.md`

**Content:** Multi-Window Context variant

**Source:** Extract from `04-AGENTS.md`:
- "Variant: 🖥️ Multi-Window Context" section (~60 lines)

---

## Phase 5: Migrate Components Content

### Task 5.1: Create implementation/components/subagent.md

**File:** `implementation/components/subagent.md`

**Content:** Complete 🐦 Subagent reference

**Source:** Extract from `01-OFFICIAL-TERMINOLOGY.md`:
- Section 1.1 🐦 Subagent (~120 lines)

---

### Task 5.2: Create implementation/components/slash-command.md

**File:** `implementation/components/slash-command.md`

**Content:** Complete 🦴 Slash Command reference

**Source:** Extract from `01-OFFICIAL-TERMINOLOGY.md`:
- Section 1.2 🦴 Slash Command (~70 lines)

---

### Task 5.3: Create implementation/components/skill.md

**File:** `implementation/components/skill.md`

**Content:** Complete 📚 Skill reference

**Source:** Extract from `01-OFFICIAL-TERMINOLOGY.md`:
- Section 1.3 📚 Skill (~60 lines)

---

### Task 5.4: Create implementation/components/hook.md

**File:** `implementation/components/hook.md`

**Content:** Complete 🪝 Hook reference

**Source:** Extract from `01-OFFICIAL-TERMINOLOGY.md`:
- Section 1.4 🪝 Hook (~60 lines)

---

## Phase 6: Migrate Architecture Content

### Task 6.1: Create implementation/architecture/01-user-layer.md

**File:** `implementation/architecture/01-user-layer.md`

**Content:** Layer 1: User Layer

**Source:** Extract from `02-LAYER-ARCHITECTURE.md`:
- "🙋‍♀️ Layer 1: User Layer" section (~40 lines)

---

### Task 6.2: Create implementation/architecture/02-main-agent-layer.md

**File:** `implementation/architecture/02-main-agent-layer.md`

**Content:** Layer 2: Main Agent Layer

**Source:** Extract from `02-LAYER-ARCHITECTURE.md`:
- "🐔 Layer 2: Main Agent Layer" section (~60 lines)

---

### Task 6.3: Create implementation/architecture/03-delegation-layer.md

**File:** `implementation/architecture/03-delegation-layer.md`

**Content:** Layer 3: Delegation Layer

**Source:** Extract from `02-LAYER-ARCHITECTURE.md`:
- "🔀 Layer 3: Delegation Layer" section (~50 lines)

---

### Task 6.4: Create implementation/architecture/04-execution-layer.md

**File:** `implementation/architecture/04-execution-layer.md`

**Content:** Layer 4: Execution Layer

**Source:** Extract from `02-LAYER-ARCHITECTURE.md`:
- "⚡ Layer 4: Execution Layer" section (~80 lines)

---

### Task 6.5: Create implementation/architecture/05-state-layer.md

**File:** `implementation/architecture/05-state-layer.md`

**Content:** Layer 5: State Layer

**Source:** Extract from `02-LAYER-ARCHITECTURE.md`:
- "💾 Layer 5: State Layer" section (~50 lines)

---

## Phase 7: Migrate Use Cases Content

### Task 7.1: Create guides/use-cases/01-multi-agent-research.md

**Source:** Extract "Use Case 1" from `05-USE-CASES.md` (~80 lines)

### Task 7.2: Create guides/use-cases/02-code-review-pipeline.md

**Source:** Extract "Use Case 2" from `05-USE-CASES.md` (~90 lines)

### Task 7.3: Create guides/use-cases/03-multi-locale-generation.md

**Source:** Extract "Use Case 3" from `05-USE-CASES.md` (~70 lines)

### Task 7.4: Create guides/use-cases/04-personal-assistant.md

**Source:** Extract "Use Case 4" from `05-USE-CASES.md` (~50 lines)

### Task 7.5: Create guides/use-cases/05-customer-support.md

**Source:** Extract "Use Case 5" from `05-USE-CASES.md` (~60 lines)

### Task 7.6: Create guides/use-cases/06-data-migration.md

**Source:** Extract "Use Case 6" from `05-USE-CASES.md` (~60 lines)

---

## Phase 8: Migrate Reference Content

### Task 8.1: Create reference/glossary.md

**File:** `reference/glossary.md`

**Content:** A-Z Glossary

**Source:** Extract from `07-MAPPING-GLOSSARY.md`:
- "Glossary: A-Z" section (~300 lines)
- Keep Anthropic Official Taxonomy
- Keep Master Mapping Table

---

### Task 8.2: Create reference/visual-standards.md

**File:** `reference/visual-standards.md`

**Content:** Emojis, Colors, Mermaid standards

**Source:** Extract from `01-OFFICIAL-TERMINOLOGY.md`:
- PART 2: VISUAL SYSTEM (~300 lines)
  - Section 3: ACTEUR + ACTION System
  - Section 4: Tools
  - Section 5: Status & Triggers
  - Section 6: Visual Standards
  - Section 7: Naming Conventions

---

### Task 8.3: Create reference/built-in-subagents.md

**File:** `reference/built-in-subagents.md`

**Content:** Built-in subagents reference

**Source:** Extract from `07-MAPPING-GLOSSARY.md`:
- "Built-in Subagents" section (~60 lines)

---

## Phase 9: Migrate Selection Guide

### Task 9.1: Create guides/selection-guide.md

**File:** `guides/selection-guide.md`

**Content:** Full selection guide (decision trees, matrices)

**Source:** Copy `06-SELECTION-GUIDE.md` with updated links

---

## Phase 10: Update Main README

### Task 10.1: Simplify README.md

**File:** `README.md`

**Changes:**
- Keep: Header, badges, "Why This Repo" section
- Update: Documentation Structure table with new paths
- Update: Repository Structure with new tree
- Remove: Duplicated content now in concepts/README.md
- Add: Quick Start pointing to concepts/README.md

---

## Phase 11: Cleanup

### Task 11.1: Delete old files

**Delete:**
- `00-OVERVIEW.md`
- `01-OFFICIAL-TERMINOLOGY.md`
- `02-LAYER-ARCHITECTURE.md`
- `03-WORKFLOWS.md`
- `04-AGENTS.md`
- `05-USE-CASES.md`
- `06-SELECTION-GUIDE.md`
- `07-MAPPING-GLOSSARY.md`

---

## Phase 12: Link Verification

### Task 12.1: Verify all internal links

**Command:** `grep -r "\](.*\.md" --include="*.md" | grep -v ".git"`

**Check:** All relative paths are correct

---

## Navigation Header Template

All new files should use this navigation header:

```markdown
<div align="center">

[🏠 Home](../../README.md) • [📚 Concepts](../README.md) • **Current File**

</div>

---
```

Adjust paths based on file depth.

---

## File Count Summary

| Directory | Files | Purpose |
|-----------|-------|---------|
| `/` | 1 | README.md |
| `concepts/` | 1 | Hub |
| `concepts/workflows/` | 8 | Index + 7 workflows |
| `concepts/agents/` | 3 | Index + 2 agents |
| `implementation/` | 1 | Hub |
| `implementation/components/` | 5 | Index + 4 components |
| `implementation/architecture/` | 6 | Index + 5 layers |
| `guides/` | 2 | Index + selection-guide |
| `guides/use-cases/` | 7 | Index + 6 use cases |
| `reference/` | 4 | Index + 3 references |
| **TOTAL** | **38** | — |

---

## Commit Strategy

1. **Phase 1-2:** `feat(docs): create directory structure and hub files`
2. **Phase 3:** `feat(docs): migrate workflows content to atomic files`
3. **Phase 4:** `feat(docs): migrate agents content to atomic files`
4. **Phase 5:** `feat(docs): migrate components content to atomic files`
5. **Phase 6:** `feat(docs): migrate architecture content to atomic files`
6. **Phase 7:** `feat(docs): migrate use-cases content to atomic files`
7. **Phase 8-9:** `feat(docs): migrate reference and selection guide`
8. **Phase 10:** `feat(docs): update main README with new structure`
9. **Phase 11-12:** `chore(docs): cleanup old files and verify links`

---

*Plan created: 2025-11-28*
*Total tasks: 38 files to create + cleanup*
