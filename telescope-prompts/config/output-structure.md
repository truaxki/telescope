# Telescope Output Structure

> **File organization, naming conventions, and output specifications**

## Base Directory Structure

```
ai_docs/documentation/[project-name]/
├── README.md                              # Index document (created in Phase 6)
│
├── summaries/
│   ├── [DATE]-orchestration.md            # Orchestration plan (Phase 3)
│   ├── [DATE]-agent-1-architecture.md     # Agent outputs (Phase 4)
│   ├── [DATE]-agent-2-backend.md
│   ├── [DATE]-agent-3-frontend.md
│   ├── [DATE]-agent-4-devops.md
│   └── [DATE]-agent-5-quality.md
│
├── [DATE]-master-documentation.md         # Complete synthesis (Phase 5)
├── [DATE]-pain-points.md                  # Consolidated issues (Phase 5)
├── [DATE]-recommendations.md              # Actionable improvements (Phase 5)
└── [DATE]-architecture-diagrams.md        # Visual documentation (Phase 5)
```

## File Naming Convention

### Pattern

```
[DATE]-[category]-[title].md

Components:
- DATE: YYYY-MM-DD (e.g., 2025-10-07)
- category: Document type (see categories below)
- title: Descriptive kebab-case title

Examples:
- 2025-10-07-orchestration.md
- 2025-10-07-agent-1-architecture.md
- 2025-10-07-master-documentation.md
- 2025-10-07-pain-points.md
```

### Date Format

```python
from datetime import date

def get_date_prefix() -> str:
    """Get current date in YYYY-MM-DD format."""
    return date.today().strftime("%Y-%m-%d")

# Example: "2025-10-07"
```

### Project Name Format

```python
def format_project_name(name: str) -> str:
    """Format project name for directory structure."""
    return name.lower().replace(' ', '-').replace('_', '-')

# Examples:
# "MyApp" → "myapp"
# "My App" → "my-app"
# "my_app" → "my-app"
```

---

## Document Categories

### 1. Orchestration

**Purpose:** Multi-agent coordination plan

**Naming:**
```
summaries/[DATE]-orchestration.md
```

**Created by:** Orchestrator in Phase 3

**Template:** See `steps/03-orchestration.md`

---

### 2. Agent Summaries

**Purpose:** Individual agent findings

**Naming:**
```
summaries/[DATE]-agent-[N]-[specialization].md

Where:
- N: Agent number (1-5)
- specialization: Agent domain (architecture, backend, frontend, devops, quality)

Examples:
- summaries/2025-10-07-agent-1-architecture.md
- summaries/2025-10-07-agent-2-backend.md
- summaries/2025-10-07-agent-3-frontend.md
- summaries/2025-10-07-agent-4-devops.md
- summaries/2025-10-07-agent-5-quality.md
```

**Created by:** Each agent in Phase 4

**Templates:** See `agents/agent-[N]-[specialization].md`

---

### 3. Master Documentation

**Purpose:** Complete synthesis of all findings

**Naming:**
```
[DATE]-master-documentation.md
```

**Created by:** Synthesis agent in Phase 5

**Template:** See `agents/synthesis-agent.md`

**Contents:**
- Executive summary
- Focus analysis (if focused mode)
- Architecture overview
- Technology stack
- Component analysis
- Consolidated pain points
- Prioritized recommendations
- Best practices identified
- Implementation roadmap
- Appendix with agent sources

---

### 4. Pain Points

**Purpose:** Consolidated issues and problems

**Naming:**
```
[DATE]-pain-points.md
```

**Created by:** Synthesis agent in Phase 5

**Format:**
```markdown
# Pain Points - [Project Name]

> **Date:** [DATE]
> **Total Issues:** [count]

---

## Critical Issues

### ❌ [Title]
- **Problem:** [Description]
- **Location:** [File:line]
- **Impact:** [Effect]
- **Severity:** Critical
- **Recommendation:** [Fix]

---

## High Priority Issues
[Same format]

## Medium Priority Issues
[Same format]

## Low Priority Issues
[Same format]
```

---

### 5. Recommendations

