# Telescope 🔭

> Point Telescope at a codebase and it will map it out for you — architecture, tradeoffs, and clear next steps.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Version](https://img.shields.io/badge/version-2.0-blue.svg)](https://github.com/yourusername/telescope)

---

## What is Telescope?

Telescope is a modular, template-driven system that reads a codebase and produces approachable documentation: architecture, component overviews, risks, and recommendations. Under the hood, it runs a small “team” of specialist agents in parallel for in depth documentation.

**Why it works:** v2.0 uses a modular prompt system that keeps each agent focused and light on context — typically an 80–85% reduction per agent compared to a single monolithic-prompt.

---

## Quick Start

```bash
# Analyze a local codebase
"Telescope analyze /path/to/project"

# Analyze a remote repository (initiates local repo clone)
"Telescope analyze https://github.com/user/repo"

# Run a focused deep-dive
"Telescope focus on ADK architecture"
"Telescope focus on database design"
"Telescope focus on performance"
```

**Output Structure:**
```
ai_docs/documentation/[project]/
├── summaries/
│   ├── YYYY-MM-DD-orchestration.md
│   ├── YYYY-MM-DD-agent-1-architecture.md
│   └── ... (5 specialized agent reports)
├── YYYY-MM-DD-master-documentation.md
├── YYYY-MM-DD-pain-points.md
└── YYYY-MM-DD-recommendations.md
```

---

## Key Features

### Human-friendly, structured docs
- Clear, plain-language summaries with concrete examples
- Opinions when they help; links and detail when you need them

### Modular Prompt System (v2.0)
- 25+ focused files instead of one giant prompt
- ~80% less context per agent via step-based execution
- Source prompts live in [`telescope-prompts/`](telescope-prompts/)

### Works with any codebase
- Local folders or remote Git repositories
- Framework-agnostic: Next.js, React, Python, Go, Rust, etc.
- Fits different shapes: microservices, monoliths, libraries, APIs

### Focus Modes
Target what you care about right now:
- `ADK architecture` — Agent patterns and session mechanics
- `database design` — Schema, queries, migrations
- `performance` — Bottlenecks and scalability
- `security` — Auth, data protection, vulnerabilities
- `full-stack` — End-to-end analysis (default)

### Multi-agent orchestration
Run five specialists in parallel:
1. **Architecture** — System design and boundaries
2. **Backend** — APIs, databases, services
3. **Frontend** — Components, state, UX
4. **DevOps** — CI/CD and infrastructure
5. **Quality** — Tests and code health

---

## Why prompt templates?

Without a structure:
```
User: "Analyze this codebase"
AI: [Inconsistent, shallow, misses important context]
```

With Telescope:
```
User: "Telescope analyze /path/to/project"
Template: [Coordinated 5-agent run]
AI: [Consistent, thorough, actionable]
```

What you get:
- **Consistency** — Same structure every time
- **Manageable complexity** — Break big problems into focused passes
- **Quality controls** — Required sections and cross-checks
- **Scales up** — Works for small scripts and huge repos alike
- **Knowledge capture** — Templates improve as you do

---

## Installation

### Prerequisites
- An AI agent system with multi-agent orchestration
- Git (for remote repos)
- File system access

### Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/telescope.git
   cd telescope
   ```

2. Explore the modular prompts:
   ```bash
   cd telescope-prompts
   # Start with orchestrator.md, then follow steps/
   ```

3. Run an analysis:
   ```
   "Telescope analyze /path/to/your-project"
   ```

No config required — Telescope auto-detects the stack and architecture.

---

## Using with Claude Code

### Initial setup
```bash
# Initialize Claude Code in your repository
claude init
```

### Handy commands
```bash
# Interactive mode
claude

# Ask about the codebase
claude "explain the authentication flow in this codebase"

# Work on a task
claude "add error handling to the API endpoints"

# Review changes
claude "review my changes and suggest improvements"
```

### Repository-specific examples
```bash
# Get a project overview
claude "give me an overview of this project structure"

# Find and fix issues
claude "find and fix any TypeScript errors"

# Add features
claude "add input validation to the user registration form"

# Refactor
claude "refactor the database connection logic to use connection pooling"
```

### Use Telescope through Claude Code
```bash
# Analyze this repository
claude "explain the overall architecture of the Telescope project"

# Run a focused pass
claude "Telescope focus on ADK architecture"

# Generate documentation
claude "Telescope analyze /path/to/your-project"
```

---

## Focus Modes Reference

| Mode | Agents | Focus Areas |
|------|--------|-------------|
| `ADK architecture` | 1, 2 | Agent patterns, hierarchies, sessions, callbacks |
| `database design` | 2 | Schema, queries, migrations, performance |
| `performance` | 2, 5 | Bottlenecks, optimization, scalability |
| `security` | 2, 4 | Vulnerabilities, auth, data protection |
| `API patterns` | 2, 3 | API design, error handling, versioning |
| `frontend` | 3 | Components, state management, UX |
| `devops` | 4 | CI/CD, infrastructure, deployment |
| `testing` | 5 | Test coverage, strategies, quality |
| `real-time` | 1, 2, 3 | WebSocket, sync patterns, state updates |
| `full-stack` | 1-5 | Complete system analysis (default) |

---

## Use Cases

### V2 planning
Document V1 fully, prioritize technical debt, and map the migration path.

### New developer onboarding
Generate system overviews, component guides, and workflow notes.

### Technical due diligence
Assess code quality, risks, security, and scalability with consistent outputs.

### Performance audits
Spot bottlenecks, caching opportunities, and query/infrastructure issues.

### Security reviews
Evaluate auth patterns, data protection, and potential vulnerabilities.

### ADK architecture reviews
Examine agent hierarchies, session state, and callback patterns.

---

## Example Output

### Pain Point
```markdown
❌ Pain Point: Missing State Documentation

- **Problem:** Session state keys used throughout but structure undocumented
- **Location:** All agents, multiple files
- **Impact:** Hard to debug, risk of breaking changes
- **Severity:** High
- **Recommendation:** Create docs/session-state-spec.md with types, structure, examples
- **Effort:** 4 hours
- **Value:** High
```

### Recommendation
```markdown
⭐ Focus Area: Implement Structured Outputs

- **Priority:** High | **Effort:** Medium | **Impact:** High
- **Description:** Replace free-form text with Pydantic schemas
- **Rationale:** Current parsing fragile, difficult to validate, inconsistent
- **Implementation:**
  ```python
  class ClueOutput(BaseModel):
    clue: str = Field(description="Generated clue")
    confidence: float = Field(ge=0.0, le=1.0)
    reasoning: str
  ```
- **Success Criteria:** All agents use structured outputs, zero parsing errors
```

---

## Advanced Features

```bash
# Multi-repository analysis
"Telescope analyze https://github.com/user/frontend https://github.com/user/backend"

# Comparison mode
"Telescope compare https://github.com/user/repo@v1.0 https://github.com/user/repo@v2.0"

# Incremental analysis
"Telescope analyze /path"           # Full analysis
"Telescope focus on database"       # Later: focused deep-dive
```

---

## Modular System (v2.0)

```
telescope-prompts/
├── orchestrator.md          # Entry point
├── config/                  # Configuration files
├── steps/                   # 7 sequential phases
├── agents/                  # 6 specialized prompts
└── focus-modes/             # 5 focus templates
```

Each agent loads a small, focused prompt instead of a single 2,325-line template, which keeps the system fast and readable.

---

## Contributing

We welcome contributions! See [CONTRIBUTING.md](CONTRIBUTING.md) for:
- Adding new focus modes
- Creating agent specializations
- Improving templates
- Enhancing documentation

---

## Roadmap

### v2.0 (Current) ✅
- Modular prompt system (~80% context reduction)
- Step-based execution
- Focus mode templates

### v2.1 (Coming Soon)
- AI-powered focus detection
- Interactive HTML reports
- Diff analysis
- Custom agent plugins

### v3.0 (Future)
- Real-time monitoring
- Team dashboards
- IDE integration

---

## Documentation

- **[Quick Start](#quick-start)** — Get started fast
- **[Focus Modes](#focus-modes-reference)** — Available analysis modes
- **[Use Cases](#use-cases)** — What people use it for
- **[Migration Guide](docs/MIGRATION-GUIDE.md)** — Upgrade from v1.0 to v2.0
- **[Parallel Execution](docs/PARALLEL-EXECUTION-EXAMPLE.md)** — True multi-agent runs
- **[Reference Structure](docs/REFERENCE-STRUCTURE.md)** — Output folder layout
- **[Modular System](telescope-prompts/)** — v2.0 prompt details

---

## License

MIT License — see [LICENSE](LICENSE)

---

## Support

- **Issues:** [GitHub Issues](https://github.com/yourusername/telescope/issues)
- **Discussions:** [GitHub Discussions](https://github.com/yourusername/telescope/discussions)

---

**Telescope 🔭 — Illuminate your codebase.**

*Powered by modular prompts and multi-agent orchestration.*
