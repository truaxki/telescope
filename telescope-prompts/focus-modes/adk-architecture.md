# Focus Mode: ADK Architecture

## Description
Deep analysis of Agent Development Kit (ADK) architecture, focusing on agent hierarchies, session management, tool integration, callback systems, and inter-agent communication patterns.

## Active Agents
- Architecture Agent (primary)
- Code Quality Agent
- Integration Agent
- Documentation Agent

## Core Focus Areas

### 1. Agent Hierarchies & Organization
**Priority: CRITICAL**

Analyze how agents are structured, organized, and interact within the ADK framework:
- Agent class hierarchies and inheritance patterns
- Parent-child agent relationships
- Agent lifecycle management (initialization, execution, cleanup)
- Agent registration and discovery mechanisms
- Namespace organization and module structure

**Key Patterns to Identify:**
- Base agent classes and their responsibilities
- Abstract vs concrete agent implementations
- Agent factory patterns and builders
- Delegation patterns between agents
- Composite agent structures

**Questions to Answer:**
- How are agents instantiated and configured?
- What is the agent execution flow?
- How do parent agents manage child agents?
- Are agent responsibilities clearly separated?
- Is there proper encapsulation of agent logic?

### 2. Session State Management
**Priority: CRITICAL**

Examine how session state is maintained across agent interactions:
- Session initialization and teardown
- State persistence mechanisms
- Context passing between agents
- Session scope and boundaries
- State mutation patterns

**Key Patterns to Identify:**
- Stateful vs stateless agents
- Session storage mechanisms (memory, cache, database)
- State serialization/deserialization
- Context propagation strategies
- Session isolation and security

**Questions to Answer:**
- How is session state initialized?
- Where is session state stored?
- How is state shared between agents?
- Are there potential state leaks or conflicts?
- Is session cleanup handled properly?

### 3. Callback Systems
**Priority: HIGH**

Analyze callback mechanisms for agent communication and event handling:
- Callback registration patterns
- Event-driven architecture components
- Synchronous vs asynchronous callbacks
- Error handling in callbacks
- Callback lifecycle management

**Key Patterns to Identify:**
- Observer pattern implementations
- Event emitter/listener patterns
- Callback chains and composition
- Hook systems for agent extensions
- Middleware patterns

**Questions to Answer:**
- How are callbacks registered and invoked?
- What events trigger callbacks?
- How are callback errors handled?
- Are callbacks properly cleaned up?
- Is there risk of callback hell or circular dependencies?

### 4. Tool Integration
**Priority: HIGH**

Evaluate how tools are integrated into the ADK framework:
- Tool registration and discovery
- Tool invocation mechanisms
- Tool parameter validation
- Tool result handling
- Tool versioning and compatibility

**Key Patterns to Identify:**
- Tool interface definitions
- Tool adapter patterns
- Tool factory implementations
- Tool configuration management
- Tool error handling strategies

**Questions to Answer:**
- How are tools registered with agents?
- What is the tool invocation flow?
- How are tool inputs validated?
- How are tool outputs processed?
- Are tools properly isolated from agent logic?

### 5. Inter-Agent Communication
**Priority: CRITICAL**

Analyze communication patterns between agents:
- Message passing mechanisms
- Communication protocols
- Request/response patterns
- Asynchronous communication
- Communication error handling

**Key Patterns to Identify:**
- Message broker patterns
- Pub/sub implementations
- Request routing logic
- Communication middleware
- Protocol adapters

**Questions to Answer:**
- How do agents communicate with each other?
- What message formats are used?
- How are messages routed to target agents?
- How are communication failures handled?
- Is there proper timeout and retry logic?

## Analysis Emphasis

### Architecture Quality Indicators

**GOOD Implementation:**
- Clear separation of concerns between agents
- Well-defined agent interfaces and contracts
- Proper abstraction layers
- Minimal coupling between agents
- Robust error handling and recovery
- Comprehensive state management
- Efficient callback mechanisms
- Clean tool integration patterns
- Scalable communication architecture
- Clear documentation of agent responsibilities

**BAD Implementation:**
- Tight coupling between agents
- Unclear agent responsibilities
- Mixed concerns within agents
- Global state dependencies
- Fragile callback chains
- Ad-hoc tool integration
- Inconsistent communication patterns
- Poor error propagation
- Memory leaks in session management
- Circular dependencies between agents

### Specific Concerns

**Session Management:**
- Session state should be explicitly managed
- Avoid implicit state sharing between agents
- Ensure proper cleanup of session resources
- Implement session timeout mechanisms
- Provide session debugging capabilities

**Callback Design:**
- Use typed callback interfaces
- Implement proper error boundaries
- Avoid deep callback nesting
- Provide callback cancellation mechanisms
- Document callback execution order

**Tool Integration:**
- Enforce tool interface contracts
- Validate tool inputs rigorously
- Handle tool failures gracefully
- Provide tool execution context
- Support tool mocking for testing

**Communication Patterns:**
- Use message queues for async operations
- Implement backpressure mechanisms
- Provide message tracing capabilities
- Handle network partitions gracefully
- Support message replay for debugging

## Code Review Checklist

When reviewing ADK architecture code, verify:

1. **Agent Design:**
   - [ ] Agents have single, clear responsibilities
   - [ ] Agent interfaces are well-defined
   - [ ] Agent dependencies are explicit
   - [ ] Agent lifecycle is properly managed
   - [ ] Agent errors are handled appropriately

2. **Session Management:**
   - [ ] Session initialization is explicit
   - [ ] Session state is properly scoped
   - [ ] Session cleanup is guaranteed
   - [ ] Session conflicts are prevented
   - [ ] Session debugging is supported

3. **Callbacks:**
   - [ ] Callbacks are properly typed
   - [ ] Callback errors are caught
   - [ ] Callbacks are cleaned up
   - [ ] Callback ordering is documented
   - [ ] Callback performance is acceptable

4. **Tools:**
   - [ ] Tools follow consistent interfaces
   - [ ] Tool inputs are validated
   - [ ] Tool errors are handled
   - [ ] Tools are properly isolated
   - [ ] Tool execution is logged

5. **Communication:**
   - [ ] Messages are well-structured
   - [ ] Communication is asynchronous where appropriate
   - [ ] Timeouts are implemented
   - [ ] Retry logic is present
   - [ ] Communication is traceable

## Documentation Requirements

ADK architecture documentation should include:
- Agent hierarchy diagrams
- Session state flow diagrams
- Callback sequence diagrams
- Tool integration guides
- Communication protocol specifications
- Error handling strategies
- Performance considerations
- Testing approaches

## Performance Considerations

- Agent instantiation overhead
- Session state storage efficiency
- Callback execution performance
- Tool invocation latency
- Message passing throughput
- Memory usage per session
- Garbage collection impact
- Concurrency and parallelism opportunities
