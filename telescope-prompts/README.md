# Telescope Prompt Templates

> **Modular prompt system for multi-agent codebase analysis**

> © 2025 AgentLocker.io — Licensed under the MIT License

This folder contains a step-based prompt system that allows agents to load only the specific prompts they need at each phase of the Telescope analysis, rather than ingesting the entire template at once.

## 📁 Folder Structure

```
telescope-prompts/
├── README.md                          # This file - overview and usage guide
├── orchestrator.md                    # Main orchestration logic
│
├── config/
│   ├── target-types.md                # Supported target types (local, GitHub, etc.)
│   ├── focus-modes.md                 # Available focus modes configuration
│   └── output-structure.md            # Output file organization
│
├── steps/
│   ├── 00-preparation.md              # Phase 0: Target preparation
│   ├── 01-focus-detection.md          # Phase 1: Focus detection & agent assignment
│   ├── 02-context-scan.md             # Phase 2: Codebase scanning
│   ├── 03-orchestration.md            # Phase 3: Create orchestration document
│   ├── 04-agent-execution.md          # Phase 4: Multi-agent execution
│   ├── 05-synthesis.md                # Phase 5: Synthesis of findings
│   └── 06-cleanup.md                  # Phase 6: Cleanup & organization
│
├── agents/
│   ├── agent-1-architecture.md        # Architecture specialist prompt
│   ├── agent-2-backend.md             # Backend specialist prompt
│   ├── agent-3-frontend.md            # Frontend specialist prompt
│   ├── agent-4-devops.md              # DevOps specialist prompt
│   ├── agent-5-quality.md             # Quality specialist prompt
│   └── synthesis-agent.md             # Synthesis agent prompt
│
└── focus-modes/
    ├── adk-architecture.md            # ADK-specific analysis focus
    ├── database-design.md             # Database-specific analysis focus
    ├── performance.md                 # Performance analysis focus
    ├── security.md                    # Security analysis focus
    └── full-stack.md                  # Complete analysis (default)
```

## 🚀 Usage

### ⚠️ CRITICAL: True Parallel Execution Required

**This system is designed for TRUE PARALLEL MULTI-AGENT EXECUTION, not sequential simulation.**

The Telescope system requires an environment where multiple AI agents can run independently and simultaneously. Each agent must:
- Have its own separate conversation/context window
- Load only its specific prompt files
- Execute independently of other agents
- Write outputs without coordination

**DO NOT attempt to simulate this with a single AI assistant** - it defeats the entire purpose of the modular design and will overflow context windows.

### For the Orchestrator

The orchestrator should be run by a **coordinator agent** that:

**Step 1: Read the orchestrator file**
```
Read: telescope-prompts/orchestrator.md
```

**Step 2: Execute Phases 0-3 (Preparation through Orchestration)**
```
Read: telescope-prompts/steps/00-preparation.md → Execute
Read: telescope-prompts/steps/01-focus-detection.md → Execute
Read: telescope-prompts/steps/02-context-scan.md → Execute
Read: telescope-prompts/steps/03-orchestration.md → Execute
```

**Step 3: Launch PARALLEL agents for Phase 4**
```
Create orchestration document with agent assignments
Then LAUNCH SEPARATE AI AGENTS IN PARALLEL:
- Agent 1 → New conversation → Load agent-1-architecture.md
- Agent 2 → New conversation → Load agent-2-backend.md
- Agent 3 → New conversation → Load agent-3-frontend.md
- etc.
```

**Step 4: Wait for all agents to complete**
```
Monitor: ai_docs/documentation/[project]/summaries/
Wait for all agent summary files to be created
```

**Step 5: Launch synthesis agent (Phase 5)**
```
New conversation → Load synthesis-agent.md
Synthesis reads all agent summaries and creates master documentation
```

### For Individual Agents (PARALLEL EXECUTION)

**Each agent runs in its OWN SEPARATE CONTEXT/CONVERSATION and only loads:**

1. **The orchestration document (for context):**
   ```
   Read: ai_docs/documentation/[project]/summaries/[DATE]-orchestration.md
   ```

2. **Their specific agent prompt:**
   ```
   Read: telescope-prompts/agents/agent-[N]-[specialization].md
   ```

3. **The focus mode (if not full-stack):**
   ```
   Read: telescope-prompts/focus-modes/[focus-mode].md
   ```