**Purpose:** Actionable improvements organized by timeline

**Naming:**
```
[DATE]-recommendations.md
```

**Created by:** Synthesis agent in Phase 5

**Format:**
```markdown
# Recommendations - [Project Name]

> **Date:** [DATE]
> **Total Recommendations:** [count]

---

## Immediate Actions (Week 1)

### ⭐ [Title]
- **Priority:** Critical/High/Medium/Low
- **Effort:** Low/Medium/High
- **Impact:** Low/Medium/High
- **Description:** [What to do]
- **Rationale:** [Why]
- **Steps:** [How]

---

## Short-term Actions (Month 1)
[Same format]

## Long-term Actions (Quarter 1+)
[Same format]
```

---

### 6. Architecture Diagrams

**Purpose:** Visual representations of system architecture

**Naming:**
```
[DATE]-architecture-diagrams.md
```

**Created by:** Synthesis agent in Phase 5 (optional)

**Format:**
```markdown
# Architecture Diagrams - [Project Name]

> **Date:** [DATE]

---

## System Architecture

```
[ASCII diagram or Mermaid diagram]
```

## Agent Hierarchy

```
[Agent structure diagram]
```

## Data Flow

```
[Data flow diagram]
```
```

---

### 7. Index (README)

**Purpose:** Quick navigation and summary

**Naming:**
```
README.md
```

**Created by:** Orchestrator in Phase 6

**Template:**
```markdown
# Telescope Analysis: [Project Name]

> **Analysis Date:** [DATE]
> **Analysis Type:** [Full Stack / Focused]
> **Focus Areas:** [List if focused]

---

## Quick Links

### Master Documentation
- 📄 **[Master Documentation]([DATE]-master-documentation.md)**
- ❌ **[Pain Points]([DATE]-pain-points.md)**
- ⭐ **[Recommendations]([DATE]-recommendations.md)**

### Agent Summaries
- 🔍 **[Orchestration](summaries/[DATE]-orchestration.md)**
- 1️⃣ **[Architecture](summaries/[DATE]-agent-1-architecture.md)**
- 2️⃣ **[Backend](summaries/[DATE]-agent-2-backend.md)**
- 3️⃣ **[Frontend](summaries/[DATE]-agent-3-frontend.md)**
- 4️⃣ **[DevOps](summaries/[DATE]-agent-4-devops.md)**
- 5️⃣ **[Quality](summaries/[DATE]-agent-5-quality.md)**

---

## Analysis Summary

**Project:** [Name]
**Tech Stack:** [Technologies]
**Analysis Mode:** [Mode]

**Top Findings:**
- [Finding 1]
- [Finding 2]
- [Finding 3]

**Top Priorities:**
1. [Priority 1]
2. [Priority 2]
3. [Priority 3]

---

**Telescope Version:** 1.0
**Analysis Duration:** [Time]
```

---

## Path Construction

### Functions

```python
from pathlib import Path
from datetime import date

class OutputPaths:
    """Construct output paths for Telescope analysis."""

    def __init__(self, project_name: str):
        self.project_name = self._format_name(project_name)
        self.date_str = date.today().strftime("%Y-%m-%d")
        self.base_path = Path("ai_docs") / "documentation" / self.project_name

    @staticmethod
    def _format_name(name: str) -> str:
        """Format project name for directory."""
        return name.lower().replace(' ', '-').replace('_', '-')

    @property
    def summaries_dir(self) -> Path:
        """Get summaries directory path."""
        return self.base_path / "summaries"

    def orchestration(self) -> Path:
        """Get orchestration file path."""
        return self.summaries_dir / f"{self.date_str}-orchestration.md"

    def agent_summary(self, agent_num: int, specialization: str) -> Path:
        """Get agent summary file path."""
        return self.summaries_dir / f"{self.date_str}-agent-{agent_num}-{specialization}.md"

    def master_doc(self) -> Path:
        """Get master documentation file path."""
        return self.base_path / f"{self.date_str}-master-documentation.md"

    def pain_points(self) -> Path:
        """Get pain points file path."""
        return self.base_path / f"{self.date_str}-pain-points.md"

    def recommendations(self) -> Path:
        """Get recommendations file path."""
        return self.base_path / f"{self.date_str}-recommendations.md"

    def readme(self) -> Path:
        """Get README file path."""
        return self.base_path / "README.md"

    def ensure_dirs(self):
        """Create all necessary directories."""
        self.base_path.mkdir(parents=True, exist_ok=True)
        self.summaries_dir.mkdir(exist_ok=True)


# Usage:
paths = OutputPaths("MyProject")
paths.ensure_dirs()

orchestration_path = paths.orchestration()
agent_1_path = paths.agent_summary(1, "architecture")
master_path = paths.master_doc()
```

