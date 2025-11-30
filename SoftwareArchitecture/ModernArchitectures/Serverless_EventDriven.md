# Serverless and Event-Driven Architectures

## Serverless Computing
A cloud execution model where the cloud provider runs the server, and dynamically manages the allocation of machine resources.

**Key Concepts:**
- **FaaS (Function as a Service):** AWS Lambda, Google Cloud Functions.
- **BaaS (Backend as a Service):** Firebase, AWS Amplify.

**Pros:**
- No server management.
- Pay-per-use pricing.
- Auto-scaling.

**Cons:**
- Cold start latency.
- Vendor lock-in.
- Debugging complexity.

## Event-Driven Architecture (EDA)
A software architecture paradigm promoting the production, detection, consumption of, and reaction to events.

**Diagram:**
```
[Producer] --> (Event Bus / Broker) --> [Consumer A]
                                    --> [Consumer B]
```

**Patterns:**
- **Pub/Sub:** Publishers send messages to topics; subscribers receive them.
- **Event Sourcing:** Store state changes as a sequence of events.
- **CQRS (Command Query Responsibility Segregation):** Separate read and write models.

**Example (CQRS):**
- **Write Side:** Handles commands (CreateOrder), validates, emits events.
- **Read Side:** Subscribes to events, updates a denormalized view for fast queries.

**Pros:**
- Decoupling of producers and consumers.
- Asynchronous processing.
- Scalability.

**Cons:**
- Eventual consistency.
- Complexity in tracing flows.
