# Telescope Reference Structure

> **Complete reference package: Code snapshot + Analysis documentation**

## Overview

Telescope now creates a **complete reference package** that includes both the analyzed codebase AND all documentation in a single, self-contained structure.

## Structure

```
ai_docs/reference/[project-name]/
│
├── [project-name]/                        # CODE SNAPSHOT
│   ├── src/                               # Complete source code
│   ├── package.json                       # Dependencies at analysis time
│   ├── README.md                          # Original project documentation
│   ├── apps/                              # Application code
│   ├── components/                        # Components
│   └── [all project files]                # Everything except .git, node_modules, etc.
│
└── documentation/                         # ANALYSIS DOCUMENTATION
    ├── README.md                          # Navigation index
    │
    ├── summaries/                         # Agent findings
    │   ├── 2025-10-08-orchestration.md    # Coordination plan
    │   ├── 2025-10-08-agent-1-architecture.md
    │   ├── 2025-10-08-agent-2-backend.md
    │   ├── 2025-10-08-agent-3-frontend.md
    │   ├── 2025-10-08-agent-4-devops.md
    │   └── 2025-10-08-agent-5-quality.md
    │
    ├── 2025-10-08-master-documentation.md  # Complete synthesis
    ├── 2025-10-08-pain-points.md           # Consolidated issues
    ├── 2025-10-08-recommendations.md       # Actionable improvements
    └── 2025-10-08-architecture-diagrams.md # Visual documentation
```

## Why This Structure?

### 1. Self-Contained Reference

**Problem:** Documentation referencing code that no longer exists
```
Documentation: "See the AuthManager class in auth/manager.ts:42"
Reality: File was refactored 3 months ago, line doesn't exist
```

**Solution:** Code snapshot preserved with documentation
```
Documentation: "See the AuthManager class in auth/manager.ts:42"
Code Snapshot: File exists exactly as it was when analyzed
```

### 2. Time-Travel Capability

**See exactly what was analyzed:**
- Code at specific point in time
- Dependencies at that version
- Configuration as it was
- Documentation references stay valid forever

### 3. Version Correlation

Documentation explicitly tied to code version:
```
Master Documentation Header:
> **Analysis Date:** 2025-10-08
> **Code Version:** Snapshot at ai_docs/reference/adk-walkthrough-youtube/adk-walkthrough-youtube/
> **Tech Stack:** Next.js 15, ADK, as of 2025-10-08
```

### 4. Portable Analysis

Move the entire reference folder and you have:
- Complete code
- Complete analysis
- All context
- No broken references

### 5. Multiple Analyses Over Time

```
ai_docs/reference/
├── my-project/
│   ├── my-project/                      # v1.0 code snapshot
│   └── documentation/
│       ├── 2025-01-15-master-documentation.md  # Q1 analysis
│       └── 2025-04-10-master-documentation.md  # Q2 analysis
│
├── my-project-v2/
│   ├── my-project-v2/                   # v2.0 code snapshot
│   └── documentation/
│       └── 2025-07-01-master-documentation.md  # v2 analysis
```

## What Gets Copied (Code Snapshot)

### ✅ Included

- All source code files (.js, .ts, .py, .go, etc.)
- Configuration files (package.json, tsconfig.json, .env.example)
- Documentation (README.md, docs/, etc.)
- Static assets (public/, assets/)
- Project structure (folders, organization)

### ❌ Excluded (Don't Copy)

```python
exclude_patterns = {
    '.git',               # Git history (large, not needed)
    'node_modules',       # Dependencies (can reinstall)
    '__pycache__',        # Python cache
    '.venv', 'venv',      # Virtual environments
    '.next',              # Build artifacts
    'dist', 'build',      # Compiled code
    '.cache',             # Cache files
    '*.pyc', '*.pyo',     # Compiled Python
    '.DS_Store',          # OS files
}
```

**Rationale:**
- Keep reference size manageable
- Focus on source code, not generated files
- Dependencies can be reinstalled from package.json
- Git history in .git not needed for reference

## Real Example: ADK Walkthrough

