# Telescope - Universal Codebase Analysis Tool

> **Purpose:** Point Telescope at any codebase (local or remote) and get comprehensive multi-agent architecture analysis with organized documentation
> **Created:** 2025-10-07
> **Version:** 1.0
> **Nickname:** "Telescope" 🔭

---

## 🔭 Quick Start

### **Basic Usage:**

```bash
# Local codebase
"Telescope analyze /path/to/project"

# Remote repository
"Telescope analyze https://github.com/user/repo"

# Focused analysis
"Telescope focus on [topic]"
# Examples:
# - "Telescope focus on ADK architecture"
# - "Telescope focus on database design"
# - "Telescope focus on API patterns"
# - "Telescope focus on performance"
```

### **What Telescope Does:**

1. **Prepares target** (clones if remote, validates if local)
2. **Launches 5 specialized agents** in parallel
3. **Each agent analyzes** specific aspects
4. **Synthesizes findings** into master documentation
5. **Organizes outputs** in structured folders

### **Where Outputs Go:**

```
ai_docs/documentation/[project-name]/
├── summaries/
│   ├── 2025-10-07-orchestration.md           # Orchestration plan
│   ├── 2025-10-07-agent-1-architecture.md    # Architecture findings
│   ├── 2025-10-07-agent-2-backend.md         # Backend analysis
│   ├── 2025-10-07-agent-3-frontend.md        # Frontend review
│   ├── 2025-10-07-agent-4-devops.md          # DevOps assessment
│   └── 2025-10-07-agent-5-quality.md         # Quality analysis
│
├── 2025-10-07-master-documentation.md        # Complete synthesis
├── 2025-10-07-pain-points.md                 # Consolidated issues
├── 2025-10-07-recommendations.md             # Actionable improvements
└── 2025-10-07-architecture-diagrams.md       # Visual documentation
```

---

## 1. Telescope Configuration

### 1.1 Target Specification

**Telescope can analyze:**

```yaml
target_types:
  local_path:
    example: "/path/to/project"
    description: "Existing local codebase"
    preparation: "Validate path exists"

  github_url:
    example: "https://github.com/user/repo"
    description: "GitHub repository"
    preparation: "Clone to temp directory"

  gitlab_url:
    example: "https://gitlab.com/user/repo"
    description: "GitLab repository"
    preparation: "Clone to temp directory"

  bitbucket_url:
    example: "https://bitbucket.org/user/repo"
    description: "Bitbucket repository"
    preparation: "Clone to temp directory"
```

### 1.2 Focus Mode Configuration

**Telescope can focus on specific topics:**

```yaml
focus_modes:
  architecture:
    agents: [1, 2]  # Architecture + Backend specialists
    depth: "comprehensive"
    output_emphasis: "system design, component relationships, data flow"

  performance:
    agents: [2, 5]  # Backend + Quality specialists
    depth: "comprehensive"
    output_emphasis: "bottlenecks, optimization opportunities, scalability"

  security:
    agents: [2, 4]  # Backend + DevOps specialists
    depth: "comprehensive"
    output_emphasis: "vulnerabilities, auth patterns, data protection"

  database:
    agents: [2]     # Backend specialist only
    depth: "deep_dive"
    output_emphasis: "schema design, query patterns, migrations"

  api_design:
    agents: [2, 3]  # Backend + Frontend specialists
    depth: "comprehensive"
    output_emphasis: "API contracts, error handling, versioning"

  frontend:
    agents: [3]     # Frontend specialist only
    depth: "deep_dive"
    output_emphasis: "component architecture, state management, UX"

  devops:
    agents: [4]     # DevOps specialist only
    depth: "deep_dive"
    output_emphasis: "CI/CD, infrastructure, deployment"

  testing:
    agents: [5]     # Quality specialist only
    depth: "deep_dive"
    output_emphasis: "test coverage, testing strategies, quality"

  adk_architecture:
    agents: [1, 2]  # Architecture + Backend specialists
    depth: "comprehensive"
    output_emphasis: "ADK patterns, agent hierarchies, session management, callbacks"

  real_time:
    agents: [1, 2, 3]  # Architecture + Backend + Frontend
    depth: "comprehensive"
    output_emphasis: "real-time sync, WebSocket patterns, state updates"

  full_stack:
    agents: [1, 2, 3, 4, 5]  # All agents
    depth: "comprehensive"
    output_emphasis: "complete system analysis"
```

### 1.3 Output Configuration

**Customize output structure:**

```yaml
output_config:
  base_path: "ai_docs/documentation"
  project_folder: "[project-name]"  # Auto-detected from repo/path
  date_format: "YYYY-MM-DD"         # 2025-10-07

  file_naming:
    pattern: "[DATE]-[category]-[title].md"
    examples:
      - "2025-10-07-orchestration.md"
      - "2025-10-07-agent-1-architecture.md"
      - "2025-10-07-master-documentation.md"
      - "2025-10-07-pain-points.md"

  folder_structure:
    summaries: "summaries/"          # Individual agent outputs
    master: "./"                     # Master documentation at root
    artifacts: "artifacts/"          # Diagrams, exports, etc.
```

---

## 2. Telescope Execution Process

### 2.1 Phase 0: Target Preparation

**For Remote Repositories:**

```bash
# Step 1: Detect repository type
if [url contains "github.com"]:
  repo_type = "github"
elif [url contains "gitlab.com"]:
  repo_type = "gitlab"
elif [url contains "bitbucket.org"]:
  repo_type = "bitbucket"

# Step 2: Clone repository
temp_dir = "/tmp/telescope-[project-name]-[timestamp]"
git clone [url] [temp_dir]

# Step 3: Remove .git directory (clean clone)
rm -rf [temp_dir]/.git

# Step 4: Set target path
target_path = temp_dir

# Step 5: Extract project name
project_name = [extracted from url or folder name]
```

**For Local Paths:**

```bash
# Step 1: Validate path exists
if not exists([path]):
  error: "Path does not exist"

# Step 2: Set target path
target_path = [path]

# Step 3: Extract project name
project_name = [folder name or user-provided]
```

**Preparation Output:**

```markdown
## Telescope Target Prepared

**Target Type:** [Local Path / GitHub / GitLab / Bitbucket]
**Source:** [Original URL or path]
**Target Path:** [Where code is located]
**Project Name:** [Detected name]
**Clone Time:** [Timestamp if remote]
**Ready for Analysis:** ✅

---
```

### 2.2 Phase 1: Focus Detection & Agent Assignment

**Telescope analyzes the command:**

```bash
# Default: Full analysis
"Telescope analyze /path/to/project"
→ mode = "full_stack"
→ agents = [1, 2, 3, 4, 5]

# Focused analysis
"Telescope focus on ADK architecture"
→ mode = "adk_architecture"
→ agents = [1, 2]
→ emphasis = "ADK patterns, agent hierarchies, session management"

"Telescope focus on database design"
→ mode = "database"
→ agents = [2]
→ emphasis = "schema design, query patterns, migrations"
```

**Agent Assignment Output:**

```markdown
## Telescope Focus Configuration

**Analysis Mode:** [Mode name]
**Active Agents:** [Count]
**Emphasis Areas:** [List]

### Agent Assignments:

**Agent 1 - Architecture Specialist**
- Status: [Active / Inactive]
- Focus: [Specific areas for this analysis]

**Agent 2 - Backend Specialist**
- Status: [Active / Inactive]
- Focus: [Specific areas for this analysis]

[... repeat for each agent ...]

---
```

### 2.3 Phase 2: Codebase Scanning & Context Gathering

**Telescope scans target to gather context:**

