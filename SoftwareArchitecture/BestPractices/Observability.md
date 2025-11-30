# Observability and Monitoring

**Observability:** The ability to understand the internal state of a system based on its external outputs.

## Three Pillars of Observability

### 1. Logs
**What:** Discrete events (e.g., "Error connecting to DB", "Request received").
**Best Practices:**
- Structured logging (JSON).
- Include correlation IDs.
- Centralized log management (ELK Stack, Splunk).

### 2. Metrics
**What:** Aggregated numerical data over time (e.g., CPU usage, Request rate, Error rate).
**Best Practices:**
- RED Method: Rate, Errors, Duration.
- USE Method: Utilization, Saturation, Errors.
- Tools: Prometheus, Grafana, Datadog.

### 3. Tracing (Distributed Tracing)
**What:** Tracks a request flow across service boundaries.
**Best Practices:**
- OpenTelemetry standard.
- Visualize waterfalls to find latency bottlenecks.
- Tools: Jaeger, Zipkin.

## Monitoring vs. Observability
- **Monitoring:** Tells you *when* something is wrong (Alerts).
- **Observability:** Tells you *why* something is wrong (Debugging).