4. **Output structure:**
   ```
   Read: telescope-prompts/config/output-structure.md
   ```

**Each agent independently:**
- Analyzes the codebase based on their specialization
- Creates their summary document
- Exits when complete

**Total context per agent:** ~3-4 files (~1,000 lines) vs entire system

### For Synthesis Agent

**Synthesis agent loads:**

1. **Synthesis prompt:**
   ```
   Read: telescope-prompts/agents/synthesis-agent.md
   ```

2. **Output structure:**
   ```
   Read: telescope-prompts/config/output-structure.md
   ```

3. **All completed agent summaries** (generated during analysis)

## 📦 What Gets Created

After Telescope analysis, you'll have a complete reference package:

```
ai_docs/reference/[project-name]/
│
├── [project-name]/              # COMPLETE CODE SNAPSHOT
│   ├── src/                     # Source code preserved
│   ├── package.json             # Dependencies at analysis time
│   ├── README.md                # Original project docs
│   └── [all source files]       # Snapshot for permanent reference
│
└── documentation/               # ANALYSIS DOCUMENTATION
    ├── summaries/               # Individual agent findings
    ├── master-documentation.md  # Complete synthesis
    ├── pain-points.md           # Issues identified
    ├── recommendations.md       # Actionable improvements
    └── README.md                # Navigation index
```

**Why Both Code + Documentation?**
- **Self-Contained** - All context in one place
- **Version Snapshot** - Documentation references specific code version
- **Time-Travel** - See exactly what was analyzed
- **Portable** - Move entire folder as single unit

## 🔭 Quick Start Commands

### Basic Usage

```bash
# Full analysis (loads: orchestrator + all steps + full-stack focus)
"Telescope analyze /path/to/project"

# Focused analysis (loads: orchestrator + relevant steps + specific focus)
"Telescope focus on ADK architecture"
```

**Result Structure:**
```
ai_docs/reference/my-project/
├── my-project/              ← Code snapshot
└── documentation/           ← Analysis docs
```

## 💡 Execution Environments

### Supported Multi-Agent Environments

Telescope requires environments that support true parallel agent execution:

1. **Multiple AI Assistant Instances**
   - Open 5-6 separate conversations/windows
   - Each loads different agent prompts
   - All analyze simultaneously

2. **API-Based Orchestration**
   - Script that launches multiple API calls
   - Each call to a separate agent/thread
   - Parallel processing via async/await

3. **Agent Platforms**
   - LangChain with multiple chains
   - AutoGen with agent swarm
   - Custom orchestration frameworks

4. **Cloud Functions**
   - AWS Lambda functions (one per agent)
   - Google Cloud Functions
   - Azure Functions

### ❌ What NOT to Do

**DO NOT:**
- Try to run all agents in a single conversation
- Have one AI simulate multiple agents sequentially
- Load all agent prompts into one context

**This will:**
- Overflow context windows (5 agents × 5,000 lines = 25,000 lines)
- Defeat the performance benefits
- Produce inferior analysis (no true specialization)

## 📋 Step-by-Step Flow

### Orchestrator Flow (Coordinator Agent)

```
COORDINATOR AGENT:
1. Load: orchestrator.md
   ↓
2. Execute Phases 0-3 sequentially:
   - Phase 0: Preparation (clone/validate target)
   - Phase 1: Focus Detection (determine mode)
   - Phase 2: Context Scan (analyze structure)
   - Phase 3: Create Orchestration Document
   ↓
3. LAUNCH PARALLEL AGENTS:
   - Start Agent 1 in new conversation → agent-1-architecture.md
   - Start Agent 2 in new conversation → agent-2-backend.md
   - Start Agent 3 in new conversation → agent-3-frontend.md
   - Start Agent 4 in new conversation → agent-4-devops.md
   - Start Agent 5 in new conversation → agent-5-quality.md
   ↓
4. WAIT for all agents to write their summaries
   ↓
5. LAUNCH SYNTHESIS AGENT:
   - Start synthesis in new conversation → synthesis-agent.md
   ↓
6. Execute Phase 6: Cleanup
```

### Individual Agent Flow

