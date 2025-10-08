# Focus Mode: Performance

## Description
In-depth analysis of application performance, focusing on bottleneck identification, optimization opportunities, caching strategies, resource utilization, and scalability patterns.

## Active Agents
- Performance Agent (primary)
- Architecture Agent
- Database Agent
- Code Quality Agent

## Core Focus Areas

### 1. Bottleneck Identification
**Priority: CRITICAL**

Identify performance bottlenecks across the application:
- CPU-intensive operations
- I/O-bound operations
- Network latency issues
- Database query performance
- Memory allocation patterns

**Key Patterns to Identify:**
- Synchronous blocking operations
- Inefficient algorithms (O(n²) or worse)
- Repeated expensive operations
- Resource contention points
- Serial operations that could be parallelized

**Questions to Answer:**
- What are the slowest operations?
- Where is time being spent in request handling?
- Are there unnecessary waits or blocks?
- What operations are CPU vs I/O bound?
- Are there cascading performance issues?

### 2. Algorithm & Data Structure Efficiency
**Priority: CRITICAL**

Analyze computational efficiency:
- Algorithm complexity (time and space)
- Data structure selection
- Loop optimization opportunities
- Recursion vs iteration
- Algorithmic improvements

**Key Patterns to Identify:**
- Nested loops over large datasets
- Linear searches that could use indexes/maps
- Inefficient sorting algorithms
- Unnecessary data copying
- Poor data structure choices

**Questions to Answer:**
- What is the Big-O complexity of critical operations?
- Are data structures appropriate for access patterns?
- Are there opportunities to reduce complexity?
- Can algorithms be optimized or replaced?
- Are there redundant computations?

### 3. Caching Strategies
**Priority: HIGH**

Evaluate caching implementation and effectiveness:
- Cache layer design
- Cache key strategies
- Cache invalidation logic
- Cache hit/miss ratios
- Cache storage mechanisms

**Key Patterns to Identify:**
- Cache-aside pattern
- Write-through/write-back caching
- Read-through caching
- Distributed caching
- Memoization opportunities

**Questions to Answer:**
- What should be cached?
- When should cache be invalidated?
- What is the cache TTL strategy?
- Are cache hit rates acceptable?
- Is cache size appropriately configured?

### 4. Database Performance
**Priority: HIGH**

Analyze database-related performance:
- Query execution time
- N+1 query problems
- Connection pooling efficiency
- Index utilization
- Query batching opportunities

**Key Patterns to Identify:**
- Missing indexes
- Inefficient queries
- Excessive database round-trips
- Large result sets
- Unoptimized ORMs

**Questions to Answer:**
- Are queries optimized?
- Are indexes being used?
- Can queries be batched?
- Are there N+1 problems?
- Is connection pooling optimal?

### 5. Memory Management
**Priority: HIGH**

Examine memory usage patterns:
- Memory allocation patterns
- Garbage collection impact
- Memory leaks
- Object pooling opportunities
- Large object handling

**Key Patterns to Identify:**
- Excessive object creation
- Memory retention issues
- Large in-memory data structures
- Inefficient string operations
- Resource leak patterns

**Questions to Answer:**
- What is the memory footprint?
- Are there memory leaks?
- Is GC pressure excessive?
- Can memory usage be reduced?
- Are large objects handled efficiently?

### 6. Concurrency & Parallelism
**Priority: HIGH**

Analyze concurrent execution patterns:
- Thread/process utilization
- Async/await usage
- Parallel processing opportunities
- Lock contention
- Race condition risks

**Key Patterns to Identify:**
- Serial operations that could be parallel
- Thread pool configuration
- Async operation usage
- Lock-free algorithms
- Work queue patterns

**Questions to Answer:**
- Are CPU cores fully utilized?
- Are operations appropriately async?
- Is there lock contention?
- Can work be parallelized?
- Are there concurrency bugs?

### 7. Network & I/O Performance
**Priority: MEDIUM**

Evaluate network and I/O efficiency:
- API call patterns
- Payload sizes
- Connection reuse
- Streaming vs buffering
- Compression usage

**Key Patterns to Identify:**
- Chatty API calls
- Large payload transfers
- Synchronous I/O operations
- Connection establishment overhead
- Missing compression

**Questions to Answer:**
- Are network calls minimized?
- Are payloads optimized?
- Is compression used appropriately?
- Are connections reused?
- Can operations be batched?

### 8. Resource Utilization
**Priority: MEDIUM**

Monitor system resource usage:
- CPU utilization patterns
- Memory consumption
- Disk I/O patterns
- Network bandwidth usage
- Thread/connection pool usage

**Key Patterns to Identify:**
- Resource saturation points
- Inefficient resource allocation
- Resource pooling opportunities
- Resource leak scenarios
- Throttling requirements

**Questions to Answer:**
- What resources are constrained?
- Is resource allocation efficient?
- Are resources properly released?
- Are pools sized correctly?
- Is there resource waste?

## Analysis Emphasis

### Performance Quality Indicators

**GOOD Implementation:**
- Optimal algorithm complexity for critical paths
- Effective caching strategies
- Efficient database queries with proper indexes
- Appropriate async/parallel processing
- Minimal memory allocations
- Resource pooling and reuse
- Lazy loading where appropriate
- Efficient serialization/deserialization
- Proper connection management
- Comprehensive performance monitoring

