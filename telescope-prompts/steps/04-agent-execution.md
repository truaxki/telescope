# Phase 4: Multi-Agent Execution

> **Purpose:** Launch specialized agents in parallel to analyze the codebase

## Prerequisites

**Input from previous phases:**
- `target_path`
- `active_agents`
- `orchestration_file`
- `base_output_path`
- `focus_mode`

**Required files:**
- `agents/agent-1-architecture.md`
- `agents/agent-2-backend.md`
- `agents/agent-3-frontend.md`
- `agents/agent-4-devops.md`
- `agents/agent-5-quality.md`

## Execution Steps

### Step 1: Prepare Agent Context

```python
def prepare_agent_context(agent_num: int) -> dict:
    """Prepare context for each agent."""

    # Files each agent must load
    common_files = [
        "orchestrator.md",
        "summaries/orchestration.md",
        f"agents/agent-{agent_num}-{agent_specs[agent_num]}.md"
    ]

    # Additional context based on agent
    focus_files = {
        1: ["config/architecture-patterns.md"],
        2: ["config/backend-checklist.md"],
        3: ["config/frontend-checklist.md"],
        4: ["config/devops-checklist.md"],
        5: ["config/quality-metrics.md"]
    }

    return {
        'agent_num': agent_num,
        'target_path': target_path,
        'output_path': f"{base_output_path}/summaries/agent-{agent_num}-summary.md",
        'required_files': common_files + focus_files.get(agent_num, []),
        'focus_mode': focus_mode
    }
```

### Step 2: Launch Agents in Parallel

```python
# Agent launching pseudo-code
for agent_num in active_agents:
    context = prepare_agent_context(agent_num)

    # Each agent receives:
    agent_params = {
        'target_path': context['target_path'],
        'output_file': context['output_path'],
        'focus_mode': focus_mode,
        'load_prompts': context['required_files']
    }

    # Launch agent (implementation specific to runtime)
    launch_agent(agent_num, agent_params)
```

### Step 3: Agent Execution Flow

**Each agent independently performs:**

```markdown
1. Load Required Prompts
   - Read orchestrator.md for overall guidance
   - Read orchestration.md for specific assignment
   - Read agent-specific prompt file
   - Read any focus-specific config files

2. Analyze Target Codebase
   - Navigate to target_path
   - Scan relevant directories per specialization
   - Read key files in their domain
   - Identify patterns, issues, opportunities

3. Document Findings
   - Create structured summary
   - List pain points with severity
   - Provide recommendations with effort estimates
   - Include code examples where relevant

4. Write Summary File
   - Write to assigned output path
   - Follow summary template format
   - Signal completion by file creation
```

### Step 4: Agent Parameters Reference

**Agent 1 - Architecture:**
```yaml
focus: System design, patterns, structure
scan_dirs: ["/src", "/lib", "/app", "/agents"]
key_files: ["architecture docs", "config files", "entry points"]
deliverable: "agent-1-summary.md"
```

**Agent 2 - Backend:**
```yaml
focus: APIs, database, server logic
scan_dirs: ["/api", "/server", "/functions", "/database"]
key_files: ["API routes", "models", "schema", "migrations"]
deliverable: "agent-2-summary.md"
```

**Agent 3 - Frontend:**
```yaml
focus: UI, components, user experience
scan_dirs: ["/components", "/pages", "/app", "/public"]
key_files: ["components", "styles", "layouts", "routes"]
deliverable: "agent-3-summary.md"
```

**Agent 4 - DevOps:**
```yaml
focus: Infrastructure, deployment, CI/CD
scan_dirs: ["/.github", "/deploy", "/config"]
key_files: ["workflows", "Dockerfile", "deploy configs"]
deliverable: "agent-4-summary.md"
```

**Agent 5 - Quality:**
```yaml
focus: Testing, performance, code quality
scan_dirs: ["/test", "/tests", "/__tests__"]
key_files: ["test files", "config", "coverage reports"]
deliverable: "agent-5-summary.md"
```

### Step 5: Agent Completion Signal

**Agents signal completion by:**

```python
# Agent completion checklist
completion_requirements = {
    'file_created': f"agent-{n}-summary.md exists",
    'file_not_empty': "file size > 0 bytes",
    'valid_markdown': "file is valid markdown",
    'required_sections': [
        "Executive Summary",
        "Key Findings",
        "Pain Points",
        "Recommendations"
    ]
}

# Orchestrator checks for completion
def check_agent_completion(agent_num: int) -> bool:
    summary_path = f"{base_output_path}/summaries/agent-{agent_num}-summary.md"

    if not os.path.exists(summary_path):
        return False

    if os.path.getsize(summary_path) == 0:
        return False

    # Agent has completed
    return True
```

## Agent Summary Template

**Each agent follows this structure:**

```markdown
# Agent {n} Analysis - {Specialization}

**Project:** {project_name}
**Focus Mode:** {focus_mode}
**Analysis Date:** {date_str}

---

## Executive Summary

{2-3 paragraph overview of findings}

---

## Key Findings

### Strengths
- {strength_1}
- {strength_2}

### Areas for Improvement
- {improvement_1}
- {improvement_2}

---

## Pain Points

### High Priority
1. **{pain_point_title}**
   - Severity: High
   - Impact: {description}
   - Location: {file_paths}

### Medium Priority
{...}

### Low Priority
{...}

---

## Recommendations

1. **{recommendation_title}**
   - Priority: High/Medium/Low
   - Effort: High/Medium/Low
   - Impact: {expected_impact}
   - Implementation: {how_to}

---

## Code Examples

{relevant code snippets with analysis}

---

**Analysis completed by Agent {n} - {agent_name}**
```

## User Communication

```markdown
## Telescope Multi-Agent Analysis Launched ✅

**Active Agents:** {agent_count}
**Target:** {project_name}
**Mode:** {focus_mode}

### Agents in Progress:
{for each agent:}
- 🔄 Agent {n} ({name}): Analyzing {domain}...
{end for}

**Parallel execution initiated** - Agents are independently analyzing the codebase.

Monitoring for completion signals...

---

Next: Phase 5 - Synthesis (when all agents complete)
```

## Next Phase

When all active agents have completed their summaries:
1. Verify all expected summary files exist
2. Load `steps/05-synthesis.md`
3. Begin synthesis phase
