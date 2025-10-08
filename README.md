# Telescope 🔭

> **Point Telescope at any codebase and get comprehensive multi-agent architecture analysis with organized documentation**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Version](https://img.shields.io/badge/version-1.0-blue.svg)](https://github.com/yourusername/telescope)
[![AI Engineering](https://img.shields.io/badge/AI-Engineering-purple.svg)](https://github.com/yourusername/telescope)

---

## 🎯 What is Telescope?

Telescope is a **prompt template framework** for comprehensive codebase analysis using multi-agent orchestration. Point it at any codebase (local or remote), and it generates detailed architecture documentation, identifies pain points, and provides actionable recommendations.

**In essence:** Telescope demonstrates the power of structured prompt templates in AI engineering—transforming a complex analysis task into a repeatable, organized, and thorough process.

---

## ⚡ Quick Start

### Basic Usage

```bash
# Analyze local codebase
"Telescope analyze /path/to/project"

# Analyze remote repository
"Telescope analyze https://github.com/user/repo"

# Focused analysis
"Telescope focus on ADK architecture"
"Telescope focus on database design"
"Telescope focus on performance"
```

### What You Get

```
ai_docs/documentation/[project-name]/
├── summaries/
│   ├── 2025-10-07-orchestration.md           # Multi-agent coordination plan
│   ├── 2025-10-07-agent-1-architecture.md    # Architecture specialist findings
│   ├── 2025-10-07-agent-2-backend.md         # Backend specialist analysis
│   ├── 2025-10-07-agent-3-frontend.md        # Frontend specialist review
│   ├── 2025-10-07-agent-4-devops.md          # DevOps specialist assessment
│   └── 2025-10-07-agent-5-quality.md         # Quality specialist analysis
│
├── 2025-10-07-master-documentation.md        # Complete synthesis
├── 2025-10-07-pain-points.md                 # Consolidated issues
├── 2025-10-07-recommendations.md             # Actionable improvements
└── README.md                                  # Navigation index
```

---

## 🚀 Key Features

### 1. Universal Compatibility
- **Local Codebases:** Analyze any directory on your machine
- **Remote Repositories:** Automatically clone from GitHub, GitLab, Bitbucket
- **Any Tech Stack:** Works with Next.js, React, Python, Go, Rust, and more
- **Any Architecture:** Microservices, monoliths, libraries, APIs

### 2. Focus Modes
Zero in on specific aspects:
- `ADK architecture` - Agent Development Kit patterns
- `database design` - Schema, queries, migrations
- `performance` - Bottlenecks and optimizations
- `security` - Vulnerabilities and best practices
- `API patterns` - API design and integration
- `frontend` - Component architecture and UX
- `devops` - CI/CD and infrastructure
- `testing` - Test coverage and strategies
- `real-time` - WebSocket and synchronization patterns
- `full-stack` - Complete system analysis (default)

### 3. Multi-Agent Orchestration
- **5 Specialized Agents** run in parallel
- **Architecture Specialist** - System design and component relationships
- **Backend Specialist** - APIs, databases, backend services
- **Frontend Specialist** - Components, state management, UX
- **DevOps Specialist** - CI/CD, infrastructure, deployment
- **Quality Specialist** - Testing, code quality, best practices

### 4. Organized Documentation
- **Consistent file naming:** `YYYY-MM-DD-category-title.md` format
- **Structured folders:** Summaries separate from master docs
- **Navigation index:** README with quick links to all outputs
- **Cross-referenced:** Easy to find related information

### 5. Actionable Insights
- **Pain Points:** Identified with severity (Critical, High, Medium, Low)
- **Recommendations:** Prioritized by timeline (Immediate, Short-term, Long-term)
- **Best Practices:** Extracted patterns worth replicating
- **Implementation Roadmap:** Phased approach to improvements

---

## 📖 The Power of Prompt Templates in AI Engineering

### Why Prompt Templates Matter

**Traditional AI Interaction:**
```
User: "Analyze this codebase for me"
AI: [Provides surface-level overview, misses key details, inconsistent structure]
```

**Prompt Template Approach (Telescope):**
```
User: "Telescope analyze /path/to/project"
Template: [Executes structured 5-agent orchestration]
         → Phase 0: Preparation & Context Gathering
         → Phase 1: Focus Detection & Agent Assignment
         → Phase 2: Parallel Multi-Agent Execution
         → Phase 3: Synthesis & Consolidation
         → Phase 4: Organization & Cleanup
AI: [Comprehensive, structured, reproducible analysis with 15+ documents]
```

### What Prompt Templates Enable

#### 1. **Consistency & Reproducibility**
Every analysis follows the same structure, making results comparable across projects and time.

```markdown
# Without Template:
- Analysis depth varies wildly
- Different structure each time
- Hard to compare results
- Missing critical areas

# With Template:
- Consistent depth and coverage
- Same structure every time
- Easy to compare across projects
- Comprehensive by design
```

#### 2. **Complexity Management**
Break down overwhelming tasks into manageable, specialized sub-tasks.

```markdown
# Single Agent (Overwhelming):
"Analyze everything about this 100k+ line codebase"
→ Surface-level, misses details, incomplete

# Multi-Agent Template (Manageable):
Agent 1: Focus only on architecture patterns
Agent 2: Focus only on backend and database
Agent 3: Focus only on frontend and UX
Agent 4: Focus only on DevOps and deployment
Agent 5: Focus only on quality and testing
→ Deep, thorough, comprehensive
```

#### 3. **Quality Assurance**
Templates enforce quality through required sections and structured outputs.

```markdown
# Template Requirements:
✅ Every agent MUST provide:
  - Complete file review checklist
  - Architecture overview
  - Pain points with severity ratings
  - Recommendations with priority/effort/impact
  - Specific code examples
  - Timeline estimates

# Result:
- No vague findings
- All areas covered
- Actionable outputs
- Measurable quality
```

#### 4. **Scalability**
Same template works on 100-line scripts or 1M-line enterprise systems.

```markdown
# Small Project:
Telescope → 3 agents, high-level analysis, 30 min
Result: Focused recommendations for quick wins

# Large Project:
Telescope → 5 agents, comprehensive analysis, 4 hours
Result: Complete architecture documentation + roadmap
```

#### 5. **Knowledge Capture**
Templates accumulate best practices and improve over time.

```markdown
# Template Evolution:
Version 1.0: Basic 3-agent analysis
   ↓ [Learn from 10 projects]
Version 1.1: Add security focus mode
   ↓ [Learn from 20 projects]
Version 1.2: Add comparison mode
   ↓ [Learn from 50 projects]
Version 2.0: Domain-specific agents (e-commerce, SaaS, games)

# Result: Each analysis gets better
```

### Prompt Template Design Principles

Telescope embodies these AI engineering principles:

#### 1. **Separation of Concerns**
```yaml
Orchestration Layer:
  - Coordinates agents
  - Manages workflow
  - Handles cleanup

Agent Layer:
  - Specialized analysis
  - Domain expertise
  - Independent execution

Synthesis Layer:
  - Consolidates findings
  - Identifies patterns
  - Creates master documentation
```

#### 2. **Progressive Refinement**
```yaml
Phase 0: Context (What are we analyzing?)
  ↓
Phase 1: Focus (What should we emphasize?)
  ↓
Phase 2: Analysis (Deep dive into specifics)
  ↓
Phase 3: Synthesis (Consolidate findings)
  ↓
Phase 4: Action (Prioritized recommendations)
```

#### 3. **Explicit Requirements**
```markdown
# Bad Prompt:
"Analyze the architecture"

# Template Prompt:
"You are Agent 1: Architecture Specialist

Required Analysis:
1. Agent Hierarchy Map (visual representation)
2. Session State Analysis (all keys documented)
3. Pattern Assessment (✅ good, ⚠️ anti-patterns)
4. Pain Points (❌ with severity: Critical/High/Medium/Low)
5. Focus Areas (⭐ with priority/effort/impact)

Output Format:
- File: 2025-10-07-agent-1-architecture.md
- Sections: [10 required sections listed]
- Examples: Provide code samples for key findings
- Metrics: Quantify where possible"
```

#### 4. **Context Preservation**
```markdown
# Template maintains context through:
- Orchestration document (shared coordination)
- Consistent file naming (easy reference)
- Cross-linking (related findings)
- State passing (agent → synthesis)
```

#### 5. **Failure Prevention**
```markdown
# Template includes:
- Validation (target exists before starting)
- Checkpoints (verify each phase completes)
- Error handling (cleanup on failure)
- Fallbacks (graceful degradation)
- Documentation (what went wrong, how to fix)
```

### Real-World Impact

**Before Telescope (Ad-hoc Analysis):**
- ⏱️ **Time:** 2-3 days for senior engineer to manually review
- 📊 **Coverage:** ~40% of codebase (time constraints)
- 📝 **Documentation:** Scattered notes, inconsistent format
- 🔄 **Repeatability:** Hard to compare across projects
- 💡 **Insights:** Surface-level, misses patterns

**After Telescope (Template-Driven):**
- ⏱️ **Time:** 4-6 hours for complete analysis
- 📊 **Coverage:** 100% of codebase (systematic approach)
- 📝 **Documentation:** 15+ structured documents
- 🔄 **Repeatability:** Identical process every time
- 💡 **Insights:** Deep patterns, cross-domain findings, actionable roadmap

**ROI Example:**
```
Senior Engineer Hourly Rate: $150/hr

Manual Analysis:
- Time: 16 hours (2 days)
- Cost: $2,400
- Coverage: 40%
- Documentation: Minimal

Telescope Analysis:
- Time: 6 hours (AI + validation)
- Cost: $900 engineering time + $50 AI costs
- Coverage: 100%
- Documentation: Comprehensive

Savings per Analysis: $1,450
Additional Value: 2.5x coverage, reusable docs
```

---

## 🎓 Learning from Telescope

Telescope is a **teaching tool** for prompt engineering best practices:

### 1. Orchestration Pattern
Study `telescope.md` to learn:
- How to coordinate multiple AI agents
- Phase-based workflow design
- State management across agents
- Parallel vs. sequential execution

### 2. Specialization Pattern
Each agent demonstrates:
- Domain-specific expertise
- Focused analysis scope
- Consistent output structure
- Clear success criteria

### 3. Synthesis Pattern
The synthesis agent shows:
- Cross-referencing multiple sources
- Pattern identification
- Priority assignment
- Actionable recommendation generation

### 4. Template Reusability
Telescope's design enables:
- Easy customization (focus modes)
- Extension (new agent types)
- Adaptation (domain-specific analysis)
- Evolution (version improvements)

---

## 📚 Use Cases

### 1. V2 Planning
**Scenario:** Planning major version upgrade

**Command:** `"Telescope analyze /path/to/v1"`

**Result:**
- Complete V1 architecture documentation
- Pain points become V2 requirements
- Technical debt prioritization
- Migration strategy roadmap

### 2. New Developer Onboarding
**Scenario:** Help new developers understand codebase

**Command:** `"Telescope analyze /path/to/project"`

**Result:**
- Architecture guide
- Component overview
- Development workflow documentation
- Best practices extraction

### 3. Technical Due Diligence
**Scenario:** Evaluating acquisition target or vendor code

**Command:** `"Telescope analyze https://github.com/vendor/product"`

**Result:**
- Code quality assessment
- Technical debt inventory
- Security vulnerability identification
- Scalability analysis

### 4. Performance Audit
**Scenario:** System running slow, need optimization

**Command:** `"Telescope focus on performance"`

**Result:**
- Bottleneck identification
- Caching opportunities
- Query optimization recommendations
- Infrastructure improvements

### 5. Security Review
**Scenario:** Preparing for security audit

**Command:** `"Telescope focus on security"`

**Result:**
- Vulnerability identification
- Authentication pattern review
- Data protection assessment
- Compliance gap analysis

### 6. ADK Architecture Review
**Scenario:** Optimizing Agent Development Kit implementation

**Command:** `"Telescope focus on ADK architecture"`

**Result:**
- Agent hierarchy analysis
- Session state documentation
- Callback pattern assessment
- Best practices vs. anti-patterns

---

## 🛠️ Installation & Setup

### Prerequisites
- AI agent system capable of multi-agent orchestration
- Git (for remote repository cloning)
- File system access

### Setup
1. **Clone Telescope repository:**
   ```bash
   git clone https://github.com/yourusername/telescope.git
   cd telescope
   ```

2. **Copy template to your project:**
   ```bash
   mkdir -p /path/to/your-project/ai_docs/dev_templates
   cp telescope.md /path/to/your-project/ai_docs/dev_templates/
   ```

3. **Run analysis:**
   ```
   "Telescope analyze /path/to/your-project"
   ```

### First-Time Configuration
No configuration needed! Telescope auto-detects:
- Tech stack
- Framework
- Architecture patterns
- Directory structure

---

## 📋 Focus Modes Reference

| Focus Mode | Agents | Analysis Emphasis |
|------------|--------|-------------------|
| `ADK architecture` | 1, 2 | Agent patterns, hierarchies, sessions, callbacks |
| `database design` | 2 | Schema, queries, migrations, performance |
| `performance` | 2, 5 | Bottlenecks, optimization, scalability |
| `security` | 2, 4 | Vulnerabilities, auth, data protection |
| `API patterns` | 2, 3 | API design, error handling, versioning |
| `frontend` | 3 | Components, state management, UX |
| `devops` | 4 | CI/CD, infrastructure, deployment |
| `testing` | 5 | Test coverage, strategies, quality |
| `real-time` | 1, 2, 3 | WebSocket, sync patterns, state updates |
| `full-stack` | 1, 2, 3, 4, 5 | Complete system analysis (default) |

---

## 🏗️ Advanced Features

### Multi-Repository Analysis
Analyze multiple repos together:
```bash
"Telescope analyze https://github.com/user/frontend https://github.com/user/backend"
```

### Comparison Mode
Compare two versions:
```bash
"Telescope compare https://github.com/user/repo@v1.0 https://github.com/user/repo@v2.0"
```

### Incremental Analysis
Re-analyze with different focus:
```bash
# First: Full analysis
"Telescope analyze /path/to/project"

# Later: Focused deep-dive
"Telescope focus on database design"
```

### Custom Agent Configuration
Use more agents for complex projects:
```bash
"Telescope analyze /path --agents 7"
```

---

## 📊 Output Structure

### File Naming Convention
All files follow: `YYYY-MM-DD-category-title.md`

Examples:
- `2025-10-07-orchestration.md`
- `2025-10-07-agent-1-architecture.md`
- `2025-10-07-master-documentation.md`
- `2025-10-07-pain-points.md`
- `2025-10-07-recommendations.md`

### Folder Structure
```
ai_docs/documentation/[project-name]/
├── summaries/                  # Individual agent outputs
│   ├── [DATE]-orchestration.md
│   ├── [DATE]-agent-1-architecture.md
│   ├── [DATE]-agent-2-backend.md
│   ├── [DATE]-agent-3-frontend.md
│   ├── [DATE]-agent-4-devops.md
│   └── [DATE]-agent-5-quality.md
│
├── [DATE]-master-documentation.md     # Synthesis
├── [DATE]-pain-points.md              # Issues
├── [DATE]-recommendations.md          # Actions
├── [DATE]-architecture-diagrams.md    # Visuals
└── README.md                          # Index
```

---

## 🎯 Example Output

### Pain Point Example
```markdown
### ❌ Pain Point 1: Missing State Documentation

- **Problem:** Session state keys used throughout codebase but structure undocumented
- **Location:** All agents, multiple files
- **Impact:** Developers don't know available data, hard to debug, breaking changes risky
- **Severity:** High
- **Recommendation:**
  1. Create `docs/session-state-spec.md`
  2. Document each key with type, structure, creator, consumers
  3. Add TypeScript interfaces
  4. Include JSON examples
- **Effort:** 4 hours
- **Value:** High (improves developer experience immediately)
```

### Recommendation Example
```markdown
### ⭐ Focus Area 1: Implement Structured Outputs

- **Priority:** High
- **Effort:** Medium
- **Impact:** High
- **Description:** Replace free-form text responses with Pydantic schemas
- **Rationale:**
  - Current parsing fragile (breaks on format changes)
  - Difficult to validate responses
  - Inconsistent outputs across runs
- **Implementation:**
  ```python
  class ClueOutput(BaseModel):
    clue: str = Field(description="Generated clue")
    confidence: float = Field(ge=0.0, le=1.0)
    reasoning: str

  clue_agent = LlmAgent(
    output_schema=ClueOutput,
    instruction="Generate clue..."
  )
  ```
- **Success Criteria:**
  - All agents use structured outputs
  - Zero parsing errors
  - Consistent format
```

---

## 🤝 Contributing

We welcome contributions to improve Telescope!

### Ways to Contribute
1. **New Focus Modes** - Add domain-specific analysis patterns
2. **Agent Specializations** - Create new agent types for specific domains
3. **Template Improvements** - Enhance existing prompts for better analysis
4. **Documentation** - Improve guides and examples
5. **Bug Reports** - Report issues or edge cases

### Contribution Process
1. Fork the repository
2. Create feature branch (`git checkout -b feature/new-focus-mode`)
3. Make changes
4. Test with real codebases
5. Submit pull request

---

## 📝 License

MIT License - See [LICENSE](LICENSE) file for details

---

## 🙏 Acknowledgments

Telescope was inspired by:
- **Multi-agent orchestration patterns** from production AI systems
- **ADK (Agent Development Kit)** architecture best practices
- **Real-world codebase review challenges** faced by development teams
- **The power of structured prompts** in AI engineering

---

## 📞 Support

- **Issues:** [GitHub Issues](https://github.com/yourusername/telescope/issues)
- **Discussions:** [GitHub Discussions](https://github.com/yourusername/telescope/discussions)
- **Email:** your.email@example.com

---

## 🗺️ Roadmap

### Version 1.1 (Coming Soon)
- [ ] AI-powered focus detection (auto-detect what to analyze)
- [ ] Interactive HTML reports
- [ ] Diff analysis (changes between commits)
- [ ] Custom agent plugins

### Version 2.0 (Future)
- [ ] Real-time monitoring
- [ ] Team dashboards
- [ ] Continuous codebase health tracking
- [ ] Integration with popular IDEs

---

## 💡 Pro Tips

1. **Start Broad, Then Focus**
   - First run: `"Telescope analyze /path"` (full analysis)
   - Then: `"Telescope focus on [specific topic]"` (deep dive)

2. **Use Focus Modes for Quick Wins**
   - Performance issues? → `focus on performance`
   - Planning refactor? → `focus on architecture`
   - Security audit? → `focus on security`

3. **Compare Before/After**
   - Before refactor: `"Telescope analyze /path"`
   - After refactor: `"Telescope analyze /path"`
   - Compare outputs to validate improvements

4. **Share with Team**
   - Commit Telescope outputs to repo
   - Use as onboarding documentation
   - Reference in architecture decisions

5. **Iterate on Findings**
   - Address critical pain points first
   - Re-run analysis after fixes
   - Track improvements over time

---

**Telescope 🔭 - Illuminate your codebase**

*Built with the power of prompt templates and multi-agent AI engineering*
