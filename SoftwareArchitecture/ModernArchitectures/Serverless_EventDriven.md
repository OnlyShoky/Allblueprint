# Serverless and Event-Driven Architectures

#architecture #serverless #event-driven #async #scalability

> [!important] Modern Cloud Paradigms
> Serverless and event-driven architectures represent a shift from always-on servers to on-demand, event-triggered execution. These approaches enable extreme scalability and cost efficiency.

**Related Topics:** [[CloudNative|Cloud-Native]] · [[Monolith_Microservices|Microservices]] · [[../DesignPatterns/Behavioral#Observer|Observer Pattern]] · [[../Principles/Functional_Reactive#Reactive|Reactive Principles]]

---

## Serverless Computing

A cloud execution model where the cloud provider runs the server and dynamically manages the allocation of machine resources.

**Key Concepts:**
- **FaaS (Function as a Service):** AWS Lambda, Google Cloud Functions, Azure Functions
- **BaaS (Backend as a Service):** Firebase, AWS Amplify, Supabase

> [!success] Zero Server Management
> With serverless, you focus purely on code. No provisioning, scaling, or server maintenance required—the cloud provider handles everything.

**Pros:**
- No server management or infrastructure overhead
- Pay-per-use pricing (only pay for execution time)
- Auto-scaling to zero and to infinity
- Fast time to market

**Cons:**
- Cold start latency (first invocation delay)
- Vendor lock-in (provider-specific APIs)
- Debugging complexity (distributed traces needed)
- Limited execution time (typically 15 min max)
- State management challenges

**Use Cases:** API backends, data processing triggers, scheduled tasks, webhooks.

**Related:** Complements [[../BestPractices/CICD_DevOps|CI/CD automation]] and [[../DataAndAI/MLOps|MLOps pipelines]].

---

## Event-Driven Architecture (EDA)

A software architecture paradigm promoting the production, detection, consumption of, and reaction to events.

**Diagram:**
```
[Producer] --> (Event Bus / Broker) --> [Consumer A]
                                   --> [Consumer B]
```

> [!tip] Loose Coupling
> Event-driven architecture achieves extreme decoupling—producers don't know who consumes their events. This enables independent scaling and evolution.

---

## Event-Driven Patterns

### Pub/Sub (Publish-Subscribe)

Publishers send messages to topics; subscribers receive them asynchronously.

**Technologies:** Kafka, RabbitMQ, Google Pub/Sub, AWS SNS/SQS

**Example Use Case:** Notification system where one user action triggers multiple downstream processes (email, SMS, analytics).

**Related:** Implements [[../DesignPatterns/Behavioral#Observer|Observer pattern]] at scale.

---

### Event Sourcing

Store state changes as a sequence of events rather than storing current state.

> [!important] Immutable Event Log
> Every state change is captured as an immutable event. The current state is derived by replaying events.

**Benefits:**
- Complete audit trail
- Time-travel debugging
- Easy to rebuild state

**Challenges:**
- Event schema evolution
- Storage growth

**Related:** Often paired with CQRS and used in [[../DataAndAI/DataEngineering|data pipelines]].

---

### CQRS (Command Query Responsibility Segregation)

Separate read and write models for different performance and scalability characteristics.

**Example (CQRS):**
- **Write Side:** Handles commands (CreateOrder), validates, emits events
- **Read Side:** Subscribes to events, updates a denormalized view for fast queries

> [!success] Optimized for Separate Concerns  
> CQRS lets you optimize writes for consistency and reads for performance independently.

**Related:** Supports [[../BestPractices/Scalability_Resilience#Scalability|high scalability]] patterns.

---

## Comparison Table

| Aspect | Serverless | Event-Driven |
|--------|-----------|--------------|
| **Execution Model** | On-demand functions | Continuous event processing |
| **Scaling** | Automatic, instant | Scales with event volume |
| **State** | Stateless | Can be stateful (event stores) |
| **Use Case** | Isolated tasks, APIs | Workflow orchestration, data pipelines |
| **Complexity** | Low | Medium-High |

---

## Combined Benefits

**Pros:**
- Decoupling of producers and consumers
- Asynchronous processing (non-blocking)
- Infinite horizontal scalability
- Fault isolation (one consumer failure doesn't affect others)

**Cons:**
- Eventual consistency (not ACID)
- Complexity in tracing flows (need distributed tracing)
- Message ordering challenges
- Duplicate message handling

---

## Further Reading

- Apply [[../Principles/Functional_Reactive#Reactive|reactive principles]]
- Implement with [[CloudNative|Kubernetes and cloud-native tools]]
- Monitor using [[../BestPractices/Observability|distributed tracing]]
- Secure with [[../Cybersecurity/API_Microservice_Security|event security patterns]]
- Use in [[../DataAndAI/DataEngineering|real-time data pipelines]]

**Tags:** #serverless #event-driven #lambda #async #scalability #pubsub
