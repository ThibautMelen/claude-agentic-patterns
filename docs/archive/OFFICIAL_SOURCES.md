# Official Anthropic Sources Reference

**Purpose:** Comprehensive list of official Anthropic documentation sources for agentic patterns.

**Last Updated:** 2025-11-28

---

## Primary Sources

### 1. Building Effective Agents (December 2024)

**URL:** https://www.anthropic.com/research/building-effective-agents

**Status:** 🟢 Active (as of Nov 2024)

**Content:**
- Defines all 7 core patterns (Building Block + 5 Workflows + Agents)
- Official terminology and definitions
- Design philosophy ("workflows first")
- Best practices and warnings

**Key Sections:**
- Introduction to agentic systems
- Augmented LLM (Building Block)
- Workflow patterns (Prompt Chaining, Routing, Parallelization, Orchestrator-Workers, Evaluator-Optimizer)
- Autonomous Agents
- When to use workflows vs agents
- Agent-Computer Interface (ACI) design

**How to Scrape:**
```bash
# Using Firecrawl MCP
firecrawl_scrape --url "https://www.anthropic.com/research/building-effective-agents" \
  --formats markdown,html \
  --extract-sections true
```

**Archive:**
- Web Archive: https://web.archive.org/web/*/anthropic.com/research/building-effective-agents
- Local backup recommended: Yes

---

### 2. Claude Code Documentation

**URL:** https://docs.anthropic.com/en/docs/claude-code

**Status:** 🟢 Active

**Content:**
- Claude Code CLI overview
- Component definitions (Subagents, Skills, Commands, Hooks)
- Built-in tools (Task, AskUserQuestion, etc.)
- Setup and configuration

**Relevant Subsections:**

#### 2a. Components
**URL:** https://docs.anthropic.com/en/docs/claude-code/components

**Content:**
- Subagent definition and usage
- Slash Command creation
- Skill system (progressive loading)
- Hooks for event automation

#### 2b. Built-in Tools
**URL:** https://docs.anthropic.com/en/docs/claude-code/tools

**Content:**
- Task tool (spawning subagents)
- AskUserQuestion (human-in-the-loop)
- File operations
- MCP integration

**How to Scrape:**
```bash
# Scrape main page + all subpages
firecrawl_map --url "https://docs.anthropic.com/en/docs/claude-code" \
  --include "/claude-code/*"

# Then batch scrape relevant pages
firecrawl_batch_scrape --urls @claude_code_urls.txt
```

---

### 3. Anthropic Cookbook

**URL:** https://github.com/anthropics/anthropic-cookbook

**Status:** 🟢 Active (regularly updated)

**Content:**
- Code examples and notebooks
- Implementation patterns
- Best practices
- Real-world use cases

**Relevant Sections:**

#### 3a. Agent Examples
**Path:** `/anthropic-cookbook/agents/`

**Content:**
- Autonomous agent implementations
- Tool use examples
- Multi-step workflow examples

#### 3b. Tool Use
**Path:** `/anthropic-cookbook/tool_use/`

**Content:**
- Tool definition examples
- Function calling patterns
- Error handling

**How to Access:**
```bash
# Clone repository
git clone https://github.com/anthropics/anthropic-cookbook.git

# List all agent examples
find anthropic-cookbook -path "*/agents/*" -name "*.ipynb"

# List all tool use examples
find anthropic-cookbook -path "*/tool_use/*" -name "*.ipynb"
```

**Relevant Files to Track:**
```
anthropic-cookbook/
├── agents/
│   ├── autonomous_agent_example.ipynb
│   ├── workflow_examples.ipynb
│   └── tool_orchestration.ipynb
├── tool_use/
│   ├── tool_definition.ipynb
│   ├── function_calling.ipynb
│   └── error_handling.ipynb
└── patterns/
    ├── prompt_chaining.ipynb
    ├── routing.ipynb
    └── parallelization.ipynb
```

---

## Secondary Sources

### 4. Anthropic API Documentation

**URL:** https://docs.anthropic.com/en/api/

**Relevance:** Medium (API-level details)

**Content:**
- Messages API
- Tool use API specification
- Streaming responses
- Token limits and pricing

---

### 5. Tool Use Guide

**URL:** https://docs.anthropic.com/en/docs/build-with-claude/tool-use

**Relevance:** High (tool design best practices)

**Content:**
- How to define tools
- Best practices for tool descriptions
- Error handling in tools
- Examples of good vs bad tool definitions

**How to Scrape:**
```bash
firecrawl_scrape --url "https://docs.anthropic.com/en/docs/build-with-claude/tool-use" \
  --formats markdown
```

