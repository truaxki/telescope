# Phase 2: Codebase Context Scan

> **Purpose:** Scan target codebase to gather context about tech stack, frameworks, and metrics

## Prerequisites

**Input:** `target_path` from Phase 0

## Scanning Tasks

### 1. Detect Tech Stack

**Scan for technology indicators:**
```bash
# Package managers & languages
- package.json          → Node.js/npm
- requirements.txt      → Python
- Gemfile              → Ruby
- pom.xml              → Java/Maven
- go.mod               → Go
- Cargo.toml           → Rust
- composer.json        → PHP
```

### 2. Detect Frameworks

**Read dependency files:**
```python
# In package.json dependencies:
- "@google/adk"        → Agent Development Kit
- "next"               → Next.js
- "react"              → React
- "express"            → Express
- "firebase"           → Firebase
```

### 3. Detect Architecture

**Scan directory structure:**
```bash
src/app/               → Next.js App Router
src/pages/             → Next.js Pages Router
functions/             → Cloud Functions
agents/                → Agent-based architecture
components/            → Component architecture
```

### 4. Count Metrics

```python
metrics = {
    "total_files": count_all_files(),
    "total_lines": count_total_lines(),
    "languages": detect_languages(),  # with percentages
    "components": count_component_files(),
    "test_files": count_test_files(),
}
```

## Output

**Phase 2 produces context object:**

```yaml
tech_stack: ["Next.js 15", "TypeScript", "Firebase"]
framework: "Next.js"
architecture_pattern: "App Router with Server Actions"
metrics:
  total_files: 145
  total_lines: 12453
  languages:
    TypeScript: 85%
    JavaScript: 10%
    CSS: 5%
  components: 23
  test_files: 18
key_dependencies:
  - "@google/adk": "^0.x"
  - "next": "15.x"
  - "firebase": "^10.x"
```

## User Communication

```markdown
## Telescope Context Scan ✅

**Project:** {project_name}
**Tech Stack:** {primary technologies}
**Framework:** {main framework}
**Architecture:** {detected pattern}

### Codebase Metrics:
- Total Files: {count}
- Total Lines: {count}
- Primary Language: {language} ({percent}%)
- Components: {count}
- Test Files: {count}

### Key Dependencies:
- {dependency}: {version}
- {dependency}: {version}

---

Next: Phase 3 - Orchestration Document
```

## Next Phase

Load `steps/03-orchestration.md`
