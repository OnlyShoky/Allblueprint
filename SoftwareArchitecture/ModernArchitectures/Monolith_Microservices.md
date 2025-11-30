# Monolith vs Microservices

#architecture #microservices #monolith #system-design

> [!note] Architectural Evolution
> The choice between monolithic and microservices architecture is one of the most critical decisions in modern software development. Each approach has clear trade-offs that depend on team size, scalability needs, and organizational maturity.

**Related Topics:** [[CloudNative|Cloud-Native]] · [[Serverless_EventDriven|Event-Driven]] · [[../DesignPatterns/Architectural|Architectural Patterns]] · [[../BestPractices/CICD_DevOps|CI/CD]]

---

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

> [!success] Start Simple
> For most projects, especially MVPs and startups, a well-designed monolith is the right starting point. Don't prematurely optimize for scale you don't have yet.

**Pros:**
- Simple to develop and deploy initially
- Easier debugging and testing (end-to-end)
- No network latency between components
- Single deployment unit
- Simpler development workflow

**Cons:**
- Hard to scale individual components
- Tightly coupled; a change in one part can break others
- Technology stack lock-in
- Longer build and deployment times as codebase grows
- Can become difficult to maintain at scale

**Use Case:** Small startups, MVPs, simple applications, teams < 10 developers.

**Related:** Aligns with [[../Principles/DRY_KISS_YAGNI#KISS|KISS principle]] and [[../DesignPatterns/Architectural#Layered|layered architecture]].

---

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

> [!warning] Complexity Trade-off
> Microservices introduce significant operational complexity. Only adopt this architecture when you have clear scalability requirements and mature DevOps practices.

**Pros:**
- Independent scaling and deployment
- Technology diversity (polyglot persistence and programming)
- Fault isolation (one service failure doesn't bring down the system)
- Team autonomy (different teams can own different services)
- Better alignment with [[../DesignPatterns/Architectural#Hexagonal|DDD and bounded contexts]]

**Cons:**
- Complexity in management and orchestration
- Distributed system challenges (latency, consistency, data management)
- Requires robust [[../BestPractices/CICD_DevOps|DevOps]] culture and [[../BestPractices/Observability|observability]]
- Network overhead and potential points of failure
- Testing complexity (integration tests, contract testing)
- Data consistency challenges

**Use Case:** Large-scale enterprise applications (Netflix, Amazon, Uber), systems with clear bounded contexts.

**Related:** Requires [[CloudNative|cloud-native infrastructure]], [[../BestPractices/Observability|comprehensive monitoring]], and [[../Cybersecurity/API_Microservice_Security|API security]].

---

## Comparison Table

| Aspect | Monolith | Microservices |
|--------|----------|---------------|
| **Deployment** | Single unit | Multiple independent services |
| **Scaling** | Scale entire app | Scale individual services |
| **Tech Stack** | Usually uniform | Polyglot possible |
| **Team Size** | Best for small-medium | Suitable for large, distributed teams |
| **Testing** | Simpler E2E testing | Complex integration testing |
| **Fault Isolation** | Single point of failure | Services can fail independently |
| **Development Speed** | Fast initially | Slower setup, faster long-term iteration |
| **Operational Complexity** | Low | High |

---

## Migration Strategy

> [!tip] Strangler Fig Pattern
> When migrating from monolith to microservices, use the Strangler Fig pattern: gradually extract services while keeping the monolith running. Don't attempt a big-bang rewrite.

**Steps:**
1. Start with clear [[../DesignPatterns/Architectural#Hexagonal|bounded contexts]]
2. Extract one service at a time
3. Use [[../DesignPatterns/Structural#Adapter|anti-corruption layers]]
4. Implement [[../Cybersecurity/API_Microservice_Security#API Gateway|API gateways]] early
5. Build [[../BestPractices/Observability|observability]] before you need it

---

## Decision Guide

> [!question] Which Architecture Should You Choose?
> 
> **Choose Monolith if:**
> - You're building an MVP or new product
> - Team size < 10 developers
> - Requirements are not fully clear yet
> - You don't have mature DevOps practices
> 
> **Choose Microservices if:**
> - You have clear scalability requirements
> - Different parts have different scaling needs
> - You have multiple autonomous teams
> - You have mature [[../BestPractices/CICD_DevOps|CI/CD]] and [[../BestPractices/Observability|observability]]
> - Your domain has clear bounded contexts

---

## Further Reading

- Implement with [[CloudNative|cloud-native patterns]]
- Secure with [[../Cybersecurity/API_Microservice_Security|API security practices]]
- Monitor using [[../BestPractices/Observability|observability tools]]
- Deploy with [[../BestPractices/CICD_DevOps|CI/CD pipelines]]
- Apply [[../Principles/SOLID#Dependency Inversion Principle|DIP]] for decoupling

**Tags:** #architecture #microservices #monolith #system-design #scalability
