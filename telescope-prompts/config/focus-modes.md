# Telescope Focus Modes

> **Analysis focus configurations and agent assignments**

## Overview

Focus modes allow Telescope to concentrate analysis on specific aspects of a codebase rather than analyzing everything. Each focus mode activates specific agents and emphasizes particular areas.

## Default Mode

### full_stack (Default)

**Activation:**
```bash
"Telescope analyze [target]"
# No focus keyword = full_stack mode
```

**Configuration:**
```yaml
mode: "full_stack"
agents: [1, 2, 3, 4, 5]  # All agents
depth: "comprehensive"
output_emphasis: "complete system analysis"
```

**Agents Activated:**
- Agent 1: Architecture & Design
- Agent 2: Backend & Database
- Agent 3: Frontend & UX
- Agent 4: DevOps & Infrastructure
- Agent 5: Quality & Testing

---

## Focused Modes

### 1. ADK Architecture

**Activation:**
```bash
"Telescope focus on ADK architecture"
"Telescope focus on ADK"
"Telescope focus on agents"
```

**Configuration:**
```yaml
mode: "adk_architecture"
agents: [1, 2]  # Architecture + Backend
depth: "comprehensive"
output_emphasis: "ADK patterns, agent hierarchies, session management, callbacks"

focus_areas:
  - Agent type selection and usage
  - Agent hierarchy design
  - Session state management
  - Tool integration patterns
  - Callback implementations
  - Communication patterns
  - ADK best practices
  - Anti-patterns and improvements
```

**Agent 1 Focus:**
- Agent hierarchy mapping
- Agent composition patterns
- Communication patterns
- Escalation and transfer patterns

**Agent 2 Focus:**
- Agent-database integration
- Agent-API integration
- Tool implementations
- State management vs. persistence

**Load for agents:**
```
agents/agent-1-architecture.md
agents/agent-2-backend.md
focus-modes/adk-architecture.md  # Additional context and emphasis
```

---

### 2. Database Design

**Activation:**
```bash
"Telescope focus on database design"
"Telescope focus on database"
"Telescope focus on schema"
```

**Configuration:**
```yaml
mode: "database"
agents: [2]  # Backend only
depth: "deep_dive"
output_emphasis: "schema design, query patterns, migrations"

focus_areas:
  - Table/collection structure
  - Relationships and foreign keys
  - Normalization assessment
  - Indexing strategy
  - ORM usage patterns
  - Query optimization
  - Migration strategy
  - Performance patterns
```

**Agent 2 Focus:**
- Deep database schema analysis
- Query pattern review
- Migration assessment
- Performance optimization opportunities

---

### 3. Performance

**Activation:**
```bash
"Telescope focus on performance"
"Telescope focus on optimization"
"Telescope focus on speed"
```

**Configuration:**
```yaml
mode: "performance"
agents: [2, 5]  # Backend + Quality
depth: "comprehensive"
output_emphasis: "bottlenecks, optimization opportunities, scalability"

focus_areas:
  backend:
    - API response times
    - Database query performance
    - Caching strategies
    - Connection pooling
    - Background job processing

  quality:
    - Bundle size analysis
    - Code splitting
    - Lazy loading
    - Memory management
    - Rendering performance
```

**Agent 2 Focus:**
- Backend performance bottlenecks
- Database optimization
- API efficiency

**Agent 5 Focus:**
- Code quality impact on performance
- Testing performance-critical paths
- Performance monitoring

---

### 4. Security

**Activation:**
```bash
"Telescope focus on security"
"Telescope focus on vulnerabilities"
```

**Configuration:**
```yaml
mode: "security"
agents: [2, 4]  # Backend + DevOps
depth: "comprehensive"
output_emphasis: "vulnerabilities, auth patterns, data protection"

focus_areas:
  backend:
    - Authentication implementation
    - Authorization patterns
    - Input validation
    - SQL injection risks
    - API security
    - Data encryption

  devops:
    - Secret management
    - Environment security
    - Dependency vulnerabilities
    - Deployment security
    - Network security
```

---

### 5. API Design

**Activation:**
```bash
"Telescope focus on API design"
"Telescope focus on API patterns"
"Telescope focus on endpoints"
```

**Configuration:**
```yaml
mode: "api_design"
agents: [2, 3]  # Backend + Frontend
depth: "comprehensive"
output_emphasis: "API contracts, error handling, versioning"

focus_areas:
  backend:
    - Endpoint design
    - Request/response schemas
    - Error handling
    - Versioning strategy
    - Documentation

  frontend:
    - API consumption patterns
    - Error handling
    - Loading states
    - Data synchronization
```

---

### 6. Frontend

**Activation:**
```bash
"Telescope focus on frontend"
"Telescope focus on UI"
"Telescope focus on components"
```

**Configuration:**
```yaml
mode: "frontend"
agents: [3]  # Frontend only
depth: "deep_dive"
output_emphasis: "component architecture, state management, UX"

focus_areas:
  - Component structure
  - State management
  - Routing patterns
  - UI/UX design
  - Accessibility
  - Performance optimization
  - Styling approach
  - Reusability
```

---

### 7. DevOps

**Activation:**
```bash
"Telescope focus on DevOps"
"Telescope focus on deployment"
"Telescope focus on CI/CD"
```

**Configuration:**
```yaml
mode: "devops"
agents: [4]  # DevOps only
depth: "deep_dive"
output_emphasis: "CI/CD, infrastructure, deployment"

focus_areas:
  - Deployment process
  - CI/CD pipelines
  - Infrastructure as code
  - Environment management
  - Monitoring and logging
  - Backup and recovery
  - Scaling strategy
```

