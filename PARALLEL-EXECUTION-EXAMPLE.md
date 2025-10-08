# Telescope Parallel Execution Example

> **How to properly execute Telescope with true multi-agent parallelism**

## The Problem with Sequential Simulation

❌ **What NOT to do:**
```
Single AI Assistant tries to:
1. Load Agent 1 prompt (5,000 lines)
2. Analyze as Agent 1
3. Load Agent 2 prompt (5,000 lines)
4. Analyze as Agent 2
...
Result: Context overflow, poor quality, defeats the purpose
```

## The Correct Parallel Approach

✅ **What TO do:**

### Step 1: Coordinator Creates Orchestration

**Coordinator Agent (Window/Conversation 1):**
```
1. Loads orchestrator.md
2. Executes Phases 0-3
3. Creates: ai_docs/documentation/[project]/summaries/[DATE]-orchestration.md
4. This document contains ALL context agents need
```

### Step 2: Launch Parallel Agents

**Open 5 SEPARATE windows/conversations simultaneously:**

**Window 2 - Agent 1 (Architecture):**
```
User: Load these files and analyze:
1. ai_docs/documentation/adk-walkthrough-youtube/summaries/2025-10-08-orchestration.md
2. telescope-prompts/agents/agent-1-architecture.md
3. telescope-prompts/focus-modes/adk-architecture.md
4. telescope-prompts/config/output-structure.md

Then analyze the codebase at: adk-walkthrough-youtube/
Focus on: architecture, agent hierarchies, patterns
Output to: ai_docs/documentation/adk-walkthrough-youtube/summaries/2025-10-08-agent-1-architecture.md
```

**Window 3 - Agent 2 (Backend):**
```
User: Load these files and analyze:
1. ai_docs/documentation/adk-walkthrough-youtube/summaries/2025-10-08-orchestration.md
2. telescope-prompts/agents/agent-2-backend.md
3. telescope-prompts/focus-modes/adk-architecture.md
4. telescope-prompts/config/output-structure.md

Then analyze the codebase at: adk-walkthrough-youtube/
Focus on: backend, tools, APIs, state management
Output to: ai_docs/documentation/adk-walkthrough-youtube/summaries/2025-10-08-agent-2-backend.md
```

**Window 4 - Agent 3 (Frontend):** [If active]
**Window 5 - Agent 4 (DevOps):** [If active]
**Window 6 - Agent 5 (Quality):** [If active]

### Step 3: Agents Work Independently

**Each agent in their separate conversation:**
- Loads ONLY their 3-4 files (~1,000 lines)
- Has full context to analyze deeply
- Produces 2,000-5,000 line analysis
- Writes to their specific output file
- No coordination needed

### Step 4: Synthesis

**Window 7 - Synthesis Agent (after all complete):**
```
User: Load these files and synthesize:
1. telescope-prompts/agents/synthesis-agent.md
2. telescope-prompts/config/output-structure.md
3. ai_docs/documentation/adk-walkthrough-youtube/summaries/2025-10-08-agent-1-architecture.md
4. ai_docs/documentation/adk-walkthrough-youtube/summaries/2025-10-08-agent-2-backend.md
[... all other agent summaries ...]

Create master documentation at:
- ai_docs/documentation/adk-walkthrough-youtube/2025-10-08-master-documentation.md
- ai_docs/documentation/adk-walkthrough-youtube/2025-10-08-pain-points.md
- ai_docs/documentation/adk-walkthrough-youtube/2025-10-08-recommendations.md
```

## Real Example: ADK Walkthrough Analysis

### What the Orchestration Document Provides

The orchestration document (created in Phase 3) gives each agent:

```markdown
# Telescope Orchestration - ADK Walkthrough YouTube

**Project:** adk-walkthrough-youtube
**Target Path:** adk-walkthrough-youtube/
**Focus Mode:** adk_architecture
**Your Assignment:** Agent 1 - Architecture

## Your Focus Areas:
- Agent hierarchy mapping
- Session state architecture
- Communication patterns

## Files to Analyze:
- youtube_workflow_agent/agent.py
- youtube_workflow_agent/sub_agents/
- youtube_workflow_agent/config.py

## Output Requirements:
Create: summaries/2025-10-08-agent-1-architecture.md
Include: hierarchy diagram, state flow, patterns, pain points
```

