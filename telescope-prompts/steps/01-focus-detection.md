# Phase 1: Focus Detection & Agent Assignment

> **Purpose:** Determine analysis mode and assign appropriate agents

## Prerequisites

**Input from Phase 0:**
- `target_path`
- `project_name`
- User command

**Must load:**
- `config/focus-modes.md`

## Execution Steps

### Step 1: Detect Focus Keywords

```python
def detect_focus_mode(command: str) -> str:
    """Detect focus mode from user command."""
    command_lower = command.lower()

    # Check for "focus on" phrase
    if "focus on" not in command_lower:
        return "full_stack"

    # Extract what comes after "focus on"
    focus_phrase = command_lower.split("focus on")[1].strip()

    # Match keywords (see config/focus-modes.md for full list)
    keyword_map = {
        'adk|agent': 'adk_architecture',
        'database|schema': 'database',
        'performance|optimization': 'performance',
        'security|vulnerability': 'security',
        'api|endpoint': 'api_design',
        'frontend|ui|component': 'frontend',
        'devops|deployment|ci': 'devops',
        'testing|test|coverage': 'testing',
        'real-time|websocket|sync': 'real_time',
    }

    for keywords, mode in keyword_map.items():
        if any(kw in focus_phrase for kw in keywords.split('|')):
            return mode

    return "full_stack"
```

### Step 2: Load Focus Configuration

```python
# Reference config/focus-modes.md for agent assignments
focus_mode_config = {
    'full_stack': {
        'agents': [1, 2, 3, 4, 5],
        'depth': 'comprehensive',
        'emphasis': 'complete system analysis'
    },
    'adk_architecture': {
        'agents': [1, 2],
        'depth': 'comprehensive',
        'emphasis': 'ADK patterns, agent hierarchies, session management'
    },
    'database': {
        'agents': [2],
        'depth': 'deep_dive',
        'emphasis': 'schema design, query patterns, migrations'
    },
    'performance': {
        'agents': [2, 5],
        'depth': 'comprehensive',
        'emphasis': 'bottlenecks, optimization, scalability'
    },
    'security': {
        'agents': [2, 4],
        'depth': 'comprehensive',
        'emphasis': 'vulnerabilities, auth, data protection'
    },
    'api_design': {
        'agents': [2, 3],
        'depth': 'comprehensive',
        'emphasis': 'API contracts, error handling, versioning'
    },
    'frontend': {
        'agents': [3],
        'depth': 'deep_dive',
        'emphasis': 'component architecture, state, UX'
    },
    'devops': {
        'agents': [4],
        'depth': 'deep_dive',
        'emphasis': 'CI/CD, infrastructure, deployment'
    },
    'testing': {
        'agents': [5],
        'depth': 'deep_dive',
        'emphasis': 'test coverage, strategies, quality'
    },
    'real_time': {
        'agents': [1, 2, 3],
        'depth': 'comprehensive',
        'emphasis': 'real-time sync, WebSocket, state updates'
    },
}

config = focus_mode_config[detected_mode]
```

### Step 3: Assign Agents

```python
# Agent specializations
agent_specs = {
    1: "architecture",
    2: "backend",
    3: "frontend",
    4: "devops",
    5: "quality"
}

active_agents = config['agents']
inactive_agents = [n for n in [1,2,3,4,5] if n not in active_agents]
```

## Output Variables

**Phase 1 produces:**

```yaml
focus_mode: "detected mode name"
active_agents: [1, 2, 3, 4, 5]  # or subset
analysis_depth: "comprehensive | deep_dive | high_level"
emphasis_areas: "what to emphasize"
```

## User Communication

```markdown
## Telescope Focus Configuration ✅

**Analysis Mode:** {focus_mode}
**Active Agents:** {len(active_agents)}
**Analysis Depth:** {analysis_depth}
**Emphasis Areas:** {emphasis_areas}

### Agent Assignments:

**Agent 1 - Architecture Specialist**
- Status: {✅ Active | ⏸️ Inactive}
- Focus: {specific areas if active}

**Agent 2 - Backend Specialist**
- Status: {✅ Active | ⏸️ Inactive}
- Focus: {specific areas if active}

**Agent 3 - Frontend Specialist**
- Status: {✅ Active | ⏸️ Inactive}
- Focus: {specific areas if active}

**Agent 4 - DevOps Specialist**
- Status: {✅ Active | ⏸️ Inactive}
- Focus: {specific areas if active}

**Agent 5 - Quality Specialist**
- Status: {✅ Active | ⏸️ Inactive}
- Focus: {specific areas if active}

---

Next: Phase 2 - Context Scan
```

## Next Phase

Load `steps/02-context-scan.md` and continue
