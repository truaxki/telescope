# Telescope Prompt Templates

> **Modular prompt system for multi-agent codebase analysis**

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

### For the Orchestrator

**Step 1: Read the orchestrator file**
```
Read: telescope-prompts/orchestrator.md
```

**Step 2: Load configuration as needed**
```
Read: telescope-prompts/config/target-types.md      # To understand target
Read: telescope-prompts/config/focus-modes.md       # To determine focus
```

**Step 3: Execute steps sequentially**
```
Read: telescope-prompts/steps/00-preparation.md
Execute Phase 0...

Read: telescope-prompts/steps/01-focus-detection.md
Execute Phase 1...

[Continue through all steps]
```

### For Individual Agents

**Each agent only needs to load:**

1. **Their specific agent prompt:**
   ```
   Read: telescope-prompts/agents/agent-1-architecture.md
   ```

2. **The focus mode (if applicable):**
   ```
   Read: telescope-prompts/focus-modes/adk-architecture.md
   ```

3. **Output structure:**
   ```
   Read: telescope-prompts/config/output-structure.md
   ```

**Total context:** ~3 files instead of 1 massive template

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

## 🔭 Quick Start Commands

### Basic Usage

```bash
# Full analysis (loads: orchestrator + all steps + full-stack focus)
"Telescope analyze /path/to/project"

# Focused analysis (loads: orchestrator + relevant steps + specific focus)
"Telescope focus on ADK architecture"
```

## 📋 Step-by-Step Flow

### Orchestrator Flow

```
1. Load: orchestrator.md
   ↓
2. Load: config/target-types.md
   ↓
3. Load: config/focus-modes.md
   ↓
4. Load: steps/00-preparation.md → Execute
   ↓
5. Load: steps/01-focus-detection.md → Execute
   ↓
6. Load: steps/02-context-scan.md → Execute
   ↓
7. Load: steps/03-orchestration.md → Execute
   ↓
8. Load: steps/04-agent-execution.md → Launch agents in parallel
   ↓
   [Agents execute independently - see below]
   ↓
9. Wait for all agents to complete
   ↓
10. Load: steps/05-synthesis.md → Execute
   ↓
11. Load: steps/06-cleanup.md → Execute
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
**Version:** 1.0 (Modular)
**Created:** 2025-10-07
