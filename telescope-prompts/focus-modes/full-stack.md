# Focus Mode: Full-Stack

## Description
Comprehensive, balanced analysis covering all aspects of full-stack development including frontend, backend, database, infrastructure, security, and architecture. This is the default focus mode providing broad coverage across all system layers.

## Active Agents
- Architecture Agent
- Code Quality Agent
- Security Agent
- Database Agent
- Performance Agent
- Integration Agent
- Documentation Agent

## Core Focus Areas

### 1. Frontend Architecture
**Priority: HIGH**

Analyze frontend structure and implementation:
- Component architecture and organization
- State management patterns
- UI/UX implementation
- Client-side routing
- Asset optimization

**Key Questions:**
- Is the component hierarchy logical and maintainable?
- Is state management appropriate for complexity?
- Are UI patterns consistent?
- Is the frontend responsive and accessible?
- Are assets optimized for performance?

### 2. Backend Architecture
**Priority: HIGH**

Examine backend design and implementation:
- API design and RESTful principles
- Service layer architecture
- Business logic organization
- Error handling patterns
- Middleware implementation

**Key Questions:**
- Is the API design consistent and intuitive?
- Is business logic properly separated?
- Are errors handled comprehensively?
- Is the architecture scalable?
- Are services loosely coupled?

### 3. Database Layer
**Priority: HIGH**

Review data persistence and management:
- Schema design and relationships
- Query optimization
- Migration strategy
- Data integrity constraints
- Connection management

**Key Questions:**
- Is the schema properly normalized?
- Are queries optimized with indexes?
- Are migrations versioned and reversible?
- Is data integrity enforced?
- Is connection pooling configured?

### 4. Security
**Priority: CRITICAL**

Assess security across all layers:
- Authentication and authorization
- Input validation and sanitization
- Data protection and encryption
- API security
- Security headers and configuration

**Key Questions:**
- Are authentication mechanisms secure?
- Is authorization checked consistently?
- Is user input validated and sanitized?
- Is sensitive data encrypted?
- Are security best practices followed?

### 5. Integration & Communication
**Priority: MEDIUM**

Evaluate system integration points:
- External API integration
- Inter-service communication
- Message passing patterns
- Event handling
- Error propagation

**Key Questions:**
- Are integrations well-designed and robust?
- Is communication between components efficient?
- Are failures handled gracefully?
- Is retry logic implemented where needed?
- Are timeouts configured appropriately?

### 6. Code Quality
**Priority: HIGH**

Examine overall code quality:
- Code organization and structure
- Naming conventions and readability
- Documentation completeness
- Test coverage and quality
- Technical debt assessment

**Key Questions:**
- Is the code readable and maintainable?
- Are naming conventions consistent?
- Is the code well-documented?
- Are tests comprehensive?
- What technical debt exists?

### 7. Performance
**Priority: MEDIUM**

Analyze performance characteristics:
- Response time optimization
- Resource utilization
- Caching strategies
- Database query performance
- Frontend rendering efficiency

**Key Questions:**
- Are response times acceptable?
- Is caching used effectively?
- Are database queries optimized?
- Is the frontend performant?
- Are resources used efficiently?

### 8. Deployment & Infrastructure
**Priority: MEDIUM**

Review deployment and infrastructure concerns:
- Build and deployment processes
- Environment configuration
- Dependency management
- Logging and monitoring
- Scalability considerations

**Key Questions:**
- Is the deployment process automated?
- Are environments properly configured?
- Are dependencies managed correctly?
- Is logging comprehensive?
- Can the system scale?

## Analysis Emphasis

### Full-Stack Quality Indicators

**GOOD Implementation:**
- Clear separation of concerns across layers
- Consistent coding patterns and conventions
- Comprehensive error handling
- Well-documented APIs and components
- Secure authentication and authorization
- Optimized database queries with indexes
- Effective caching strategies
- Proper input validation throughout
- Comprehensive test coverage
- Clean, readable, maintainable code
- Automated deployment processes
- Good logging and monitoring

**BAD Implementation:**
- Mixed concerns and tight coupling
- Inconsistent patterns across codebase
- Poor or missing error handling
- Inadequate documentation
- Security vulnerabilities (IDOR, XSS, injection)
- Unoptimized queries and N+1 problems
- No caching or ineffective caching
- Missing input validation
- Low test coverage or no tests
- Difficult to read and maintain code
- Manual deployment processes
- Insufficient logging

### Balanced Priorities

