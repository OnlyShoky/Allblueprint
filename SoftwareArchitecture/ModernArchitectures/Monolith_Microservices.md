# Monolith vs Microservices

## Monolithic Architecture
A single, unified unit where all components (UI, business logic, data access) are packaged and deployed together.

**Diagram:**
```
+---------------------------+
|        Monolith           |
| [UI] [Logic] [Data Layer] |
+---------------------------+
            |
        [Database]
```

**Pros:**
- Simple to develop and deploy initially.
- Easier debugging and testing (end-to-end).
- No network latency between components.

**Cons:**
- Hard to scale individual components.
- Tightly coupled; a change in one part can break others.
- Technology stack lock-in.

**Use Case:** Small startups, MVPs, simple applications.

## Microservices Architecture
An application is structured as a collection of loosely coupled services, each implementing a specific business capability.

**Diagram:**
```
       [API Gateway]
        /    |    \
   [Svc A] [Svc B] [Svc C]
      |       |       |
    [DB A]  [DB B]  [DB C]
```

**Pros:**
- Independent scaling and deployment.
- Technology diversity (polyglot).
- Fault isolation.

**Cons:**
- Complexity in management and orchestration.
- Distributed system challenges (latency, consistency).
- Requires robust DevOps culture.

**Use Case:** Large-scale enterprise applications (Netflix, Amazon, Uber).
