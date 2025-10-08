# Telescope Orchestrator

> **Main coordination logic for multi-agent codebase analysis**

## Purpose

This is the entry point for Telescope analysis. The orchestrator:
1. Interprets user commands
2. Loads appropriate configuration
3. Executes analysis phases sequentially
4. Coordinates parallel agent execution
5. Synthesizes final outputs

## Quick Start

### Basic Commands

```bash
# Full analysis
"Telescope analyze /path/to/project"
"Telescope analyze https://github.com/user/repo"

# Focused analysis
"Telescope focus on ADK architecture"
"Telescope focus on database design"
"Telescope focus on performance"

# Custom project name
"Telescope analyze /path/to/project as MyProject"
```

## Execution Flow

### Phase 0: Preparation
**Load:** `steps/00-preparation.md`
- Validate/clone target
- Extract project name
- Clean clone (remove .git if remote)

### Phase 1: Focus Detection
**Load:** `steps/01-focus-detection.md`
- Parse user command for focus keywords
- Determine analysis mode
- Assign agents

### Phase 2: Context Scan
**Load:** `steps/02-context-scan.md`
- Detect tech stack
- Identify frameworks
- Count metrics
- Build context

### Phase 3: Orchestration Document
**Load:** `steps/03-orchestration.md`
- Create orchestration plan
- Document agent assignments
- Prepare progress tracking

### Phase 4: Agent Execution
**Load:** `steps/04-agent-execution.md`
- Launch agents in parallel
- Each agent loads:
  - `agents/agent-[N]-[specialization].md`
  - `focus-modes/[mode].md` (if applicable)
  - `config/output-structure.md`
- Wait for completion

### Phase 5: Synthesis
**Load:** `steps/05-synthesis.md`
- Synthesis agent loads:
  - `agents/synthesis-agent.md`
  - All agent summaries
  - `config/output-structure.md`
- Create master documentation
- Extract pain points
- Generate recommendations

### Phase 6: Cleanup
**Load:** `steps/06-cleanup.md`
- Organize outputs
- Create index document
- Clean temp directories (if remote clone)
- Generate completion report

## Configuration

### Load as Needed

**Target Types:**
```
Load: config/target-types.md
Purpose: Understand what targets are supported
When: Phase 0 (Preparation)
```

**Focus Modes:**
```
Load: config/focus-modes.md
Purpose: Determine which agents to activate
When: Phase 1 (Focus Detection)
```

**Output Structure:**
```
Load: config/output-structure.md
Purpose: Know where to write files
When: Multiple phases, shared with agents
```

## Command Parsing

### Analyze Command

```bash
"Telescope analyze [TARGET]"
"Telescope analyze [TARGET] as [NAME]"
```

**Logic:**
1. Extract target (path or URL)
2. Extract custom name (if "as [NAME]" provided)
3. Set mode: "full_stack"
4. Proceed to Phase 0

### Focus Command

```bash
"Telescope focus on [TOPIC]"
"Telescope analyze [TARGET] focus on [TOPIC]"
```

**Logic:**
1. Extract target (or use current directory)
2. Extract topic keywords
3. Load `config/focus-modes.md`
4. Match topic to focus mode
5. Set mode and active agents
6. Proceed to Phase 0

### Comparison Command

```bash
"Telescope compare [TARGET1] [TARGET2]"
"Telescope compare [TARGET]@v1.0 [TARGET]@v2.0"
```

**Logic:**
1. Extract both targets
2. Set mode: "comparison"
3. Run full analysis on each
4. Create comparison synthesis

## Agent Coordination

### Parallel Execution (CRITICAL)

**⚠️ IMPORTANT: Agents must run in SEPARATE, INDEPENDENT conversations/contexts**

**When launching agents:**

```
DO NOT SIMULATE - ACTUALLY LAUNCH IN PARALLEL:

1. Create orchestration document with all parameters

2. For each active agent, START A NEW CONVERSATION:

   NEW CONVERSATION 1:
   - "Load: ai_docs/documentation/[project]/summaries/[DATE]-orchestration.md"
   - "Load: telescope-prompts/agents/agent-1-architecture.md"
   - "Load: telescope-prompts/focus-modes/[mode].md"
   - "Analyze and create summary"

   NEW CONVERSATION 2 (SIMULTANEOUS):
   - "Load: ai_docs/documentation/[project]/summaries/[DATE]-orchestration.md"
   - "Load: telescope-prompts/agents/agent-2-backend.md"
   - "Load: telescope-prompts/focus-modes/[mode].md"
   - "Analyze and create summary"

   [... MORE CONVERSATIONS FOR OTHER AGENTS ...]

3. Each agent INDEPENDENTLY:
   - Reads orchestration for context
   - Loads ONLY their specific prompts
   - Analyzes based on their specialization
   - Writes summary to summaries/[DATE]-agent-[N]-[specialization].md
   - Exits when complete

4. Orchestrator monitors for completion:
   - Check if all expected summary files exist
   - Verify file sizes (should be 2,000+ lines each)
   - Only proceed to synthesis when ALL complete
```

**Why This Matters:**
- Each agent needs ~5,000 lines of context for deep analysis
- 5 agents × 5,000 lines = 25,000 lines (impossible in one context)
- Parallel execution = 5× faster analysis
- True specialization = better quality findings

### Sequential Steps

**Orchestrator must execute phases sequentially:**