```bash
# Step 1: Detect tech stack
scan_files([
  "package.json",        # Node.js/npm
  "requirements.txt",    # Python
  "Gemfile",            # Ruby
  "pom.xml",            # Java/Maven
  "build.gradle",       # Java/Gradle
  "go.mod",             # Go
  "Cargo.toml",         # Rust
])

# Step 2: Detect frameworks
scan_dependencies([
  "next",               # Next.js
  "react",              # React
  "vue",                # Vue
  "django",             # Django
  "flask",              # Flask
  "express",            # Express
  "@google/adk",        # Agent Development Kit
  "langchain",          # LangChain
])

# Step 3: Detect architecture patterns
scan_directories([
  "src/app/",           # Next.js App Router
  "src/pages/",         # Next.js Pages Router
  "functions/",         # Firebase/Cloud Functions
  "api/",               # API routes
  "components/",        # Component architecture
  "agents/",            # Agent-based architecture
])

# Step 4: Count key metrics
metrics = {
  "total_files": count_files(),
  "total_lines": count_lines(),
  "languages": detect_languages(),
  "components": count_components(),
  "tests": count_test_files(),
}
```

**Context Output:**

```markdown
## Telescope Context Scan

**Project:** [Name]
**Tech Stack:** [Primary technologies]
**Framework:** [Main framework]
**Architecture:** [Detected pattern]

### Codebase Metrics:
- Total Files: [Count]
- Total Lines of Code: [Count]
- Languages: [List with percentages]
- Components: [Count]
- Test Files: [Count]
- Test Coverage: [Percentage if available]

### Directory Structure:
```
[Detected structure]
```

### Key Dependencies:
- [Dependency 1]: [Version]
- [Dependency 2]: [Version]
- [Dependency 3]: [Version]

---
```

### 2.4 Phase 3: Multi-Agent Orchestration

**Create orchestration document:**

**Location:** `ai_docs/documentation/[project-name]/summaries/[DATE]-orchestration.md`

**Template:**

```markdown
# Telescope Orchestration - [Project Name]

> **Date:** [YYYY-MM-DD]
> **Target:** [URL or path]
> **Analysis Mode:** [Mode name]
> **Focus:** [Focus areas]
> **Active Agents:** [Count]

---

## Analysis Configuration

**Project Information:**
- Name: [Project name]
- Type: [web_app, library, api, etc.]
- Tech Stack: [Technologies]
- Source: [Local path or cloned from URL]

**Analysis Scope:**
- Mode: [full_stack / focused analysis]
- Focus Areas: [Specific topics]
- Depth: [comprehensive / high_level / deep_dive]
- Active Agents: [Agent numbers and specializations]

**Output Structure:**
```
ai_docs/documentation/[project-name]/
├── summaries/
│   ├── [DATE]-orchestration.md        # This document
│   ├── [DATE]-agent-1-architecture.md # Agent outputs
│   └── ...
├── [DATE]-master-documentation.md     # Synthesis
└── [DATE]-pain-points.md              # Issues
```

---

## Agent Assignments

### Agent 1: Architecture & Design Specialist

**Status:** [Active / Inactive]

**Focus Areas:**
[Specific to analysis mode]

**Assigned Directories:**
- [Directory 1]
- [Directory 2]

**Expected Deliverables:**
- Architecture overview
- Component relationships
- Design patterns identified
- Pain points in architecture
- Recommendations

**Output Location:**
`summaries/[DATE]-agent-1-architecture.md`

---

### Agent 2: Backend & Database Specialist

**Status:** [Active / Inactive]

**Focus Areas:**
[Specific to analysis mode]

**Assigned Directories:**
- [Directory 1]
- [Directory 2]

**Expected Deliverables:**
- Backend architecture
- Database schema analysis
- API design review
- Data flow documentation
- Pain points in backend
- Recommendations

**Output Location:**
`summaries/[DATE]-agent-2-backend.md`

---

### Agent 3: Frontend & UX Specialist

**Status:** [Active / Inactive]

**Focus Areas:**
[Specific to analysis mode]

**Assigned Directories:**
- [Directory 1]
- [Directory 2]

**Expected Deliverables:**
- Component architecture
- State management patterns
- UI/UX review
- Performance analysis
- Pain points in frontend
- Recommendations

**Output Location:**
`summaries/[DATE]-agent-3-frontend.md`

---

### Agent 4: DevOps & Infrastructure Specialist

**Status:** [Active / Inactive]

**Focus Areas:**
[Specific to analysis mode]

**Assigned Directories:**
- [Directory 1]
- [Directory 2]

**Expected Deliverables:**
- Deployment process documentation
- Infrastructure review
- CI/CD analysis
- Environment management
- Pain points in DevOps
- Recommendations

**Output Location:**
`summaries/[DATE]-agent-4-devops.md`

---

### Agent 5: Quality & Testing Specialist

**Status:** [Active / Inactive]

**Focus Areas:**
[Specific to analysis mode]

**Assigned Directories:**
- [Directory 1]
- [Directory 2]

**Expected Deliverables:**
- Testing strategy review
- Code quality analysis
- Test coverage assessment
- Quality metrics
- Pain points in quality
- Recommendations

**Output Location:**
`summaries/[DATE]-agent-5-quality.md`

---

## Execution Timeline

**Phase 0: Preparation** ✅
- [x] Target cloned/validated
- [x] Context scan completed
- [x] Orchestration document created

**Phase 1: Parallel Agent Execution** 🔄
- [ ] Agent 1 analyzing...
- [ ] Agent 2 analyzing...
- [ ] Agent 3 analyzing...
- [ ] Agent 4 analyzing...
- [ ] Agent 5 analyzing...

**Phase 2: Synthesis** ⏳
- [ ] All agent summaries completed
- [ ] Common themes identified
- [ ] Pain points consolidated
- [ ] Master documentation created

**Phase 3: Cleanup** ⏳
- [ ] Temp directories cleaned (if remote clone)
- [ ] Outputs organized
- [ ] Review ready for user

---

## Progress Tracking

| Agent | Status | Completion | Output |
|-------|--------|-----------|--------|
| 1 - Architecture | ⏳ Pending | 0% | [DATE]-agent-1-architecture.md |
| 2 - Backend | ⏳ Pending | 0% | [DATE]-agent-2-backend.md |
| 3 - Frontend | ⏳ Pending | 0% | [DATE]-agent-3-frontend.md |
| 4 - DevOps | ⏳ Pending | 0% | [DATE]-agent-4-devops.md |
| 5 - Quality | ⏳ Pending | 0% | [DATE]-agent-5-quality.md |

**Legend:**
- ⏳ Pending
- 🔄 In Progress
- ✅ Complete
- ❌ Failed

---

## Notes

[Agent coordination notes, blockers, observations]

---

**Telescope Version:** 1.0
**Orchestration Started:** [Timestamp]
**Expected Completion:** [Estimate]
```

### 2.5 Phase 4: Agent Execution

**Each agent receives customized prompt based on focus mode:**

**Example: "Telescope focus on ADK architecture"**

**Agent 1 Prompt (Architecture Specialist):**