---

### 8. Testing

**Activation:**
```bash
"Telescope focus on testing"
"Telescope focus on quality"
"Telescope focus on test coverage"
```

**Configuration:**
```yaml
mode: "testing"
agents: [5]  # Quality only
depth: "deep_dive"
output_emphasis: "test coverage, testing strategies, quality"

focus_areas:
  - Test coverage analysis
  - Testing strategies
  - Unit vs. integration vs. E2E
  - Test quality
  - Mocking patterns
  - Test maintainability
  - Quality metrics
```

---

### 9. Real-time

**Activation:**
```bash
"Telescope focus on real-time"
"Telescope focus on WebSocket"
"Telescope focus on sync"
```

**Configuration:**
```yaml
mode: "real_time"
agents: [1, 2, 3]  # Architecture + Backend + Frontend
depth: "comprehensive"
output_emphasis: "real-time sync, WebSocket patterns, state updates"

focus_areas:
  architecture:
    - Real-time architecture patterns
    - Event-driven design
    - Message flow

  backend:
    - WebSocket implementation
    - Real-time database patterns
    - Pub/sub patterns
    - Conflict resolution

  frontend:
    - Real-time state updates
    - Optimistic updates
    - Connection management
```

---

## Focus Mode Detection

### Keyword Matching

```python
def detect_focus_mode(command: str) -> str:
    """Detect focus mode from user command."""
    command_lower = command.lower()

    # ADK Architecture
    if any(keyword in command_lower for keyword in ['adk', 'agent', 'agent hierarchy']):
        return 'adk_architecture'

    # Database
    if any(keyword in command_lower for keyword in ['database', 'schema', 'migration']):
        return 'database'

    # Performance
    if any(keyword in command_lower for keyword in ['performance', 'optimization', 'speed', 'bottleneck']):
        return 'performance'

    # Security
    if any(keyword in command_lower for keyword in ['security', 'vulnerability', 'auth']):
        return 'security'

    # API Design
    if any(keyword in command_lower for keyword in ['api', 'endpoint', 'rest']):
        return 'api_design'

    # Frontend
    if any(keyword in command_lower for keyword in ['frontend', 'ui', 'component', 'react', 'vue']):
        return 'frontend'

    # DevOps
    if any(keyword in command_lower for keyword in ['devops', 'deployment', 'ci/cd', 'infrastructure']):
        return 'devops'

    # Testing
    if any(keyword in command_lower for keyword in ['testing', 'test', 'quality', 'coverage']):
        return 'testing'

    # Real-time
    if any(keyword in command_lower for keyword in ['real-time', 'websocket', 'sync', 'live']):
        return 'real_time'

    # Default
    return 'full_stack'
```

---

## Agent Assignment

### Based on Focus Mode

```python
focus_mode_agents = {
    'full_stack': [1, 2, 3, 4, 5],
    'adk_architecture': [1, 2],
    'database': [2],
    'performance': [2, 5],
    'security': [2, 4],
    'api_design': [2, 3],
    'frontend': [3],
    'devops': [4],
    'testing': [5],
    'real_time': [1, 2, 3],
}

def get_active_agents(focus_mode: str) -> list[int]:
    """Get agent numbers to activate for focus mode."""
    return focus_mode_agents.get(focus_mode, [1, 2, 3, 4, 5])
```

---

## Focus Mode Output

### Communication to User

```markdown
## Telescope Focus Configuration ✅

**Analysis Mode:** {mode}
**Active Agents:** {count}
**Emphasis Areas:** {list}

### Agent Assignments:

**Agent 1 - Architecture Specialist**
- Status: {Active / Inactive}
- Focus: {specific areas for this mode}

**Agent 2 - Backend Specialist**
- Status: {Active / Inactive}
- Focus: {specific areas for this mode}

[... for each agent ...]

---

Next: Phase 2 - Context Scan
```

**Example (ADK Architecture Focus):**
```markdown
## Telescope Focus Configuration ✅

**Analysis Mode:** adk_architecture
**Active Agents:** 2
**Emphasis Areas:** ADK patterns, agent hierarchies, session management, callbacks

### Agent Assignments:

**Agent 1 - Architecture Specialist**
- Status: ✅ Active
- Focus: Agent hierarchies, composition patterns, communication flows

**Agent 2 - Backend Specialist**
- Status: ✅ Active
- Focus: Agent-database integration, tool implementations, state management

**Agent 3 - Frontend Specialist**
- Status: ⏸️ Inactive (not relevant for ADK focus)

**Agent 4 - DevOps Specialist**
- Status: ⏸️ Inactive (not relevant for ADK focus)

**Agent 5 - Quality Specialist**
- Status: ⏸️ Inactive (not relevant for ADK focus)

---

Next: Phase 2 - Context Scan
```

---

## Custom Focus Modes

### Creating Custom Focus

To add a new focus mode:

1. **Create focus mode file:**
   ```
   focus-modes/my-custom-focus.md
   ```

2. **Define configuration:**
   ```yaml
   mode: "my_custom_focus"
   agents: [agent numbers to activate]
   depth: "comprehensive | deep_dive | high_level"
   output_emphasis: "what to emphasize"
   focus_areas:
     - Area 1
     - Area 2
   ```

3. **Update keyword detection:**
   Add keywords to detect this focus mode

4. **Update agent assignments:**
   Add to focus_mode_agents mapping

---

**Next Step:** Load `steps/01-focus-detection.md` for execution logic