```
Agent receives launch signal with:
- agent_number: 1
- focus_mode: "adk_architecture"
- target_path: "/path/to/project"

1. Load: agents/agent-[N]-[specialization].md
   ↓
2. Load: focus-modes/[focus_mode].md (if not full-stack)
   ↓
3. Load: config/output-structure.md
   ↓
4. Execute analysis
   ↓
5. Write output to summaries/[DATE]-agent-[N]-[specialization].md
   ↓
6. Signal completion
```

### Synthesis Agent Flow

```
1. Load: agents/synthesis-agent.md
   ↓
2. Load: config/output-structure.md
   ↓
3. Read all: summaries/[DATE]-agent-*.md
   ↓
4. Execute synthesis
   ↓
5. Write: [DATE]-master-documentation.md
   ↓
6. Write: [DATE]-pain-points.md
   ↓
7. Write: [DATE]-recommendations.md
```

## 🎯 Benefits of This Structure

### 1. **Reduced Context Usage**
- Old: 1 file × 2,325 lines = entire template loaded per agent
- New: 3-4 files × ~100-200 lines = only what's needed

### 2. **Parallel Agent Execution**
- Each agent loads independently
- No contention for the same massive file
- Faster overall analysis time

### 3. **Easier Maintenance**
- Update one step without touching others
- Add new agents by creating single file
- Modify focus modes independently

### 4. **Better Organization**
- Clear separation of concerns
- Easy to find specific prompts
- Simpler to version control changes

### 5. **Flexible Customization**
- Swap out agent prompts easily
- Add custom focus modes
- Override specific steps

## 📝 File Size Reference

| Category | Files | Avg Lines | Context Saved |
|----------|-------|-----------|---------------|
| Orchestrator | 1 | ~150 | N/A (always loaded) |
| Config | 3 | ~100 each | Load as needed |
| Steps | 7 | ~150 each | Load sequentially |
| Agents | 6 | ~200 each | 1 per agent |
| Focus Modes | 5 | ~100 each | 1 per analysis |

**Old System:**
- Every agent: 2,325 lines

**New System:**
- Orchestrator: ~1,200 lines total (loaded incrementally)
- Each agent: ~300-400 lines (only what they need)
- **80-85% context reduction per agent**

## 🔄 Migration Guide

### From Single File to Modular

**Old way:**
```
1. Read telescope.md (2,325 lines)
2. Find relevant section
3. Execute
```

**New way:**
```
1. Read orchestrator.md (~150 lines)
2. Read specific step file (~150 lines)
3. Execute
```

### Example: Launching Agent 1

**Old:**
```
1. Load entire telescope.md
2. Find "Agent 1 Prompt (Architecture Specialist)" section
3. Extract prompt
4. Execute
```

**New:**
```
1. Load agents/agent-1-architecture.md
2. Load focus-modes/adk-architecture.md (if focused)
3. Load config/output-structure.md
4. Execute
```

## 🛠️ Advanced Usage

### Custom Focus Modes

Create new focus mode:
```
1. Create: focus-modes/my-custom-focus.md
2. Define: agents to activate, emphasis areas
3. Use: "Telescope focus on my custom focus"
```

### Custom Agents

Add new agent:
```
1. Create: agents/agent-6-security.md
2. Update: config/focus-modes.md (add to relevant modes)
3. Update: orchestrator.md (add to agent list)
```

### Override Steps

Customize execution:
```
1. Copy: steps/04-agent-execution.md
2. Modify: your custom logic
3. Use: custom orchestrator pointing to modified step
```

## 📖 Documentation

Each file is self-contained with:
- Clear purpose statement
- Input requirements
- Output specifications
- Examples
- Best practices

## 🔍 Finding Information

**To understand...**

- **How Telescope works overall** → Read `orchestrator.md`
- **What targets are supported** → Read `config/target-types.md`
- **What focus modes exist** → Read `config/focus-modes.md`
- **How a specific phase works** → Read `steps/[NN]-[phase].md`
- **What an agent does** → Read `agents/agent-[N]-[name].md`
- **How a focus mode customizes analysis** → Read `focus-modes/[mode].md`

---

**Telescope 🔭**
**Version:** 2.0 (Modular)
**Created:** 2025-10-07 Kirk Truax

## Licensing

All prompt templates in `telescope-prompts/` are © 2025 AgentLocker.io and released under the MIT License. See the LICENSE file at the repository root for details.