```
Phase 0 → Phase 1 → Phase 2 → Phase 3 → Phase 4 (parallel) → Phase 5 → Phase 6
```

**Within Phase 4:**
- Agents run in parallel (independent)
- Each loads only their required files
- No inter-agent communication during analysis

## File Loading Strategy

### Orchestrator Loads

**Always:**
- `orchestrator.md` (this file)
- All `steps/*.md` files (sequentially as needed)

**Conditionally:**
- `config/target-types.md` (if unclear about target)
- `config/focus-modes.md` (when determining focus)
- `config/output-structure.md` (when writing files)

### Agents Load

**Each agent loads only:**
1. Their prompt: `agents/agent-[N]-[specialization].md`
2. Focus mode: `focus-modes/[mode].md` (if not full_stack)
3. Output spec: `config/output-structure.md`

**Total: 2-3 files per agent (vs. entire template)**

### Synthesis Agent Loads

**Synthesis loads:**
1. `agents/synthesis-agent.md`
2. `config/output-structure.md`
3. All `summaries/[DATE]-agent-*.md` (generated during Phase 4)

## Progress Tracking

### Orchestration Document

**Created in Phase 3:**

```markdown
Location: ai_docs/documentation/[project-name]/summaries/[DATE]-orchestration.md

Contents:
- Analysis configuration
- Agent assignments
- Progress tracking table
- Execution timeline

Updated throughout execution:
- Agent status (Pending → In Progress → Complete)
- Completion percentages
- Notes and observations
```

### User Communication

**Provide updates:**

```
✅ Phase 0 complete: Target prepared
✅ Phase 1 complete: 5 agents assigned
✅ Phase 2 complete: Context scanned (Next.js 15, Firebase, ADK)
✅ Phase 3 complete: Orchestration document created
🔄 Phase 4: Launching 5 agents in parallel...
  - Agent 1 (Architecture): ✅ Complete
  - Agent 2 (Backend): ✅ Complete
  - Agent 3 (Frontend): 🔄 In Progress
  - Agent 4 (DevOps): 🔄 In Progress
  - Agent 5 (Quality): ⏳ Pending
```

## Error Handling

### Phase Failures

**If Phase 0 fails (Preparation):**
- Cannot find target → Error with clear message
- Clone fails → Suggest manual clone then use local path
- Invalid permissions → Check permissions

**If Phase 1 fails (Focus Detection):**
- Unknown focus keyword → List available focus modes
- Suggest full_stack as default

**If Phase 4 fails (Agent Execution):**
- Agent doesn't complete → Mark as failed in orchestration doc
- Continue with other agents
- Note incomplete analysis in synthesis

**If Phase 5 fails (Synthesis):**
- Missing agent summaries → Create partial synthesis
- Note which agents completed
- Provide available insights

### Graceful Degradation

**Philosophy:**
- Complete what can be completed
- Document what failed
- Provide partial results
- Don't fail entire analysis for one agent failure

## Output Locations

### Orchestrator Creates

```
ai_docs/documentation/[project-name]/
├── summaries/
│   └── [DATE]-orchestration.md        # Phase 3
│
├── [DATE]-master-documentation.md     # Phase 5 (synthesis)
├── [DATE]-pain-points.md              # Phase 5 (synthesis)
├── [DATE]-recommendations.md          # Phase 5 (synthesis)
└── README.md                          # Phase 6 (cleanup)
```

### Agents Create

```
ai_docs/documentation/[project-name]/summaries/
├── [DATE]-agent-1-architecture.md
├── [DATE]-agent-2-backend.md
├── [DATE]-agent-3-frontend.md
├── [DATE]-agent-4-devops.md
└── [DATE]-agent-5-quality.md
```

## Variables to Track

### Throughout Execution

```yaml
project_name: "extracted from path/URL or user-provided"
target_path: "/path/to/analyzed/code"
target_type: "local_path | github | gitlab | bitbucket"
analysis_mode: "full_stack | adk_architecture | database | etc."
focus_areas: ["list", "of", "focus", "topics"]
active_agents: [1, 2, 3, 4, 5]  # or subset for focused analysis
date: "YYYY-MM-DD"
output_base: "ai_docs/documentation/[project-name]"
temp_dir: "/tmp/telescope-[project-name]-[timestamp]" # if remote clone
```

## Best Practices

### For Orchestrator

1. **Load files only when needed** - Don't pre-load everything
2. **Execute phases sequentially** - Don't skip steps
3. **Launch agents in parallel** - Maximize efficiency
4. **Provide progress updates** - Keep user informed
5. **Handle errors gracefully** - Complete what can be completed
6. **Clean up after** - Remove temp directories

### For Communication

1. **Use clear status indicators** - ✅ 🔄 ⏳ ❌
2. **Provide context** - What phase, what agents, what found
3. **Share early findings** - Don't wait until synthesis complete
4. **Link to outputs** - Show where documentation was created

### For Performance

1. **Parallel agent execution** - Never run agents sequentially unless dependencies exist
2. **Minimal file loading** - Each component loads only what it needs
3. **Stream updates** - Don't wait for everything to complete before communicating
4. **Clean up promptly** - Remove temp directories when done

## Next Steps

After reading this orchestrator file:

1. **Load Phase 0 prompt:**
   ```
   Read: steps/00-preparation.md
   ```

2. **Execute Phase 0** based on user command

3. **Continue through phases sequentially**

---

**Telescope 🔭**
**Orchestrator Version:** 1.0
**Last Updated:** 2025-10-07
