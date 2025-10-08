# Focus Mode: Database Design

## Description
Comprehensive analysis of database architecture, schema design, query patterns, migrations, indexing strategies, and performance optimization for data persistence layers.

## Active Agents
- Database Agent (primary)
- Performance Agent
- Security Agent
- Code Quality Agent

## Core Focus Areas

### 1. Schema Design & Data Modeling
**Priority: CRITICAL**

Analyze database schema structure and data modeling decisions:
- Table design and relationships
- Normalization vs denormalization
- Data types and constraints
- Primary and foreign key design
- Naming conventions

**Key Patterns to Identify:**
- Entity-relationship patterns
- One-to-many, many-to-many relationships
- Inheritance mapping strategies
- Composite keys and surrogate keys
- Temporal data patterns

**Questions to Answer:**
- Is the schema properly normalized?
- Are relationships clearly defined?
- Are data types appropriate for the use case?
- Are constraints properly enforced?
- Is the schema flexible for future changes?

### 2. Query Patterns & Optimization
**Priority: CRITICAL**

Evaluate how data is queried and manipulated:
- SELECT query patterns
- JOIN strategies
- Subquery usage
- Aggregation patterns
- Update/delete patterns

**Key Patterns to Identify:**
- N+1 query problems
- Unnecessary joins
- Missing query optimizations
- Inefficient WHERE clauses
- Query result caching opportunities

**Questions to Answer:**
- Are queries optimized for common access patterns?
- Are there unnecessary database round-trips?
- Are queries using appropriate indexes?
- Are there opportunities for query batching?
- Is query complexity justified?

### 3. Indexing Strategy
**Priority: HIGH**

Analyze index design and usage:
- Index coverage for common queries
- Composite index design
- Unique indexes and constraints
- Full-text search indexes
- Index maintenance overhead

**Key Patterns to Identify:**
- Missing indexes on foreign keys
- Redundant or duplicate indexes
- Over-indexing scenarios
- Index usage in query plans
- Partial index opportunities

**Questions to Answer:**
- Are critical queries properly indexed?
- Are indexes being used by the query optimizer?
- Is there index bloat or fragmentation?
- Are covering indexes used appropriately?
- Do indexes match query patterns?

### 4. Migration Management
**Priority: HIGH**

Review database migration strategies:
- Migration versioning
- Forward and backward compatibility
- Data transformation logic
- Migration rollback procedures
- Migration testing approaches

**Key Patterns to Identify:**
- Reversible vs irreversible migrations
- Data migration patterns
- Schema evolution strategies
- Zero-downtime migration techniques
- Migration dependency chains

**Questions to Answer:**
- Are migrations properly versioned?
- Can migrations be rolled back safely?
- Is data preserved during schema changes?
- Are migrations tested before deployment?
- Is migration order correct?

### 5. Transaction Management
**Priority: HIGH**

Examine transaction handling and consistency:
- Transaction boundaries
- Isolation levels
- Locking strategies
- Deadlock prevention
- Distributed transactions

**Key Patterns to Identify:**
- Transaction scope issues
- Nested transaction handling
- Long-running transactions
- Transaction retry logic
- Optimistic vs pessimistic locking

**Questions to Answer:**
- Are transaction boundaries appropriate?
- Is the isolation level correct for the use case?
- Are deadlocks possible and handled?
- Are transactions kept short and focused?
- Is rollback logic properly implemented?

### 6. Connection Management
**Priority: MEDIUM**

Analyze database connection handling:
- Connection pooling configuration
- Connection lifecycle management
- Connection leak prevention
- Connection timeout settings
- Connection retry logic

**Key Patterns to Identify:**
- Connection pool sizing
- Connection leak scenarios
- Connection establishment overhead
- Connection state management
- Connection validation strategies

**Questions to Answer:**
- Is connection pooling properly configured?
- Are connections properly closed/released?
- Is the connection pool size appropriate?
- Are connection errors handled gracefully?
- Is connection state properly reset?

## Analysis Emphasis

### Database Design Quality Indicators

**GOOD Implementation:**
- Well-normalized schema with justified denormalization
- Appropriate data types and constraints
- Comprehensive indexing strategy
- Efficient query patterns
- Proper transaction boundaries
- Versioned, reversible migrations
- Optimized connection pooling
- Clear foreign key relationships
- Consistent naming conventions
- Adequate documentation

**BAD Implementation:**
- Over-normalized or severely denormalized schema
- Inappropriate data types (e.g., storing dates as strings)
- Missing or excessive indexes
- N+1 query problems
- Transaction scope issues
- Irreversible migrations without backups
- Connection leaks or pool exhaustion
- Circular foreign key dependencies
- Inconsistent naming
- Lack of constraints leading to data integrity issues