### Timeline Example

```
10:00 AM - Coordinator creates orchestration
10:01 AM - Launch 2 agents (ADK focus = 2 agents)
10:01 AM - Agent 1 starts analyzing architecture
10:01 AM - Agent 2 starts analyzing backend (PARALLEL)
11:00 AM - Agent 1 completes (4,500 lines written)
11:15 AM - Agent 2 completes (5,200 lines written)
11:16 AM - Launch synthesis agent
11:45 AM - Synthesis complete
11:46 AM - Cleanup phase
```

**Total time: 1h 46m** (vs 5+ hours if sequential)

## Implementation Options

### Option 1: Manual (Multiple Browser Windows)

1. Open 6-7 browser windows with AI assistant
2. Paste the appropriate prompts in each
3. Let them run simultaneously
4. Check outputs periodically

### Option 2: API Automation

```python
import asyncio
from ai_client import AIClient

async def run_agent(agent_num, prompt_files):
    client = AIClient()

    # Load prompts
    for file in prompt_files:
        await client.load_file(file)

    # Analyze
    result = await client.analyze()

    # Write output
    output_path = f"summaries/2025-10-08-agent-{agent_num}.md"
    await client.write_output(output_path)

async def telescope_analysis():
    # Phase 0-3: Orchestration
    orchestrator = AIClient()
    await orchestrator.create_orchestration()

    # Phase 4: Parallel agents
    agents = [
        run_agent(1, ["agent-1-architecture.md", ...]),
        run_agent(2, ["agent-2-backend.md", ...]),
    ]
    await asyncio.gather(*agents)  # TRUE PARALLEL EXECUTION

    # Phase 5: Synthesis
    synthesizer = AIClient()
    await synthesizer.synthesize()
```

### Option 3: Cloud Functions

Deploy each agent as a separate cloud function:
- AWS Lambda: 5 functions, invoke parallel
- Google Cloud Functions: 5 functions
- Azure Functions: 5 functions

## Key Benefits of True Parallel Execution

| Metric | Sequential (Wrong) | Parallel (Right) | Improvement |
|--------|-------------------|------------------|-------------|
| **Time** | 5+ hours | 1-2 hours | 60-80% faster |
| **Context per agent** | 25,000 lines | 1,000 lines | 96% reduction |
| **Quality** | Surface-level | Deep analysis | 10x better |
| **Specialization** | Simulated | True expertise | Real insights |
| **Scalability** | Breaks at scale | Handles any size | ∞ |

## Common Mistakes to Avoid

### Mistake 1: Sequential Simulation
```
❌ "Let me analyze as Agent 1, then Agent 2..."
✅ Launch multiple conversations simultaneously
```

### Mistake 2: Loading All Prompts
```
❌ Loading all 5 agent prompts into one context
✅ Each agent loads ONLY their prompt
```

### Mistake 3: Coordination During Analysis
```
❌ Agents trying to communicate during analysis
✅ Agents work independently, synthesis combines later
```

### Mistake 4: Waiting for Each Agent
```
❌ Launch Agent 1, wait, launch Agent 2, wait...
✅ Launch ALL agents at once
```

## Verification Checklist

✅ **Orchestration document created** with all parameters
✅ **Multiple conversations/windows** opened (not tabs in same conversation)
✅ **Each agent has different prompts** loaded
✅ **All agents started within 1-2 minutes** of each other
✅ **No agent loads another agent's prompt**
✅ **Output files being created** in parallel
✅ **Synthesis waits** for all agents to complete

---

**Remember:** The entire value of Telescope's modular design is TRUE PARALLEL EXECUTION. Without it, you're just making the analysis harder and worse. Embrace the parallelism!