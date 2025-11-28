# Documentation Verification Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development to execute this plan task-by-task with code review after each.

**Goal:** Verify all documentation follows official terminology, emoji taxonomy, and visual standards.

**Architecture:** 4-phase audit using parallel subagents for independent checks, with fixes applied immediately after each finding.

**Tech Stack:** Grep, Glob, Read, Edit tools. No external dependencies.

---

## Phase 1: Terminology Audit

### Task 1.1: Find Unofficial Terms

**Files to check:** All `*.md` files in repository

**Step 1: Search for banned terms**

```bash
# Terms that should NOT exist
grep -rn "sub-agent" --include="*.md"           # Should be "subagent"
grep -rn "Sub Agent" --include="*.md"           # Should be "Subagent"
grep -rn "Lead Agent" --include="*.md"          # Should be "Main Agent"
grep -rn "Parent Agent" --include="*.md"        # Should be "Main Agent"
grep -rn "Child Agent" --include="*.md"         # Should be "Subagent"
grep -rn "Subagent Orchestration" --include="*.md"  # Should be "Orchestrator-Workers"
```

**Step 2: Report findings**

Expected: Zero matches (all fixed in previous session)

**Step 3: If issues found, fix immediately**

Replace with correct terms per glossary.md

---

### Task 1.2: Verify Pattern Names

**Files to check:** All pattern documentation

**Step 1: Verify correct pattern names used**

```bash
# These SHOULD exist (correct terms)
grep -rn "Orchestrator-Workers" --include="*.md"
grep -rn "Evaluator-Optimizer" --include="*.md"
grep -rn "Prompt Chaining" --include="*.md"
grep -rn "Parallelization" --include="*.md"
grep -rn "Routing" --include="*.md"
grep -rn "Direct Execution" --include="*.md"
grep -rn "Autonomous Agents" --include="*.md"
```

**Step 2: Verify NO incorrect variants**

```bash
# These should NOT exist
grep -rn "Chain Prompting" --include="*.md"     # Wrong name
grep -rn "Router Pattern" --include="*.md"       # Wrong name
grep -rn "Parallel Execution" --include="*.md"   # Wrong name (as pattern)
grep -rn "Evaluation Loop" --include="*.md"      # Wrong name
```

**Step 3: Report and fix**

---

### Task 1.3: Verify Task Tool = 🪺 Clarity

**Files to check:** `reference/visual-standards.md`, `reference/glossary.md`, `implementation/components/subagent.md`

**Step 1: Verify 🪺 is clearly linked to Task tool**

Search for:
- "🪺" mentions should reference "Task tool"
- "Task tool" mentions should reference "🪺"

**Step 2: Add clarification if missing**

Ensure this mapping is explicit:
```
🪺 spawn = Task tool (official name)
```

---

## Phase 2: Emoji Consistency Audit

### Task 2.1: Verify Actor Emojis

**Step 1: Check 🐔 usage**

```bash
grep -rn "🐔" --include="*.md" | head -50
```

Verify ALL occurrences are:
- "🐔 Main Agent" OR
- "🐔" in ACTEUR+ACTION combos (🐔💭, 🐔🪺, etc.)

**Step 2: Check 🐦 usage**

```bash
grep -rn "🐦" --include="*.md" | head -50
```

Verify ALL occurrences are:
- "🐦 Subagent" OR
- "🐦" in ACTEUR+ACTION combos (🐦⚡, 🐦📤, etc.)

**Step 3: Check 🐉 usage**

```bash
grep -rn "🐉" --include="*.md"
```

Verify ALL occurrences are:
- "🐉 Autonomous Agents" (NEVER just "🐉 Agents")

---

### Task 2.2: Verify Pattern Emojis Not Mixed with Actors

**Step 1: Find forbidden combinations**

```bash
# These should NOT exist (mixing actor + pattern emoji)
grep -rn "🐔🦑\|🦑🐔" --include="*.md"
grep -rn "🐦🦑\|🦑🐦" --include="*.md"
grep -rn "🐔🐉\|🐉🐔" --include="*.md"
grep -rn "🐦🐉\|🐉🐦" --include="*.md"
```

Expected: Zero matches

**Step 2: Fix any violations**

Replace with correct usage:
- Actor emoji + Action emoji = OK (🐔💭)
- Actor emoji + Pattern emoji = WRONG (🐔🦑)

---

### Task 2.3: Verify ACTEUR+ACTION Combinations

**Step 1: List all emoji combinations in docs**

```bash
grep -rnoE "🐔[💭🚦🪺⚡👀✏️✅❓🔀🌀📋🔄▶️📤📥]" --include="*.md" | sort | uniq -c
grep -rnoE "🐦[💭⚡👀✏️📤✅💤]" --include="*.md" | sort | uniq -c
grep -rnoE "🙋‍♀️[📥✅❓]|💁‍♀️[📤]|🙆‍♀️[✅❓]" --include="*.md" | sort | uniq -c
```

**Step 2: Verify all combinations are valid per visual-standards.md**

Cross-reference with Combinations Matrix in visual-standards.md

---

## Phase 3: Cross-Reference Audit

### Task 3.1: Verify Glossary Coverage

**Step 1: Extract all defined terms from glossary**

```bash
grep -oE "^\*\*[^*]+\*\*" reference/glossary.md | sort
```

**Step 2: Find undefined terms in main docs**

Check that key terms used in docs appear in glossary:
- Main Agent
- Subagent
- Orchestrator-Workers
- All pattern names
- All component names

**Step 3: Add missing definitions**

---

### Task 3.2: Verify Visual Standards Completeness

**Step 1: Check visual-standards.md has all emojis**

Verify these tables are complete:
- Acteurs (WHO) table
- Actions (WHAT) table
- Pattern Emoji Reference table

**Step 2: Check for undocumented emojis in use**

```bash
# Find all emojis used in docs
grep -rnoE "[🐔🐦🐉🦑🛤️⛓️🚦🩻🏎️🧙🚂🧬🖥️📚🎛️🪝🦴🔧🔌💭📥📤⚡✅❌]" --include="*.md" | cut -d: -f3 | sort | uniq -c | sort -rn
```

Cross-reference with visual-standards.md

---

### Task 3.3: Verify Internal Links

**Step 1: Extract all markdown links**

```bash
grep -rnoE "\[([^\]]+)\]\(([^)]+)\)" --include="*.md" | grep -v "http"
```

**Step 2: Verify each relative link resolves**

For each link like `[text](path.md)`:
- Check file exists
- Check anchor exists if `#anchor` used

**Step 3: Fix broken links**

---

## Phase 4: Final Verification

### Task 4.1: Run Full Audit Summary

**Step 1: Count all issues by category**

```
Terminology issues: X
Emoji issues: X
Cross-reference issues: X
```

**Step 2: Generate verification report**

Save to: `docs/reports/2025-11-28-verification-report.md`

**Step 3: Confirm all checks pass**

Success criteria:
- Zero terminology violations
- Zero emoji violations
- Zero broken links
- 100% glossary coverage

---

## Execution Notes

**Subagent assignments:**
- Task 1.1-1.3: Terminology subagent (Explore type)
- Task 2.1-2.3: Emoji subagent (Explore type)
- Task 3.1-3.3: Cross-reference subagent (Explore type)
- Task 4.1: Summary subagent (general-purpose)

**After each task:** Code review to verify fixes are correct

**If issues found:** Fix immediately before next task

---

<div align="center">

**Plan Version:** 1.0 | **Created:** 2025-11-28

</div>