---

## Common Header Template

### For All Documents

```markdown
# [Document Title] - [Project Name]

> **Date:** [YYYY-MM-DD]
> **Analysis Type:** [Full Stack / Focused - Mode Name]
> **Specialization:** [Agent specialization if agent summary]

---

[Document content]

---

**Telescope Version:** 1.0
**Analysis Completed:** [Timestamp]
```

---

## Markdown Formatting Standards

### Headings

```markdown
# H1 - Document Title
## H2 - Major Sections
### H3 - Subsections
#### H4 - Details
```

### Pain Points

```markdown
### ❌ Pain Point: [Title]
- **Problem:** [Description]
- **Location:** `file/path.ts:123`
- **Impact:** [Effect on system]
- **Severity:** Critical | High | Medium | Low
- **Recommendation:** [How to fix]
```

### Recommendations

```markdown
### ⭐ Focus Area: [Title]
- **Priority:** Critical | High | Medium | Low
- **Effort:** Low | Medium | High
- **Impact:** Low | Medium | High
- **Description:** [What to improve]
- **Rationale:** [Why it matters]
- **Implementation:** [How to do it]
```

### Code Blocks

```markdown
**Example:**
```typescript
// Code example here
const example = "formatted code";
```
```

### File References

```markdown
- **Location:** `src/agents/root_agent.ts:15`
- **File:** `/functions/src/tools/game_tools.ts`
```

### Status Indicators

```markdown
✅ Complete
🔄 In Progress
⏳ Pending
❌ Failed / Problem
⚠️ Warning / Anti-pattern
💡 Opportunity
⭐ Recommendation
```

---

## File Size Guidelines

### Target Sizes

```yaml
orchestration:
  target: "1,000-2,000 lines"
  max: "3,000 lines"

agent_summary:
  target: "2,000-5,000 lines"
  max: "10,000 lines"

master_documentation:
  target: "10,000-20,000 lines"
  max: "30,000 lines"

pain_points:
  target: "1,000-3,000 lines"
  max: "5,000 lines"

recommendations:
  target: "1,000-3,000 lines"
  max: "5,000 lines"
```

---

## Completion Message

### After All Files Created

```markdown
## Telescope Analysis Complete ✅

📄 **Documentation created:**

**Master Documentation:**
- `ai_docs/documentation/[project-name]/[DATE]-master-documentation.md`
- `ai_docs/documentation/[project-name]/[DATE]-pain-points.md`
- `ai_docs/documentation/[project-name]/[DATE]-recommendations.md`

**Agent Summaries:**
- `ai_docs/documentation/[project-name]/summaries/[DATE]-orchestration.md`
- `ai_docs/documentation/[project-name]/summaries/[DATE]-agent-1-architecture.md`
- `ai_docs/documentation/[project-name]/summaries/[DATE]-agent-2-backend.md`
- [... for each active agent ...]

**Index:**
- `ai_docs/documentation/[project-name]/README.md`

---

📊 **Analysis Summary:**
- **Pain Points Identified:** [count]
- **Recommendations Made:** [count]
- **Files Analyzed:** [count]
- **Lines of Code:** [count]
- **Analysis Duration:** [time]

🎯 **Top 3 Priorities:**
1. [Priority 1]
2. [Priority 2]
3. [Priority 3]

---

**View full analysis:** `ai_docs/documentation/[project-name]/README.md`
```

---

**Usage:** Reference this file when writing any Telescope output document
