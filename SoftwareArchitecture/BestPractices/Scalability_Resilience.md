# Scalability and Resilience

## Scalability
The capability of a system to handle a growing amount of work.

### Vertical Scaling (Scale Up)
- Adding more power (CPU, RAM) to an existing machine.
- **Limit:** Hardware capacity.

### Horizontal Scaling (Scale Out)
- Adding more machines to the pool of resources.
- **Requirement:** Stateless applications, Load Balancer.

## Resilience Patterns
Strategies to handle failures gracefully.

### 1. Circuit Breaker
**Concept:** Stop making requests to a failing service to prevent cascading failures.
**States:** Closed (Normal), Open (Failing, stop requests), Half-Open (Test if service recovered).

### 2. Retry with Exponential Backoff
**Concept:** Retry a failed operation after waiting for an increasing amount of time.
**Why:** Handles transient network glitches.

### 3. Bulkhead
**Concept:** Isolate elements into pools so that if one fails, the others will continue to function (like ship bulkheads).

### 4. Rate Limiting
**Concept:** Control the rate of traffic sent or received.
**Why:** Protects resources from being overwhelmed (DDoS or spikes).

**Checklist:**
- [ ] No single point of failure.
- [ ] Stateless services where possible.
- [ ] Automated failover.
- [ ] Graceful degradation.