---

### 6. Prompt Engineering Guide

**URL:** https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering

**Relevance:** Medium (foundation concepts)

**Content:**
- Prompt design principles
- Few-shot examples
- Chain-of-thought prompting
- System prompts

---

### 7. Anthropic Blog

**URL:** https://www.anthropic.com/news

**Relevance:** Medium (announcements and updates)

**Content:**
- New feature announcements
- Research updates
- Case studies

**Monitoring Strategy:**
- Check monthly for new articles on agents/tools
- Subscribe to RSS if available
- Set up Google Alerts for "Anthropic agents"

---

## How to Keep Documentation Updated

### 1. Automated Monitoring

**Script to check for updates:**

```bash
#!/bin/bash
# check_anthropic_updates.sh

URLS=(
  "https://www.anthropic.com/research/building-effective-agents"
  "https://docs.anthropic.com/en/docs/claude-code"
  "https://docs.anthropic.com/en/docs/build-with-claude/tool-use"
)

for url in "${URLS[@]}"; do
  echo "Checking: $url"

  # Get current content hash
  current_hash=$(curl -s "$url" | sha256sum)

  # Compare with stored hash
  stored_hash=$(cat "hashes/$(echo $url | md5sum | cut -d' ' -f1).txt" 2>/dev/null)

  if [ "$current_hash" != "$stored_hash" ]; then
    echo "⚠️ CHANGED: $url"
    echo "$current_hash" > "hashes/$(echo $url | md5sum | cut -d' ' -f1).txt"
  else
    echo "✅ No changes"
  fi
done
```

**Run monthly:**
```bash
# Add to crontab
0 9 1 * * /path/to/check_anthropic_updates.sh
```

---

### 2. Manual Review Checklist

**Quarterly review (every 3 months):**

- [ ] Read latest "Building Effective Agents" article
- [ ] Check Claude Code docs for new components
- [ ] Review Anthropic Cookbook for new examples
- [ ] Check blog for agent-related announcements
- [ ] Update pattern definitions if changed
- [ ] Update code examples if APIs changed
- [ ] Document any new patterns discovered

---

### 3. Version Tracking

**Maintain in `/reference/version-history.md`:**

```markdown
## 2024-12-01: Building Effective Agents Published

**Source:** https://www.anthropic.com/research/building-effective-agents

**Changes:**
- Officially defined 7 core patterns
- Introduced "workflows first" philosophy
- Defined Agent-Computer Interface (ACI) concept

**Impact on our docs:** Major - aligned all terminology

---

## 2025-01-15: Claude Code v2.0 Released

**Source:** https://docs.anthropic.com/en/docs/claude-code

**Changes:**
- New Hooks component added
- Improved Task tool with better error handling
- Progressive Skills now support dependencies

**Impact on our docs:** Minor - updated component descriptions
```

---

## Scraping Best Practices

### Using Firecrawl MCP

**1. Single page scrape:**
```typescript
// Via MCP plugin
const result = await mcp.firecrawl.scrape({
  url: "https://www.anthropic.com/research/building-effective-agents",
  formats: ["markdown", "html"],
  onlyMainContent: true
});
```

**2. Map entire site section:**
```typescript
const siteMap = await mcp.firecrawl.map({
  url: "https://docs.anthropic.com/en/docs/claude-code",
  includeSubdomains: false,
  search: "components OR tools OR patterns"
});
```

**3. Batch scrape multiple pages:**
```typescript
const urls = [
  "https://docs.anthropic.com/en/docs/claude-code/components",
  "https://docs.anthropic.com/en/docs/claude-code/tools",
  "https://docs.anthropic.com/en/docs/claude-code/architecture"
];

const results = await mcp.firecrawl.batchScrape({
  urls: urls,
  formats: ["markdown"]
});
```

**4. Extract structured data:**
```typescript
const schema = {
  type: "object",
  properties: {
    pattern_name: { type: "string" },
    definition: { type: "string" },
    use_cases: { type: "array", items: { type: "string" } },
    examples: { type: "array", items: { type: "object" } }
  }
};

const extracted = await mcp.firecrawl.extract({
  url: "https://www.anthropic.com/research/building-effective-agents",
  schema: schema
});
```

---

### Using GitHub API for Cookbook

**Get latest commits to agent examples:**

```bash
# List recent commits to agents directory
curl -H "Accept: application/vnd.github.v3+json" \
  "https://api.github.com/repos/anthropics/anthropic-cookbook/commits?path=agents"

# Get specific file content
curl -H "Accept: application/vnd.github.v3.raw" \
  "https://api.github.com/repos/anthropics/anthropic-cookbook/contents/agents/autonomous_agent_example.ipynb"
```