This focus mode aims for balanced coverage:
- **Critical:** Security fundamentals, data integrity
- **High:** Core functionality, code quality, major architectural decisions
- **Medium:** Performance optimization, integration patterns, infrastructure
- **Low:** Minor refactoring, cosmetic improvements

## Code Review Checklist

Comprehensive review across all areas:

### Frontend
- [ ] Components are properly organized
- [ ] State management is appropriate
- [ ] UI is responsive and accessible
- [ ] Assets are optimized
- [ ] Error states are handled
- [ ] Loading states are shown

### Backend
- [ ] API design is RESTful and consistent
- [ ] Business logic is properly layered
- [ ] Errors are handled and logged
- [ ] Input validation is comprehensive
- [ ] Responses are properly formatted

### Database
- [ ] Schema is normalized appropriately
- [ ] Queries use indexes
- [ ] Migrations are reversible
- [ ] Foreign keys are defined
- [ ] Connection pooling is used

### Security
- [ ] Authentication is secure
- [ ] Authorization is checked
- [ ] Input is validated
- [ ] Output is encoded
- [ ] Secrets are not in code
- [ ] HTTPS is enforced
- [ ] Security headers are set

### Testing
- [ ] Unit tests cover core logic
- [ ] Integration tests verify flows
- [ ] Edge cases are tested
- [ ] Mocks are used appropriately
- [ ] Tests are maintainable

### Performance
- [ ] No obvious bottlenecks
- [ ] Caching is used where beneficial
- [ ] Database queries are optimized
- [ ] No N+1 query problems
- [ ] Resources are properly released

### Code Quality
- [ ] Code is readable and clear
- [ ] Naming is consistent and descriptive
- [ ] Functions are focused and small
- [ ] Duplications are minimized
- [ ] Comments explain why, not what
- [ ] Documentation is adequate

### Integration
- [ ] External APIs are properly integrated
- [ ] Failures are handled gracefully
- [ ] Retries are implemented where needed
- [ ] Timeouts are configured
- [ ] Errors are logged appropriately

## Common Patterns to Identify

### Positive Patterns
- MVC/MVVM architecture
- Repository pattern for data access
- Service layer for business logic
- Dependency injection
- Factory and builder patterns
- Observer/event patterns
- Middleware/interceptor patterns
- DTO pattern for API responses

### Anti-Patterns
- God objects (too many responsibilities)
- Circular dependencies
- Magic numbers and strings
- Global state
- Copy-paste code duplication
- Premature optimization
- Golden hammer (one solution for everything)
- Spaghetti code

## Layer-Specific Considerations

### Frontend Layer
- Component reusability
- State management complexity
- Browser compatibility
- Accessibility (WCAG)
- Performance (bundle size, load time)
- User experience consistency

### API Layer
- RESTful design principles
- Versioning strategy
- Rate limiting
- API documentation (OpenAPI/Swagger)
- Error response format
- Pagination implementation

### Business Logic Layer
- Domain model design
- Validation rules
- Business rule enforcement
- Transaction boundaries
- Service orchestration

### Data Access Layer
- ORM usage and configuration
- Query optimization
- Transaction management
- Connection pooling
- Data mapping

### Infrastructure Layer
- Configuration management
- Secrets management
- Logging and monitoring
- Deployment automation
- Scaling strategy

## System-Wide Concerns

### Error Handling
- Consistent error response format
- Appropriate HTTP status codes
- Error logging and tracking
- User-friendly error messages
- Stack traces in development only

### Logging
- Structured logging format
- Appropriate log levels
- No sensitive data in logs
- Correlation IDs for tracing
- Centralized log aggregation

### Configuration
- Environment-based configuration
- Secrets in secure storage
- Configuration validation
- Sensible defaults
- Documentation of settings

### Testing Strategy
- Unit tests for business logic
- Integration tests for APIs
- End-to-end tests for critical flows
- Performance tests for bottlenecks
- Security tests for vulnerabilities

## Documentation Requirements

Full-stack documentation should include:
- System architecture diagram
- API documentation (endpoints, parameters, responses)
- Database schema documentation
- Setup and installation instructions
- Deployment procedures
- Environment configuration guide
- Security considerations
- Performance baselines
- Testing strategy
- Troubleshooting guide

## Review Scope

This focus mode provides:
- **Breadth:** Coverage across all system layers
- **Balance:** Equal weight to frontend, backend, and data layers
- **Comprehensiveness:** Security, performance, and quality considerations
- **Practicality:** Focus on real-world concerns and best practices

Use this mode when:
- Initial codebase review is needed
- No specific problem area is identified
- Comprehensive assessment is required
- Understanding overall system health
- Onboarding to a new project