```markdown
You are Agent 1: Architecture Specialist (Telescope Analysis)

## Analysis Target

**Project:** [Project Name]
**Source:** [Path/URL]
**Focus Mode:** ADK Architecture
**Your Specialization:** Agent Development Kit patterns and architecture

## Your Mission

Analyze the codebase specifically for ADK (Agent Development Kit) architecture patterns.
Focus on how agents are structured, how they communicate, and session management.

## Specific Focus Areas

1. **Agent Hierarchies**
   - Root agent structure
   - Sub-agent organization
   - Parent-child relationships
   - Agent composition patterns

2. **Agent Types & Usage**
   - LlmAgent usage patterns
   - SequentialAgent implementations
   - ParallelAgent usage
   - LoopAgent patterns
   - Custom agent classes

3. **Session Management**
   - Session state structure
   - State key usage patterns
   - Input/output key patterns
   - Session lifecycle

4. **Tool Integration**
   - Built-in tools (google_search, code_execution)
   - Custom tool implementations
   - AgentTool usage (agents as tools)
   - Tool distribution across agents

5. **Callback Patterns**
   - before_agent_callback usage
   - after_agent_callback usage
   - before_tool_callback usage
   - after_tool_callback usage
   - Custom callback implementations

6. **Communication Patterns**
   - Agent-to-agent communication
   - State passing mechanisms
   - Escalation patterns
   - Transfer control patterns

## Files to Prioritize

Focus on files containing:
- Agent definitions (look for `Agent(`, `LlmAgent(`, etc.)
- Agent imports (from google.adk.agents import)
- Session state management
- Callback definitions
- Tool definitions

## Required Analysis

### 1. Agent Architecture Map
Create a visual representation (ASCII or description) of agent hierarchy:
```
root_agent (LlmAgent)
├── sub_agent_1 (SequentialAgent)
│   ├── task_agent_a (LlmAgent)
│   └── task_agent_b (LlmAgent)
└── sub_agent_2 (ParallelAgent)
    ├── parallel_task_1 (LlmAgent)
    └── parallel_task_2 (LlmAgent)
```

### 2. Session State Analysis
Document all session state keys used:
```yaml
state_keys:
  user_context:
    created_by: "root_agent"
    type: "Dictionary"
    structure: { "user_id": "string", "preferences": {} }
    used_by: ["root_agent", "task_agent_a"]

  research_results:
    created_by: "research_agent"
    type: "String"
    structure: "Markdown formatted results"
    used_by: ["synthesis_agent"]
```

### 3. Pattern Assessment
Evaluate ADK patterns used:
- ✅ Good patterns (following best practices)
- ⚠️ Anti-patterns (violations of ADK principles)
- 💡 Opportunities (could be improved)

## Output Requirements

Create comprehensive summary at:
**`ai_docs/documentation/[project-name]/summaries/[DATE]-agent-1-architecture.md`**

### Required Sections:

#### 1. Files Reviewed
- [x] File path 1
- [x] File path 2
[Complete checklist]

#### 2. ADK Architecture Overview
[High-level description of agent architecture]

#### 3. Agent Hierarchy Map
[Visual representation of agent structure]

#### 4. Agent Analysis by Type

**LlmAgent Usage:**
- [Agent name]: [Purpose, location, configuration]

**SequentialAgent Usage:**
- [Agent name]: [Purpose, sub-agents, workflow]

**ParallelAgent Usage:**
- [Agent name]: [Purpose, parallel tasks]

**LoopAgent Usage:**
- [Agent name]: [Purpose, iteration logic]

**Custom Agents:**
- [Agent class]: [Purpose, custom logic]

#### 5. Session State Architecture

**State Keys Inventory:**
[Complete list with structure]

**State Flow Diagram:**
[How state flows through agents]

#### 6. Tool Integration Patterns

**Built-in Tools:**
- [Tool]: [Used by which agents, purpose]

**Custom Tools:**
- [Tool]: [Implementation, usage]

**AgentTool Patterns:**
- [Agent as tool]: [Parent agent, usage pattern]

#### 7. Callback Analysis

**Callback Usage:**
- [Agent]: [Callbacks used, purpose]

**Callback Patterns:**
- [Pattern]: [Examples, effectiveness]

#### 8. ADK Best Practices Assessment

**✅ Good Patterns:**
- [Pattern]: [Why it's good, where used]

**⚠️ Anti-Patterns:**
- [Anti-pattern]: [Why problematic, location]

**💡 Improvement Opportunities:**
- [Opportunity]: [What could be better]

#### 9. Pain Points (❌)

**❌ Pain Point 1: [Title]**
- **Problem:** [Description]
- **Location:** [File:line]
- **Impact:** [Effect on system]
- **Severity:** Critical/High/Medium/Low
- **Recommendation:** [How to fix]

[Repeat for each pain point]

#### 10. Focus Areas for Improvement (⭐)

**⭐ Focus Area 1: [Title]**
- **Priority:** Critical/High/Medium/Low
- **Effort:** Low/Medium/High
- **Impact:** Low/Medium/High
- **Description:** [What to improve]
- **Rationale:** [Why it matters]
- **Implementation:** [How to do it]

[Repeat for each focus area]

#### 11. Recommendations

**Immediate Actions:**
- [Action with specific steps]

**Short-term Improvements:**
- [Enhancement with rationale]

**Long-term Enhancements:**
- [Strategic improvement]

---

Begin your analysis now. Focus specifically on ADK architecture patterns.
Be thorough, specific, and actionable in your findings.
```

**Agent 2 Prompt (Backend Specialist - ADK Focus):**

```markdown
You are Agent 2: Backend Specialist (Telescope Analysis)

## Analysis Target

**Project:** [Project Name]
**Source:** [Path/URL]
**Focus Mode:** ADK Architecture
**Your Specialization:** Backend integration with ADK

## Your Mission

Analyze backend integration patterns with ADK agents.
Focus on how agents interact with databases, APIs, and external services.

## Specific Focus Areas

1. **Agent-Database Integration**
   - How agents query databases
   - Database tool implementations
   - Session state vs. persistent storage
   - Data transformation patterns

2. **Agent-API Integration**
   - External API calls from agents
   - API error handling in agents
   - Rate limiting patterns
   - Response processing

3. **Tool Implementations**
   - Custom tool creation for backend operations
   - Tool parameter validation
   - Tool error handling
   - Tool response formatting

4. **State Management**
   - When to use session state vs. database
   - State persistence patterns
   - State cleanup strategies
   - State validation

[... continue with backend-specific analysis requirements ...]

[Same output structure as Agent 1]
```

**Note:** Each active agent receives a customized prompt based on:
1. **Analysis mode** (full_stack vs. focused)
2. **Focus areas** (what to emphasize)
3. **Agent specialization** (their domain expertise)
4. **Output requirements** (consistent format)

### 2.6 Phase 5: Synthesis

**After all agents complete, synthesis agent creates master documentation:**

**Location:** `ai_docs/documentation/[project-name]/[DATE]-master-documentation.md`

**Synthesis Prompt:**

```markdown
You are the Telescope Synthesis Agent

## Your Mission

Review all agent summaries and create comprehensive master documentation for [Project Name].

## Analysis Context

**Focus Mode:** [Mode name]
**Active Agents:** [Count and specializations]
**Emphasis Areas:** [Focus topics]

## Input Documents

Read these agent summaries:
[List of completed agent summaries]

## Synthesis Requirements

### 1. Identify Common Themes
Cross-reference findings across all agents to find:
- Patterns mentioned by multiple agents
- Contradicting observations
- Complementary insights
- System-wide issues

### 2. Consolidate Pain Points
Organize all pain points by:
- Severity (Critical → Low)
- Domain (Architecture, Backend, Frontend, etc.)
- Impact on system
- Effort to fix

### 3. Extract Best Practices
Document effective patterns found:
- Architectural patterns worth replicating
- Code patterns that work well
- Integration strategies that succeed
- Development workflows that help

### 4. Create Actionable Roadmap
Organize recommendations by:
- Timeline (Immediate, Short-term, Long-term)
- Dependencies (what blocks what)
- Risk (what's risky to change)
- Value (impact vs. effort)

## Output Requirements

Create comprehensive master documentation with these sections:

### Executive Summary
- 2-3 paragraph project overview
- Current state assessment
- Top 3 critical findings
- Top 3 priorities

### Focus Analysis: [Focus Topic]
**Deep dive on the analysis focus** (e.g., "ADK Architecture Analysis")

- Overview of topic in this codebase
- Strengths identified
- Weaknesses identified
- Comparison to best practices
- Specific recommendations

### Architecture Overview
[If architecture agents were active]

### Technology Stack
[Complete tech stack breakdown]

### Component Analysis
[Detailed component review]

### Consolidated Pain Points
**Organized by severity:**

#### Critical Issues
[Highest priority problems]

#### High Priority Issues
[Important but not critical]

#### Medium Priority Issues
[Should address eventually]

#### Low Priority Issues
[Nice to fix]

### Prioritized Recommendations

#### Immediate Actions (Week 1)
[What to do now]

#### Short-term Actions (Month 1)
[What to do soon]

#### Long-term Actions (Quarter 1+)
[Strategic improvements]

### Best Practices Identified
[Patterns worth keeping/replicating]

### Implementation Roadmap
[Phased approach to improvements]

### Appendix: Agent Sources
[Links to individual agent summaries]

---

**File Naming:** `[DATE]-master-documentation.md`
**Location:** `ai_docs/documentation/[project-name]/`
**Format:** Markdown with proper headings and formatting
**Length:** Comprehensive (aim for 10,000-20,000 words for full analysis)
```

### 2.7 Phase 6: Cleanup & Organization

**Final cleanup steps:**

```bash
# Step 1: Organize all outputs
move_files([
  "summaries/*.md" → "ai_docs/documentation/[project-name]/summaries/"
  "*-master-documentation.md" → "ai_docs/documentation/[project-name]/"
  "*-pain-points.md" → "ai_docs/documentation/[project-name]/"
])

# Step 2: Create index document
create_index([
  "Location: ai_docs/documentation/[project-name]/README.md"
  "Contents: Links to all outputs, quick navigation"
])

# Step 3: Clean temp directories (if remote clone)
if [was_remote_clone]:
  rm -rf [temp_dir]
  log "Cleaned temporary clone directory"

# Step 4: Generate completion report
create_report([
  "Analysis complete"
  "Files created: [count]"
  "Pain points identified: [count]"
  "Recommendations: [count]"
  "Location: ai_docs/documentation/[project-name]/"
])
```

---

## 3. Focus Mode Deep Dives

### 3.1 ADK Architecture Focus

**Command:** `"Telescope focus on ADK architecture"`

**Activated Agents:** Agent 1 (Architecture), Agent 2 (Backend)

**Analysis Emphasis:**

```yaml
adk_specific_analysis:
  agent_patterns:
    - "Agent type selection (LlmAgent vs. SequentialAgent vs. ParallelAgent vs. LoopAgent)"
    - "Agent hierarchy design"
    - "Root agent as consultant pattern"
    - "Sub-agent specialization"
    - "Custom agent implementations"

  session_management:
    - "Session state structure"
    - "State key naming conventions"
    - "Input/output key patterns"
    - "State data types and structures"
    - "State cleanup strategies"

  tool_integration:
    - "Built-in tool usage (google_search, code_execution, vertex_ai_search)"
    - "Custom tool implementations"
    - "AgentTool patterns (agents as tools)"
    - "Tool parameter design"
    - "Tool error handling"

  callback_patterns:
    - "before_agent_callback usage"
    - "after_agent_callback usage"
    - "before_tool_callback usage"
    - "after_tool_callback usage"
    - "Custom callback implementations"
    - "State transformation callbacks"

  communication:
    - "Agent-to-agent communication patterns"
    - "Transfer control mechanisms"
    - "Escalation patterns"
    - "Parent-child communication"
    - "Peer-to-peer transfer"

  best_practices:
    - "Instruction clarity"
    - "Global vs. local instructions"
    - "Content inclusion control"
    - "Structured outputs (Pydantic schemas)"
    - "Model selection (Flash vs. Pro)"
    - "Disallow transfer patterns"
```

**Expected Outputs:**

1. **Agent Hierarchy Diagram**
   ```
   root_agent (LlmAgent)
   ├── Tools: [AgentTool(research_agent), AgentTool(analysis_agent)]
   ├── research_agent (SequentialAgent)
   │   ├── planning_agent (LlmAgent + google_search)
   │   ├── execution_agent (LlmAgent + code_execution)
   │   └── validation_agent (LlmAgent)
   └── analysis_agent (ParallelAgent)
       ├── quantitative_agent (LlmAgent)
       └── qualitative_agent (LlmAgent)
   ```

2. **Session State Map**
   ```yaml
   user_context:
     created_by: "root_agent"
     type: "Dictionary"
     structure:
       user_id: "string"
       preferences: "dict"
     accessed_by: ["root_agent", "research_agent"]

   research_findings:
     created_by: "execution_agent"
     type: "String"
     structure: "Markdown formatted research results"
     accessed_by: ["validation_agent", "analysis_agent"]
   ```

3. **Pattern Assessment**
   - ✅ **Good:** Root agent delegates to specialists
   - ⚠️ **Anti-pattern:** Complex logic in root agent instructions
   - 💡 **Opportunity:** Could use ParallelAgent for independent research tasks

4. **Pain Points:**
   - ❌ Session state keys not documented (hard to understand flow)
   - ❌ Missing callbacks for source collection
   - ❌ No structured outputs (using raw text parsing)

5. **Recommendations:**
   - ⭐ Document all state keys with data structures
   - ⭐ Implement after_agent_callback for metadata collection
   - ⭐ Use Pydantic schemas for structured outputs

### 3.2 Database Design Focus

**Command:** `"Telescope focus on database design"`

**Activated Agents:** Agent 2 (Backend)

**Analysis Emphasis:**

```yaml
database_specific_analysis:
  schema_design:
    - "Table/collection structure"
    - "Relationships (foreign keys, references)"
    - "Normalization level"
    - "Denormalization patterns"
    - "Indexing strategy"

  data_models:
    - "ORM models (Prisma, Drizzle, Mongoose)"
    - "Type definitions"
    - "Validation rules"
    - "Default values"
    - "Computed fields"

  query_patterns:
    - "Common queries"
    - "Query optimization"
    - "N+1 query issues"
    - "Complex joins"
    - "Aggregation patterns"

  migrations:
    - "Migration strategy"
    - "Down migrations (rollback capability)"
    - "Seed data"
    - "Migration safety"
    - "Data transformation logic"

  performance:
    - "Index coverage"
    - "Query performance"
    - "Database connection pooling"
    - "Caching strategy"
    - "Read/write patterns"
```

### 3.3 Performance Focus

**Command:** `"Telescope focus on performance"`

**Activated Agents:** Agent 2 (Backend), Agent 5 (Quality)

**Analysis Emphasis:**

```yaml
performance_specific_analysis:
  backend_performance:
    - "API response times"
    - "Database query performance"
    - "Caching strategies"
    - "Connection pooling"
    - "Background job processing"

  frontend_performance:
    - "Bundle size analysis"
    - "Code splitting"
    - "Lazy loading patterns"
    - "Image optimization"
    - "Rendering performance"

  infrastructure:
    - "Server response times"
    - "CDN usage"
    - "Caching headers"
    - "Compression"
    - "Load balancing"

  bottlenecks:
    - "Slow queries"
    - "Memory leaks"
    - "CPU intensive operations"
    - "Network latency"
    - "Rendering bottlenecks"
```

---

## 4. Advanced Features

### 4.1 Multi-Repository Analysis

**Analyze multiple repos together:**

```bash
"Telescope analyze https://github.com/user/frontend https://github.com/user/backend"
```

**Creates:**
```
ai_docs/documentation/multi-repo-analysis/
├── frontend/
│   ├── summaries/...
│   └── 2025-10-07-master-documentation.md
├── backend/
│   ├── summaries/...
│   └── 2025-10-07-master-documentation.md
└── 2025-10-07-combined-analysis.md  # Cross-repo insights
```

### 4.2 Incremental Analysis

**Re-analyze with narrower focus:**

```bash
# First: Full analysis
"Telescope analyze /path/to/project"

# Later: Focused re-analysis
"Telescope focus on database design"
# Uses existing full analysis + new focused analysis
```

### 4.3 Comparison Mode

**Compare two versions:**

```bash
"Telescope compare https://github.com/user/repo@v1.0 https://github.com/user/repo@v2.0"
```

**Creates:**
```
ai_docs/documentation/comparison-v1-v2/
├── v1.0/
│   └── 2025-10-07-master-documentation.md
├── v2.0/
│   └── 2025-10-07-master-documentation.md
└── 2025-10-07-comparison-analysis.md  # What changed, improvements, regressions
```

---

## 5. Telescope Commands Reference

### 5.1 Basic Commands

```bash
# Analyze local codebase
"Telescope analyze /path/to/project"

# Analyze remote repository
"Telescope analyze https://github.com/user/repo"

# Analyze with custom name
"Telescope analyze /path/to/project as MyProject"
```

### 5.2 Focus Commands

```bash
# ADK architecture analysis
"Telescope focus on ADK architecture"

# Database design analysis
"Telescope focus on database design"

# Performance analysis
"Telescope focus on performance"

# Security analysis
"Telescope focus on security"

# API design analysis
"Telescope focus on API patterns"

# Frontend architecture
"Telescope focus on frontend"

# DevOps & deployment
"Telescope focus on devops"

# Testing strategy
"Telescope focus on testing"

# Real-time patterns
"Telescope focus on real-time"
```

### 5.3 Advanced Commands

```bash
# Multi-repository analysis
"Telescope analyze repo1 repo2 repo3"

# Comparison analysis
"Telescope compare version1 version2"

# Re-analyze with focus
"Telescope re-analyze MyProject focus on database"

# Custom agent configuration
"Telescope analyze /path --agents 7"

# Deep dive mode
"Telescope deep-dive /path focus on ADK"
```

---

## 6. Output Examples

### 6.1 Orchestration Document Example

**File:** `ai_docs/documentation/polygon/summaries/2025-10-07-orchestration.md`

```markdown
# Telescope Orchestration - Polygon

> **Date:** 2025-10-07
> **Target:** https://github.com/user/polygon
> **Analysis Mode:** ADK Architecture
> **Focus:** Agent patterns, session management, callbacks
> **Active Agents:** 2 (Architecture, Backend)

---

## Analysis Configuration

**Project Information:**
- Name: Polygon
- Type: AI-powered party game
- Tech Stack: Next.js 15, Firebase, Vertex AI ADK
- Source: Cloned from GitHub
- Clone Time: 2025-10-07 14:30:00

**Analysis Scope:**
- Mode: adk_architecture
- Focus Areas: ADK patterns, agent hierarchies, session management, callbacks
- Depth: comprehensive
- Active Agents: 1 (Architecture), 2 (Backend)

[... rest of orchestration document ...]
```

### 6.2 Agent Summary Example

**File:** `ai_docs/documentation/polygon/summaries/2025-10-07-agent-1-architecture.md`

```markdown
# Agent 1: Architecture Analysis - Polygon

> **Date:** 2025-10-07
> **Specialization:** Architecture & ADK Patterns
> **Focus:** ADK architecture, agent hierarchies, session management

---

## Files Reviewed

- [x] `functions/src/agents/root_agent.ts`
- [x] `functions/src/agents/game_agent.ts`
- [x] `functions/src/agents/research_agent.ts`
- [x] `functions/src/tools/game_tools.ts`
- [x] `functions/src/callbacks/state_management.ts`

**Total Files:** 23
**Lines Analyzed:** 4,521

---

## ADK Architecture Overview

Polygon uses a hierarchical agent architecture with a root consultant agent
that delegates to specialized game agents. The architecture follows ADK best
practices with clear separation of concerns and effective use of session state.

### Agent Hierarchy

```
chuck_agent (LlmAgent) - Root consultant
├── Tools: [AgentTool(game_coordinator), google_search]
├── Session State: Manages user context, game preferences
│
└── game_coordinator (SequentialAgent)
    ├── topic_agent (LlmAgent + google_search)
    ├── clue_agent (LlmAgent)
    └── guess_agent (LlmAgent + code_execution)
```

---

## Agent Analysis by Type

### LlmAgent Usage

**chuck_agent (Root Agent)**
- **Location:** `functions/src/agents/root_agent.ts:15`
- **Purpose:** Acts as conversational entry point, gathers context
- **Tools:** AgentTool(game_coordinator), google_search
- **Pattern:** ✅ Follows "root as consultant" best practice
- **Session State:**
  - Writes: `user_context`, `game_preferences`
  - Reads: None (entry point)

**topic_agent**
- **Location:** `functions/src/agents/game_agent.ts:42`
- **Purpose:** Analyzes topic and generates contextual understanding
- **Tools:** google_search
- **Pattern:** ✅ Specialized, single responsibility
- **Session State:**
  - Writes: `topic_analysis`
  - Reads: `user_context`

[... detailed analysis continues ...]

---

## Session State Architecture

### State Keys Inventory

**user_context**
```yaml
created_by: "chuck_agent"
type: "Dictionary"
structure:
  user_id: "string"
  session_id: "string"
  game_code: "string"
  player_role: "string (human|ai)"
data_type: "Dict[str, str]"
accessed_by:
  - chuck_agent (write)
  - topic_agent (read)
  - clue_agent (read)
  - guess_agent (read)
```

**topic_analysis**
```yaml
created_by: "topic_agent"
type: "String"
structure: "Markdown formatted topic analysis"
data_type: "str"
accessed_by:
  - topic_agent (write)
  - clue_agent (read)
```

[... all state keys documented ...]

### State Flow Diagram

```
chuck_agent
  ↓ writes user_context
game_coordinator
  ↓ passes user_context
topic_agent
  ↓ writes topic_analysis, reads user_context
clue_agent
  ↓ writes clue_suggestions, reads user_context + topic_analysis
guess_agent
  ↓ writes guess_result, reads all previous state
```

---

## Tool Integration Patterns

### Built-in Tools

**google_search**
- **Used by:** chuck_agent, topic_agent
- **Purpose:** Research topics and game context
- **Pattern:** ✅ Appropriate use for external knowledge
- **Observation:** Could benefit from after_tool_callback for source collection

**code_execution**
- **Used by:** guess_agent
- **Purpose:** Execute word matching logic
- **Pattern:** ⚠️ Could be replaced with custom tool (more efficient)

### Custom Tools

**None identified** - Opportunity for optimization

### AgentTool Patterns

**game_coordinator as Tool**
- **Parent:** chuck_agent
- **Pattern:** ✅ Correct delegation pattern
- **Observation:** Clean separation between consultation and execution

---

## Callback Analysis

### Callback Usage

**chuck_agent:**
- before_agent_callback: ✅ `setup_game_context`
- after_agent_callback: ❌ None (missing)
- Observation: Should collect conversation history

**topic_agent:**
- before_tool_callback: ❌ None
- after_tool_callback: ❌ None
- Observation: Missing source collection from google_search

**No callbacks found in:** clue_agent, guess_agent

### Callback Patterns

**⚠️ Missing Pattern:** After-agent callbacks for metadata collection
**💡 Opportunity:** Implement source collection callbacks for search results

---

## ADK Best Practices Assessment

### ✅ Good Patterns

**1. Root Agent as Consultant**
- **Location:** `root_agent.ts:15-30`
- **Pattern:** Chuck acts as consultant, delegates to game_coordinator
- **Why Good:** Follows ADK recommendation, clean separation
- **Example:**
  ```typescript
  const chuck_agent = new LlmAgent({
    name: "chuck",
    instruction: "You are a friendly game assistant. Gather context...",
    tools: [new AgentTool(game_coordinator)],
  });
  ```

**2. Sequential Agent for Workflow**
- **Location:** `game_agent.ts:20`
- **Pattern:** game_coordinator orchestrates topic → clue → guess flow
- **Why Good:** Natural sequential game progression
- **Example:**
  ```typescript
  const game_coordinator = new SequentialAgent({
    name: "game_coordinator",
    sub_agents: [topic_agent, clue_agent, guess_agent],
  });
  ```

**3. Clear State Key Naming**
- **Pattern:** Descriptive names like `user_context`, `topic_analysis`
- **Why Good:** Self-documenting, easy to understand flow

### ⚠️ Anti-Patterns

**1. Missing State Documentation**
- **Problem:** State keys used without documented structure
- **Location:** Throughout codebase
- **Impact:** Hard to understand what data flows where
- **Recommendation:** Document all state keys with types and examples

**2. No Structured Outputs**
- **Problem:** Agents return free-form text, parsed manually
- **Location:** clue_agent, guess_agent
- **Impact:** Fragile parsing, inconsistent outputs
- **Recommendation:** Use Pydantic schemas for structured responses
- **Example:**
  ```typescript
  class ClueOutput(BaseModel):
    clue: str = Field(description="The generated clue")
    confidence: float = Field(description="Confidence 0-1")
    reasoning: str = Field(description="Why this clue")

  clue_agent = new LlmAgent({
    output_schema: ClueOutput,
    // ...
  });
  ```

**3. code_execution for Simple Logic**
- **Problem:** Using code_execution for word matching
- **Location:** `guess_agent`
- **Impact:** Slower than custom tool, unnecessary complexity
- **Recommendation:** Create custom `word_matcher` tool

### 💡 Improvement Opportunities

**1. Source Collection Callbacks**
- **Opportunity:** Collect research sources for transparency
- **Implementation:** Add after_tool_callback to topic_agent
- **Benefit:** Users see where AI got information

**2. Error Handling Enhancement**
- **Opportunity:** Add before_tool_callback for validation
- **Implementation:** Validate inputs before expensive google_search calls
- **Benefit:** Reduce wasted API calls, better error messages

**3. Parallel Topic Analysis**
- **Opportunity:** Analyze multiple aspects of topic simultaneously
- **Implementation:** Convert topic_agent to ParallelAgent with sub-agents
- **Benefit:** Faster response time

---

## Pain Points (❌)

### ❌ Pain Point 1: Missing State Documentation

- **Problem:** Session state keys (`user_context`, `topic_analysis`, etc.) are used throughout the codebase but their structure is undocumented
- **Location:** All agents
- **Impact:**
  - Developers don't know what data is available
  - Hard to debug state-related issues
  - Risk of breaking changes when state structure changes
- **Severity:** High
- **Recommendation:**
  - Create `docs/session-state-spec.md` documenting all state keys
  - Add JSDoc comments with state structure examples
  - Example:
    ```typescript
    /**
     * State: user_context
     * Type: { user_id: string, session_id: string, game_code: string, player_role: 'human'|'ai' }
     * Created by: chuck_agent
     * Used by: all game agents
     */
    ```

### ❌ Pain Point 2: No Structured Outputs

- **Problem:** Agents return free-form text that must be parsed manually
- **Location:** `clue_agent.ts:45`, `guess_agent.ts:62`
- **Impact:**
  - Fragile string parsing logic
  - Inconsistent output formats
  - Hard to validate responses
  - Difficult to handle edge cases
- **Severity:** Medium
- **Example of Current Issue:**
  ```typescript
  // Current: Manual parsing
  const clue = response.match(/Clue: (.+)/)?.[1];
  const confidence = parseFloat(response.match(/Confidence: (.+)/)?.[1] || "0");
  ```
- **Recommendation:**
  ```typescript
  // Better: Pydantic schema
  class ClueOutput(BaseModel):
    clue: str = Field(description="Generated clue")
    confidence: float = Field(ge=0.0, le=1.0)
    reasoning: str

  clue_agent = new LlmAgent({
    output_schema: ClueOutput,
    // Gemini automatically returns structured JSON
  });
  ```

### ❌ Pain Point 3: Missing Callback Implementations

- **Problem:** No callbacks for metadata collection or source tracking
- **Location:** All agents
- **Impact:**
  - Cannot track research sources
  - Missing conversation history
  - No audit trail for debugging
  - Can't analyze tool usage patterns
- **Severity:** Medium
- **Recommendation:**
  - Implement `after_tool_callback` on topic_agent for source collection
  - Implement `after_agent_callback` on chuck_agent for history tracking
  - Example:
    ```typescript
    function collect_sources_callback(ctx: CallbackContext) {
      const sources = {};
      for (const event of ctx.session.events) {
        if (event.grounding_metadata) {
          for (const chunk of event.grounding_metadata.grounding_chunks) {
            if (chunk.web) {
              sources[chunk.web.uri] = chunk.web.title;
            }
          }
        }
      }
      ctx.state["research_sources"] = sources;
    }
    ```

[... more pain points ...]

---

## Focus Areas for Improvement (⭐)

### ⭐ Focus Area 1: Implement State Documentation

- **Priority:** High
- **Effort:** Low
- **Impact:** High
- **Description:** Document all session state keys with types, structures, and usage
- **Rationale:**
  - Developers waste time reverse-engineering state flow
  - High risk of breaking changes
  - Poor onboarding experience for new developers
- **Implementation:**
  1. Create `docs/session-state-spec.md`
  2. Document each state key:
     - Name
     - Type (string, dict, etc.)
     - Structure (with example)
     - Created by (which agent)
     - Used by (which agents)
  3. Add JSDoc comments to agent code
  4. Create TypeScript interfaces for state
- **Success Criteria:**
  - All state keys documented
  - Types defined in TypeScript
  - Examples provided for complex structures

### ⭐ Focus Area 2: Migrate to Structured Outputs

- **Priority:** High
- **Effort:** Medium
- **Impact:** High
- **Description:** Replace free-form text responses with Pydantic schemas
- **Rationale:**
  - Current parsing is fragile (breaks on format changes)
  - Difficult to validate responses
  - Inconsistent outputs across runs
  - Hard to handle edge cases
- **Implementation:**
  1. Define Pydantic schemas for each agent output:
     ```python
     class TopicAnalysis(BaseModel):
       topic_category: str
       key_concepts: List[str]
       difficulty: Literal["easy", "medium", "hard"]

     class ClueOutput(BaseModel):
       clue: str
       confidence: float = Field(ge=0, le=1)
       reasoning: str

     class GuessOutput(BaseModel):
       guess: str
       confidence: float
       matching_logic: str
       word_scores: Dict[str, float]
     ```
  2. Update agents to use `output_schema`:
     ```typescript
     const clue_agent = new LlmAgent({
       output_schema: ClueOutput,
       instruction: "Generate a clue...",
     });
     ```
  3. Remove manual parsing code
  4. Add validation logic for structured outputs
- **Success Criteria:**
  - All agents use structured outputs
  - Zero parsing errors
  - Consistent output format
  - Validated responses

### ⭐ Focus Area 3: Implement Callback System

- **Priority:** Medium
- **Effort:** Medium
- **Impact:** Medium
- **Description:** Add callbacks for metadata collection and audit trails
- **Rationale:**
  - Need research source transparency
  - Want conversation history for debugging
  - Require tool usage analytics
  - Enable better error tracking
- **Implementation:**
  1. Source collection callback (topic_agent):
     ```typescript
     function collect_sources(ctx: CallbackContext) {
       // Extract sources from grounding metadata
       const sources = extract_sources_from_events(ctx.session.events);
       ctx.state["research_sources"] = sources;
     }

     topic_agent.after_tool_callback = collect_sources;
     ```
  2. History tracking callback (chuck_agent):
     ```typescript
     function track_history(ctx: CallbackContext) {
       const history = ctx.session.events.map(e => ({
         author: e.author,
         content: e.content,
         timestamp: e.timestamp,
       }));
       ctx.state["conversation_history"] = history;
     }

     chuck_agent.after_agent_callback = track_history;
     ```
  3. Tool usage analytics (all agents):
     ```typescript
     function track_tool_usage(ctx: CallbackContext) {
       const usage = ctx.state.get("tool_usage", {});
       usage[ctx.tool_name] = (usage[ctx.tool_name] || 0) + 1;
       ctx.state["tool_usage"] = usage;
     }

     // Apply to all agents
     all_agents.forEach(agent => {
       agent.before_tool_callback = track_tool_usage;
     });
     ```
- **Success Criteria:**
  - Research sources collected and displayed
  - Conversation history available for debugging
  - Tool usage tracked for analytics
  - Audit trail complete

[... more focus areas ...]

---

## Recommendations

### Immediate Actions (Week 1)

**1. Document Session State**
- Create `docs/session-state-spec.md`
- Add JSDoc comments to all state key usage
- Define TypeScript interfaces
- **Effort:** 4 hours
- **Impact:** High (improves developer experience immediately)

**2. Fix Missing Wireframes**
- Note: Discovered `wireframe.md` is for wrong product (RAG-SaaS)
- Create actual Polygon game wireframes
- **Effort:** 8 hours (design time)
- **Impact:** Critical (blocking frontend development)

**3. Add Basic Callbacks**
- Implement source collection on topic_agent
- Implement history tracking on chuck_agent
- **Effort:** 6 hours
- **Impact:** Medium (improves transparency)

### Short-term Improvements (Month 1)

**1. Migrate to Structured Outputs**
- Define Pydantic schemas for all agents
- Update agent configurations
- Remove manual parsing code
- Test thoroughly
- **Effort:** 12 hours
- **Impact:** High (eliminates parsing bugs)

**2. Create Custom Tools**
- Replace code_execution with custom word_matcher tool
- Optimize game logic execution
- **Effort:** 8 hours
- **Impact:** Medium (performance improvement)

**3. Implement Error Handling**
- Add before_tool_callback for validation
- Improve error messages
- Add retry logic for transient failures
- **Effort:** 10 hours
- **Impact:** Medium (better reliability)

### Long-term Enhancements (Quarter 1+)

**1. Optimize with Parallel Agents**
- Convert topic_agent to ParallelAgent
- Analyze multiple topic aspects simultaneously
- **Effort:** 16 hours
- **Impact:** Medium (faster response times)

**2. Add Observability**
- Implement comprehensive logging
- Add monitoring dashboards
- Track agent performance metrics
- **Effort:** 24 hours
- **Impact:** High (production readiness)

**3. Create Agent Testing Framework**
- Unit tests for each agent
- Integration tests for workflows
- Mock tools for testing
- **Effort:** 32 hours
- **Impact:** High (quality assurance)

---

**Analysis Completed:** 2025-10-07 15:45:00
**Total Analysis Time:** 1 hour 15 minutes
**Files Analyzed:** 23
**Lines of Code:** 4,521
**Pain Points Identified:** 8
**Recommendations Made:** 12
```

### 6.3 Master Documentation Example

**File:** `ai_docs/documentation/polygon/2025-10-07-master-documentation.md`

[This would be similar to the master documentation we created earlier, but focused on the specific analysis mode]

---

## 7. File Naming Standards

### 7.1 Naming Convention

**All Telescope outputs follow this pattern:**

```
[DATE]-[category]-[title].md

Components:
- DATE: YYYY-MM-DD format (e.g., 2025-10-07)
- category: Type of document (see categories below)
- title: Descriptive kebab-case title

Examples:
- 2025-10-07-orchestration.md
- 2025-10-07-agent-1-architecture.md
- 2025-10-07-master-documentation.md
- 2025-10-07-pain-points.md
- 2025-10-07-recommendations.md
- 2025-10-07-architecture-diagrams.md
```

### 7.2 Document Categories

```yaml
categories:
  orchestration:
    description: "Multi-agent coordination plans"
    location: "summaries/"
    example: "2025-10-07-orchestration.md"

  agent-summaries:
    description: "Individual agent findings"
    location: "summaries/"
    pattern: "2025-10-07-agent-[N]-[specialization].md"
    examples:
      - "2025-10-07-agent-1-architecture.md"
      - "2025-10-07-agent-2-backend.md"

  master-documentation:
    description: "Complete synthesis of all findings"
    location: "./"
    example: "2025-10-07-master-documentation.md"

  pain-points:
    description: "Consolidated issues and problems"
    location: "./"
    example: "2025-10-07-pain-points.md"

  recommendations:
    description: "Actionable improvements"
    location: "./"
    example: "2025-10-07-recommendations.md"

  architecture:
    description: "Architecture diagrams and visualizations"
    location: "./"
    example: "2025-10-07-architecture-diagrams.md"

  comparison:
    description: "Version or repo comparisons"
    location: "./"
    example: "2025-10-07-comparison-v1-v2.md"
```

### 7.3 Index Document

**Every analysis includes an index:**

**File:** `ai_docs/documentation/[project-name]/README.md`

```markdown
# Telescope Analysis: [Project Name]

> **Analysis Date:** [DATE]
> **Analysis Type:** [Full Stack / Focused]
> **Focus Areas:** [List if focused]

---

## Quick Links

### Master Documentation
- 📄 **[Master Documentation](2025-10-07-master-documentation.md)** - Complete analysis synthesis
- ❌ **[Pain Points](2025-10-07-pain-points.md)** - Consolidated issues
- ⭐ **[Recommendations](2025-10-07-recommendations.md)** - Actionable improvements
- 🏗️ **[Architecture Diagrams](2025-10-07-architecture-diagrams.md)** - Visual documentation

### Agent Summaries
- 🔍 **[Orchestration](summaries/2025-10-07-orchestration.md)** - Analysis plan
- 1️⃣ **[Architecture Analysis](summaries/2025-10-07-agent-1-architecture.md)**
- 2️⃣ **[Backend Analysis](summaries/2025-10-07-agent-2-backend.md)**
- 3️⃣ **[Frontend Analysis](summaries/2025-10-07-agent-3-frontend.md)**
- 4️⃣ **[DevOps Analysis](summaries/2025-10-07-agent-4-devops.md)**
- 5️⃣ **[Quality Analysis](summaries/2025-10-07-agent-5-quality.md)**

---

## Analysis Summary

**Project:** [Name]
**Tech Stack:** [Primary technologies]
**Analysis Mode:** [Mode]
**Active Agents:** [Count]

**Key Findings:**
- [Finding 1]
- [Finding 2]
- [Finding 3]

**Top Priorities:**
1. [Priority 1]
2. [Priority 2]
3. [Priority 3]

---

## File Structure

```
ai_docs/documentation/[project-name]/
├── README.md (this file)
├── summaries/
│   ├── 2025-10-07-orchestration.md
│   ├── 2025-10-07-agent-1-architecture.md
│   ├── 2025-10-07-agent-2-backend.md
│   ├── 2025-10-07-agent-3-frontend.md
│   ├── 2025-10-07-agent-4-devops.md
│   └── 2025-10-07-agent-5-quality.md
├── 2025-10-07-master-documentation.md
├── 2025-10-07-pain-points.md
├── 2025-10-07-recommendations.md
└── 2025-10-07-architecture-diagrams.md
```

---

**Telescope Version:** 1.0
**Analysis Duration:** [Time taken]
**Last Updated:** [Timestamp]
```

---

## 8. Troubleshooting

### 8.1 Common Issues

**Issue: "Path not found" for local codebase**
- **Cause:** Invalid path or typo
- **Solution:** Verify path exists, check for typos
- **Command:** Use absolute paths, not relative

**Issue: "Clone failed" for remote repo**
- **Cause:** Invalid URL, private repo, network issue
- **Solution:**
  - Verify URL is correct
  - For private repos, ensure authentication
  - Check network connection
- **Alternative:** Clone manually, then use local path

**Issue: "No agents activated" in focus mode**
- **Cause:** Unknown focus keyword
- **Solution:** Use valid focus modes (see Section 1.2)
- **Available:** architecture, database, performance, security, api_design, frontend, devops, testing, adk_architecture, real_time, full_stack

**Issue: "Incomplete agent summaries"**
- **Cause:** Agents didn't find relevant code
- **Solution:**
  - Verify codebase contains expected patterns
  - Try different focus mode
  - Check agent prompts were understood

**Issue: "Output folder already exists"**
- **Cause:** Previous analysis not cleaned up
- **Solution:**
  - Delete old analysis: `rm -rf ai_docs/documentation/[project-name]/`
  - Or specify different date manually
  - Or use incremental mode

---

## 9. Telescope Prompt Examples

### Example 1: Basic Local Analysis

```
User: "Telescope analyze /Users/ktrua/source/games/mimic"

Telescope:
✅ Target validated: /Users/ktrua/source/games/mimic
✅ Project detected: mimic
✅ Context scan complete: Next.js 15, Firebase, Vertex AI
✅ Analysis mode: full_stack
✅ Agents activated: 5

🔄 Launching multi-agent analysis...

Agent 1 (Architecture): ✅ Complete
Agent 2 (Backend): ✅ Complete
Agent 3 (Frontend): ✅ Complete
Agent 4 (DevOps): ✅ Complete
Agent 5 (Quality): ✅ Complete

✅ Synthesis complete

📄 Documentation created:
- ai_docs/documentation/mimic/2025-10-07-master-documentation.md
- ai_docs/documentation/mimic/2025-10-07-pain-points.md
- ai_docs/documentation/mimic/2025-10-07-recommendations.md
- ai_docs/documentation/mimic/summaries/ (6 files)

🎯 Top 3 findings:
1. Missing game UI wireframes (Critical)
2. Undocumented session state structure (High)
3. No structured outputs for agents (High)

📊 Analysis complete: 8 pain points, 12 recommendations
```

### Example 2: Remote Repo with Focus

```
User: "Telescope analyze https://github.com/anthropics/agent-starter-pack focus on ADK architecture"

Telescope:
✅ Repository detected: GitHub
✅ Cloning: agent-starter-pack
✅ Clone complete: /tmp/telescope-agent-starter-pack-1696789234
✅ Removed .git directory
✅ Context scan complete: Python, ADK, LangGraph
✅ Analysis mode: adk_architecture
✅ Agents activated: 2 (Architecture, Backend)

🔄 Launching focused analysis on ADK architecture...

Agent 1 (Architecture): ✅ Complete - 43 agents analyzed
Agent 2 (Backend): ✅ Complete - ADK integration patterns documented

✅ Synthesis complete

📄 Documentation created:
- ai_docs/documentation/agent-starter-pack/2025-10-07-master-documentation.md
- ai_docs/documentation/agent-starter-pack/summaries/ (3 files)

🎯 ADK Architecture Findings:
- 5 different agent hierarchy patterns identified
- Excellent callback usage examples
- Strong session state documentation
- Production-ready patterns

📊 Analysis complete: 12 best practices extracted, 3 minor suggestions

🗑️ Cleaned temp directory: /tmp/telescope-agent-starter-pack-1696789234
```

### Example 3: Comparison Mode

```
User: "Telescope compare https://github.com/user/myapp@v1.0 https://github.com/user/myapp@v2.0"

Telescope:
✅ Cloning v1.0...
✅ Cloning v2.0...
✅ Analysis mode: comparison
✅ Agents activated: 5 (per version)

🔄 Analyzing v1.0...
[10 agents complete]

🔄 Analyzing v2.0...
[10 agents complete]

🔄 Comparing versions...

📄 Documentation created:
- ai_docs/documentation/comparison-v1-v2/v1.0/2025-10-07-master-documentation.md
- ai_docs/documentation/comparison-v1-v2/v2.0/2025-10-07-master-documentation.md
- ai_docs/documentation/comparison-v1-v2/2025-10-07-comparison-analysis.md

🎯 Key Changes from v1.0 → v2.0:
✅ Improvements:
  - Migrated to structured outputs (Pydantic schemas)
  - Added comprehensive callbacks
  - Implemented error handling

⚠️ Regressions:
  - Removed some documentation
  - Increased code complexity in agent initialization

📈 Metrics:
  - Lines of code: +2,341
  - Agent count: 5 → 8
  - Test coverage: 45% → 67%

🗑️ Cleaned temp directories
```

---

## 10. Integration with Existing Workflows

### 10.1 CI/CD Integration

**Auto-analyze on PR:**

```yaml
# .github/workflows/telescope-analysis.yml
name: Telescope Analysis

on:
  pull_request:
    branches: [main, develop]

jobs:
  analyze:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2

      - name: Run Telescope Analysis
        run: |
          # Run focused analysis on changed areas
          telescope analyze . focus on changes

      - name: Upload Results
        uses: actions/upload-artifact@v2
        with:
          name: telescope-analysis
          path: ai_docs/documentation/

      - name: Comment on PR
        uses: actions/github-script@v5
        with:
          script: |
            const fs = require('fs');
            const summary = fs.readFileSync(
              'ai_docs/documentation/*/2025-*-pain-points.md',
              'utf8'
            );

            github.rest.issues.createComment({
              issue_number: context.issue.number,
              owner: context.repo.owner,
              repo: context.repo.repo,
              body: `## Telescope Analysis\n\n${summary}`
            });
```

### 10.2 Pre-commit Hook

**Analyze before commit:**

```bash
# .git/hooks/pre-commit
#!/bin/bash

# Run quick analysis on staged files
staged_files=$(git diff --cached --name-only)

if [[ $staged_files == *"agents/"* ]]; then
  echo "🔭 Telescope: ADK changes detected, running quick analysis..."
  telescope quick-check focus on ADK architecture
fi
```

---

## 11. Maintenance & Updates

### 11.1 Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2025-10-07 | Initial Telescope release |

### 11.2 Future Enhancements

**Planned Features:**

- 🔜 **AI-Powered Focus Detection** - Auto-detect what to focus on
- 🔜 **Interactive Reports** - HTML/web-based interactive documentation
- 🔜 **Diff Analysis** - Analyze changes between commits
- 🔜 **Custom Agent Plugins** - User-defined specialized agents
- 🔜 **Real-time Monitoring** - Continuous codebase health tracking
- 🔜 **Team Dashboards** - Aggregate metrics across projects

---

**Telescope 🔭**
**Version:** 1.0
**Created:** 2025-10-07
**Maintained By:** Architecture Team
**Questions:** Open issue in repository