**Watch for updates:**
```bash
# Subscribe to repository notifications
gh repo watch anthropics/anthropic-cookbook

# Or poll for changes
gh api repos/anthropics/anthropic-cookbook/commits \
  --jq '.[0].commit.message'
```

---

## Citation Format

When referencing official sources in documentation:

### For Articles/Blog Posts

```markdown
> **From "Building Effective Agents" (Anthropic, December 2024):**
>
> "[exact quote]"
>
> **Source:** https://www.anthropic.com/research/building-effective-agents
```

### For API Documentation

```markdown
> **From Claude Code Documentation (Anthropic, 2025):**
>
> "[exact quote]"
>
> **Source:** https://docs.anthropic.com/en/docs/claude-code/[specific-section]
```

### For Code Examples

```markdown
> **From Anthropic Cookbook:**
>
> Implementation: [link to specific notebook]
>
> **Source:** https://github.com/anthropics/anthropic-cookbook/blob/main/[path]
```

---

## Contact Points

### Official Channels

**Documentation Issues:**
- GitHub: https://github.com/anthropics/anthropic-cookbook/issues
- Email: docs@anthropic.com (if available)

**API Questions:**
- Support: https://support.anthropic.com
- Discord: https://discord.gg/anthropic (if available)

**Claude Code Specific:**
- Documentation: https://docs.anthropic.com/en/docs/claude-code
- GitHub Discussions: https://github.com/anthropics/anthropic-tools/discussions

---

## Future Sources to Monitor

### Potential Upcoming Documentation

- **Agent SDK Documentation** (mentioned in current docs)
  - Expected URL: https://docs.anthropic.com/en/docs/agent-sdk
  - What to watch for: Programmatic agent orchestration APIs

- **Advanced Patterns** (if released)
  - Look for: Multi-agent collaboration patterns
  - Look for: State management best practices
  - Look for: Production deployment guides

- **Case Studies** (as they're published)
  - Where: https://www.anthropic.com/news
  - What: Real-world agent implementations

---

## Archive Strategy

### Local Backups

**What to backup:**
```
backups/
├── 2024-12/
│   ├── building-effective-agents.md
│   ├── claude-code-docs.md
│   └── cookbook-snapshot/
├── 2025-01/
│   └── ...
└── current/
    └── latest-snapshot.md
```

**Backup script:**
```bash
#!/bin/bash
# backup_official_docs.sh

DATE=$(date +%Y-%m)
BACKUP_DIR="backups/$DATE"
mkdir -p "$BACKUP_DIR"

# Backup main article
curl -s "https://www.anthropic.com/research/building-effective-agents" \
  > "$BACKUP_DIR/building-effective-agents.html"

# Convert to markdown
pandoc "$BACKUP_DIR/building-effective-agents.html" \
  -o "$BACKUP_DIR/building-effective-agents.md"

echo "✅ Backup complete: $BACKUP_DIR"
```

---

## Research Workflow

**When updating this repository based on official sources:**

1. **Identify what changed**
   - Run update check script
   - Read new/updated content
   - Note any terminology changes

2. **Validate impact**
   - Does this affect our pattern definitions?
   - Do code examples need updates?
   - Are there new patterns to document?

3. **Update documentation**
   - Add official quotes/citations
   - Update definitions if changed
   - Add new patterns if introduced
   - Update version history

4. **Cross-reference**
   - Ensure consistency across all docs
   - Update links and references
   - Validate examples still work

5. **Document changes**
   - Update CHANGELOG
   - Note in version-history.md
   - Update "Last verified" dates

---

## Quick Reference: Where to Find What

| Need | Source | URL |
|------|--------|-----|
| **Pattern definitions** | Building Effective Agents | anthropic.com/research/building-effective-agents |
| **Component specs** | Claude Code Docs | docs.anthropic.com/en/docs/claude-code/components |
| **Code examples** | Anthropic Cookbook | github.com/anthropics/anthropic-cookbook |
| **Tool design** | Tool Use Guide | docs.anthropic.com/.../tool-use |
| **API details** | API Documentation | docs.anthropic.com/en/api |
| **Announcements** | Anthropic Blog | anthropic.com/news |

---

**Last Verified:** 2025-11-28
**Next Review Due:** 2025-02-28

---

<div align="center">

**━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━**

[🏠 Home](./README.md) • [📚 Research Report](./RESEARCH_REPORT_ANTHROPIC_OFFICIAL.md)

</div>
