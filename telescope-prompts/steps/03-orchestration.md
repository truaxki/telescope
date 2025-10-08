# Phase 3: Orchestration Document Creation

> **Purpose:** Create orchestration document to coordinate multi-agent analysis

## Prerequisites

**Input from previous phases:**
- `project_name`
- `base_output_path`
- `active_agents` (from Phase 1)
- `focus_mode` (from Phase 1)
- `tech_stack` (from Phase 2)
- `date_str`

## Execution Steps

### Step 1: Create Orchestration Document

```python
def create_orchestration_doc(
    project_name: str,
    active_agents: list,
    focus_mode: str,
    tech_stack: list,
    emphasis_areas: str
) -> str:
    """Generate orchestration.md content."""

    # Agent specs mapping
    agent_specs = {
        1: {
            'name': 'Architecture Specialist',
            'domain': 'System architecture, design patterns, ADK integration'
        },
        2: {
            'name': 'Backend Specialist',
            'domain': 'APIs, databases, server logic, data flow'
        },
        3: {
            'name': 'Frontend Specialist',
            'domain': 'UI/UX, components, state management, user flows'
        },
        4: {
            'name': 'DevOps Specialist',
            'domain': 'Infrastructure, CI/CD, deployment, monitoring'
        },
        5: {
            'name': 'Quality Specialist',
            'domain': 'Testing, code quality, performance, best practices'
        }
    }

    return orchestration_template
```

### Step 2: Write Orchestration File

```python
from pathlib import Path

# Construct path
orchestration_path = Path(base_output_path) / "summaries" / "orchestration.md"

# Write orchestration document
with open(orchestration_path, 'w') as f:
    f.write(orchestration_content)
```

### Step 3: Orchestration Document Template

```markdown
# Telescope Analysis Orchestration

**Project:** {project_name}
**Analysis Mode:** {focus_mode}
**Date:** {date_str}
**Tech Stack:** {tech_stack_summary}
**Emphasis:** {emphasis_areas}

---

## Agent Assignments

### Active Agents: {len(active_agents)}

{for each active agent:}
#### Agent {n} - {agent_name}

**Status:** 🔄 Pending
**Domain:** {domain}
**Focus Areas:**
- {area_1}
- {area_2}
- {area_3}

**Deliverables:**
- `agent-{n}-summary.md` - Detailed findings
- Pain points identified
- Recommendations

**Progress:**
- [ ] Analysis started
- [ ] Codebase scanned
- [ ] Findings documented
- [ ] Summary created

---

{end for}

## Inactive Agents

{for each inactive agent:}
**Agent {n} - {agent_name}:** ⏸️ Skipped (not needed for {focus_mode} analysis)
{end for}

---

## Coordination Notes

### Analysis Scope
{focus_mode_description}

### Priority Areas
1. {priority_1}
2. {priority_2}
3. {priority_3}

### Expected Output
Each agent should produce:
- Comprehensive summary of their domain
- Specific pain points with severity ratings
- Actionable recommendations with effort estimates

---

## Progress Tracking

**Overall Status:** 🔄 In Progress

| Agent | Status | Completion |
|-------|--------|------------|
{for each active agent:}
| Agent {n} | 🔄 Pending | 0% |
{end for}

**Started:** {timestamp}
**Estimated Duration:** {estimate based on agent count}

---

## Next Steps

1. Launch all active agents in parallel
2. Each agent loads relevant prompts and context
3. Agents perform independent analysis
4. Agents write summaries to summaries/
5. Synthesis phase collects and integrates findings
```

## Output Variables

**Phase 3 produces:**

```yaml
orchestration_file: "ai_docs/documentation/{project}/summaries/orchestration.md"
orchestration_created: true
ready_for_agents: true
```

## User Communication

```markdown
## Telescope Orchestration Document Created ✅

**Orchestration File:** {orchestration_path}
**Active Agents:** {agent_count}
**Analysis Scope:** {focus_mode}

### Agent Lineup:
{for each active agent:}
- Agent {n} ({agent_name}): {focus_summary}
{end for}

**Coordination ready** - All agents have clear assignments and deliverables.

---

Next: Phase 4 - Multi-Agent Execution
```

## Document Purpose

The orchestration document serves as:

1. **Central coordination** - Single source of truth for analysis scope
2. **Agent instruction** - Each agent knows what to analyze
3. **Progress tracking** - Real-time status updates
4. **Context sharing** - All agents understand the overall mission

## Next Phase

Load `steps/04-agent-execution.md` and begin parallel agent execution