**BAD Implementation:**
- Inefficient algorithms (O(n²) or worse on large data)
- No caching or cache stampede issues
- N+1 query problems
- Blocking I/O on critical paths
- Excessive memory allocations
- Resource leaks
- Eager loading of unnecessary data
- Inefficient string concatenation in loops
- Connection per request pattern
- No performance metrics or monitoring

### Specific Concerns

**Hot Path Optimization:**
- Profile to identify actual hot paths
- Optimize hot paths first (80/20 rule)
- Avoid premature optimization
- Measure before and after changes
- Consider readability vs performance tradeoffs

**Caching:**
- Cache expensive computations
- Cache database queries appropriately
- Implement cache invalidation strategy
- Monitor cache hit rates
- Avoid caching everything (memory tradeoff)

**Database:**
- Eliminate N+1 queries
- Add indexes for common queries
- Use connection pooling
- Batch operations when possible
- Consider read replicas for read-heavy loads

**Async Operations:**
- Use async for I/O-bound operations
- Avoid blocking the event loop
- Implement proper error handling
- Use timeouts for external calls
- Consider backpressure mechanisms

**Memory:**
- Minimize object creation in hot paths
- Use object pooling for large/frequent objects
- Implement streaming for large data
- Monitor GC metrics
- Fix memory leaks promptly

## Code Review Checklist

When reviewing for performance, verify:

1. **Algorithm Efficiency:**
   - [ ] Algorithm complexity is acceptable for data size
   - [ ] Data structures match access patterns
   - [ ] No unnecessary nested loops
   - [ ] Efficient sorting/searching algorithms used
   - [ ] No redundant computations

2. **Caching:**
   - [ ] Expensive operations are cached
   - [ ] Cache keys are well-designed
   - [ ] Cache invalidation is correct
   - [ ] Cache TTL is appropriate
   - [ ] Cache size limits are set

3. **Database:**
   - [ ] No N+1 query problems
   - [ ] Queries are optimized
   - [ ] Indexes support queries
   - [ ] Connection pooling is used
   - [ ] Batch operations where possible

4. **Async/Concurrency:**
   - [ ] I/O operations are async
   - [ ] CPU-intensive work can be parallelized
   - [ ] No blocking on critical paths
   - [ ] Proper error handling in async code
   - [ ] Timeouts are implemented

5. **Memory:**
   - [ ] No excessive object creation
   - [ ] Resources are properly released
   - [ ] Large data uses streaming
   - [ ] String concatenation is efficient
   - [ ] No obvious memory leaks

6. **Network/I/O:**
   - [ ] API calls are minimized
   - [ ] Payloads are optimized
   - [ ] Compression is used where beneficial
   - [ ] Connections are reused
   - [ ] Batch operations reduce round-trips

## Performance Patterns

### Optimization Techniques

**Lazy Loading:**
- Load data only when needed
- Implement pagination for large datasets
- Use virtual scrolling for long lists
- Defer non-critical operations

**Eager Loading:**
- Preload related data to avoid N+1
- Use database joins appropriately
- Prefetch for predictable access patterns
- Balance with memory usage

**Batching:**
- Batch database operations
- Batch API calls
- Use bulk insert/update operations
- Implement request coalescing

**Memoization:**
- Cache function results
- Use for expensive pure functions
- Implement cache eviction strategy
- Monitor memory usage

**Object Pooling:**
- Reuse expensive-to-create objects
- Pool database connections
- Pool worker threads
- Implement pool size limits

**Streaming:**
- Stream large files
- Use streaming APIs for big data
- Implement backpressure handling
- Process data incrementally

## Performance Metrics

### Key Metrics to Track

**Response Time:**
- Average response time
- p50, p95, p99 percentiles
- Response time by endpoint
- Response time trends over time

**Throughput:**
- Requests per second
- Transactions per second
- Data processed per second
- Peak vs average throughput

**Resource Utilization:**
- CPU usage percentage
- Memory usage and GC frequency
- Disk I/O operations
- Network bandwidth
- Connection pool usage

**Database Metrics:**
- Query execution time
- Connection pool saturation
- Cache hit rates
- Slow query frequency
- Index usage statistics

**Error Rates:**
- Timeout frequency
- Error rate percentage
- Failed request patterns
- Retry counts

## Profiling & Monitoring

**Profiling Tools:**
- CPU profilers (identify hot spots)
- Memory profilers (find leaks and allocations)
- Database query profilers
- Network request profilers
- Application Performance Monitoring (APM) tools

**Monitoring Best Practices:**
- Establish baseline performance metrics
- Set up alerts for degradation
- Track performance over time
- Monitor in production environment
- Use distributed tracing for microservices

## Scalability Considerations

**Horizontal Scaling:**
- Stateless application design
- Load balancing strategies
- Session management across instances
- Distributed caching

**Vertical Scaling:**
- Resource limit identification
- Optimal resource allocation
- Diminishing returns analysis

**Database Scaling:**
- Read replicas for read-heavy loads
- Sharding strategies
- Connection pool sizing
- Query optimization

## Documentation Requirements

Performance documentation should include:
- Performance baselines and targets
- Identified bottlenecks and solutions
- Caching strategy documentation
- Scaling strategies
- Performance testing procedures
- Monitoring and alerting setup
- Optimization history and results