```
ai_docs/reference/adk-walkthrough-youtube/
│
├── adk-walkthrough-youtube/              # Code snapshot (22 MB)
│   ├── apps/
│   │   ├── web/                          # Next.js frontend
│   │   └── youtube-workflow-agent/       # ADK agents
│   ├── package.json                      # Dependencies preserved
│   ├── CLAUDE.md                         # Project context
│   ├── SETUP.md                          # Setup instructions
│   └── README.md                         # Original docs
│
└── documentation/                         # Analysis docs (2 MB)
    ├── summaries/
    │   ├── 2025-10-08-orchestration.md
    │   ├── 2025-10-08-agent-1-architecture.md
    │   └── 2025-10-08-agent-2-backend.md
    │
    ├── 2025-10-08-master-documentation.md
    ├── 2025-10-08-pain-points.md
    └── README.md

Total: 24 MB - Complete self-contained reference
```

## Benefits by Use Case

### Onboarding New Developers

**Give them:**
```
"Check out ai_docs/reference/our-app/"
```

**They get:**
- Complete codebase to explore
- Comprehensive architecture documentation
- Pain points to avoid
- Recommendations for improvements
- All in one place

### Technical Due Diligence

**Evaluating acquisition:**
```
1. Run Telescope analysis
2. Get complete snapshot + analysis
3. Share ai_docs/reference/target-company/ with stakeholders
4. Everyone has identical codebase + analysis
5. Code can't change mid-evaluation
```

### Architecture Documentation

**Maintaining current docs:**
```
Quarter 1: Telescope analysis
  → ai_docs/reference/app/documentation/2025-01-15-*.md

Quarter 2: Telescope analysis
  → ai_docs/reference/app/documentation/2025-04-10-*.md

Quarter 3: Telescope analysis
  → ai_docs/reference/app/documentation/2025-07-15-*.md

Track evolution: Compare documentation over time
Code snapshot: See exactly what changed
```

### Bug Investigation

**Analyzing production issue:**
```
Problem: Bug in production (v2.3.1)

1. Run Telescope on v2.3.1:
   ai_docs/reference/app-v2.3.1/

2. Analysis shows pattern causing bug

3. Code snapshot proves pattern exists in v2.3.1

4. Fix applied, new analysis:
   ai_docs/reference/app-v2.3.2/

5. Compare: Bug pattern gone in v2.3.2 snapshot
```

## Cross-Referencing in Documentation

Documentation can reference code with stable paths:

```markdown
### ❌ Pain Point 1: Missing Error Handling

**Problem:** API tools don't handle network failures

**Location:** `../../adk-walkthrough-youtube/apps/youtube-workflow-agent/youtube_workflow_agent/tools/api_tools.py:42-55`

**Code:**
```python
# See actual code at:
# ai_docs/reference/adk-walkthrough-youtube/adk-walkthrough-youtube/
#   apps/youtube-workflow-agent/youtube_workflow_agent/tools/api_tools.py

def save_workflow_output(...):
    response = requests.post(...)  # ❌ No error handling
    return response.json()
```

**Recommendation:** Add try/except with retries
```

## Storage Considerations

### Typical Sizes

| Project Type | Code Snapshot | Documentation | Total |
|--------------|---------------|---------------|-------|
| Small Library | 1-5 MB | 1-2 MB | 2-7 MB |
| Medium SaaS | 10-30 MB | 2-5 MB | 12-35 MB |
| Large Monorepo | 50-200 MB | 5-15 MB | 55-215 MB |

### Storage Best Practices

1. **Exclude build artifacts** - Keeps size down
2. **Don't track in git** - Add `ai_docs/reference/` to `.gitignore`
3. **Archive old analyses** - Compress after 90 days
4. **Cloud storage** - Upload to S3/GCS for team access

## Migration from Old Structure

### Old Structure (v1.0)

```
ai_docs/documentation/my-project/
├── summaries/
└── master-documentation.md
```

**Problem:** No code reference, documentation orphaned

### New Structure (v2.0)

```
ai_docs/reference/my-project/
├── my-project/              ← Code added!
└── documentation/
    ├── summaries/
    └── master-documentation.md
```

**Solution:** Complete self-contained reference

## Implementation

See `telescope-prompts/steps/00-preparation.md` for the complete implementation:

1. Create reference structure
2. Copy code (excluding build artifacts)
3. Create documentation folders
4. All analysis writes to `documentation/` subdirectory

---

**Telescope v2.0 - Complete Reference Architecture**

*Code + Documentation = Self-Contained Knowledge Base*