### Specific Concerns

**Schema Design:**
- Avoid EAV (Entity-Attribute-Value) anti-pattern unless necessary
- Use appropriate column types (VARCHAR vs TEXT, INT vs BIGINT)
- Enforce referential integrity with foreign keys
- Use NOT NULL constraints where appropriate
- Consider partitioning for large tables

**Query Performance:**
- Avoid SELECT * in production queries
- Use LIMIT for potentially large result sets
- Leverage database-specific features (CTEs, window functions)
- Consider materialized views for complex aggregations
- Profile slow queries regularly

**Indexing:**
- Index foreign keys by default
- Use composite indexes for multi-column queries
- Consider index selectivity
- Monitor index usage statistics
- Remove unused indexes

**Migrations:**
- Always test migrations on production-like data
- Use transactions for DDL when supported
- Plan for migration failures
- Keep migrations atomic and focused
- Document breaking changes

**Transactions:**
- Keep transactions as short as possible
- Avoid business logic in transactions
- Use appropriate isolation levels
- Handle deadlocks with retry logic
- Avoid distributed transactions when possible

## Code Review Checklist

When reviewing database code, verify:

1. **Schema Design:**
   - [ ] Tables are properly normalized
   - [ ] Relationships are clearly defined with foreign keys
   - [ ] Data types are appropriate
   - [ ] Constraints are enforced (NOT NULL, UNIQUE, CHECK)
   - [ ] Naming is consistent and descriptive

2. **Query Quality:**
   - [ ] No N+1 query problems
   - [ ] Queries use appropriate indexes
   - [ ] SELECT statements specify needed columns
   - [ ] Joins are necessary and efficient
   - [ ] Query complexity is justified

3. **Indexing:**
   - [ ] Foreign keys are indexed
   - [ ] Common query patterns are covered
   - [ ] No redundant or duplicate indexes
   - [ ] Composite index column order is optimal
   - [ ] Index maintenance is considered

4. **Migrations:**
   - [ ] Migrations are versioned sequentially
   - [ ] Migrations are reversible or have backups
   - [ ] Data transformations are correct
   - [ ] Migrations are idempotent
   - [ ] Breaking changes are documented

5. **Transactions:**
   - [ ] Transaction scope is minimal
   - [ ] Isolation level is appropriate
   - [ ] Deadlock scenarios are handled
   - [ ] Rollback logic is present
   - [ ] Error handling is comprehensive

6. **Connections:**
   - [ ] Connection pooling is configured
   - [ ] Connections are properly released
   - [ ] Connection errors are handled
   - [ ] Timeouts are configured
   - [ ] Connection leaks are prevented

## Database-Specific Patterns

### PostgreSQL
- Use JSONB for semi-structured data
- Leverage array types when appropriate
- Use EXPLAIN ANALYZE for query optimization
- Consider table partitioning for large datasets
- Use CTEs for complex queries

### MySQL/MariaDB
- Choose appropriate storage engine (InnoDB vs MyISAM)
- Use EXPLAIN for query analysis
- Consider table partitioning
- Optimize buffer pool size
- Use prepared statements

### SQLite
- Use Write-Ahead Logging (WAL) mode
- Optimize PRAGMA settings
- Consider VACUUM for maintenance
- Use transactions for bulk writes
- Be aware of type affinity

### MongoDB
- Design schema for query patterns
- Use indexes on query fields
- Leverage aggregation pipeline
- Consider sharding strategy
- Use appropriate read/write concerns

## Performance Metrics to Monitor

- Query execution time (p50, p95, p99)
- Connection pool utilization
- Index hit ratio
- Cache hit ratio
- Transaction rollback rate
- Deadlock frequency
- Table scan frequency
- Slow query log entries
- Database size growth
- Replication lag (if applicable)

## Security Considerations

- Use parameterized queries (prevent SQL injection)
- Implement least-privilege access control
- Encrypt sensitive data at rest and in transit
- Audit database access logs
- Regularly update database software
- Secure database credentials (use secrets management)
- Implement row-level security when needed
- Validate and sanitize user inputs
- Monitor for unusual query patterns

## Documentation Requirements

Database documentation should include:
- Entity-Relationship Diagrams (ERD)
- Schema documentation with column descriptions
- Index strategy documentation
- Query performance baselines
- Migration procedures
- Backup and restore procedures
- Scaling strategies
- Common query patterns
- Data retention policies
