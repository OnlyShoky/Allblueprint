# Architectural Patterns

#architecture #patterns #high-level #system-design

> [!important] High-Level System Organization
> Architectural patterns are high-level strategies that concern large-scale components, the global properties and mechanisms of a system. They define the overall structure and organization of software systems.

**Related Topics:** [[Creational|Creational Patterns]] · [[../ModernArchitectures/Monolith_Microservices|Modern Architectures]] · [[../Principles/GRASP#Controller|GRASP Controller]]

---

## 1. MVC (Model-View-Controller)

**Concept:** Separates application into three interconnected components.

| Component | Responsibility |
|-----------|----------------|
| **Model** | Data and business logic |
| **View** | UI and presentation |
| **Controller** | Handles input and updates Model/View |

**Diagram:**
```
    User
     |
     v
Controller -> Model
     |          |
     v          v
    View <------
```

> [!success] Separation of Concerns
> MVC enforces [[../Principles/SOLID#Single Responsibility Principle|SRP]] at the architectural level, making applications easier to test and maintain.

**Use Case:** Web frameworks (Django, Ruby on Rails, ASP.NET MVC).

**Related:** Foundation of [[../BestPractices/Testing_TDD_BDD|testable applications]] and aligns with [[../Principles/GRASP#Controller|GRASP Controller pattern]].

---

## 2. MVVM (Model-View-ViewModel)

**Concept:** Facilitates separation of GUI development from business logic.

| Component | Responsibility |
|-----------|----------------|
| **Model** | Business logic and data |
| **View** | UI layout and presentation |
| **ViewModel** | Exposes data streams and commands for the View |

> [!tip] Data Binding
> MVVM leverages data binding to automatically sync the View with the ViewModel, reducing boilerplate code.

**Diagram:**
```
View <--Binding--> ViewModel <--> Model
```

**Use Case:** Modern frontend frameworks (React with Redux, Vue, Angular), Mobile apps (Android Jetpack, SwiftUI).

**Related:** Common in [[../TrendsAndInnovations/MicroFrontends|micro frontends]] and [[../ModernArchitectures/Serverless_EventDriven|reactive UIs]].

---

## 3. Hexagonal Architecture (Ports and Adapters)

**Concept:** Allows an application to be equally driven by users, programs, automated tests, or batch scripts, and to be developed and tested in isolation from its eventual run-time devices and databases.

**Structure:**
- **Core:** Domain logic (business rules)
- **Ports:** Interfaces defining how to interact with the core
- **Adapters:** Implementations of ports (e.g., REST API adapter, SQL Database adapter)

**Diagram:**
```
[ Adapter ] --> [ Port ] --> [ Domain Core ] <-- [ Port ] <-- [ Adapter ]
 (REST API)   (Input Port)                    (Output Port)   (Database)
```

> [!important] Testability and Flexibility
> Hexagonal Architecture makes your domain logic completely independent of frameworks, databases, and UIs. This supports [[../Principles/SOLID#Dependency Inversion Principle|DIP]].

**Pros:**
- High testability
- Independence from frameworks and external tools
- Easy to swap implementations

**Cons:**
- Initial complexity
- More interfaces and classes

**Related:** Essential for [[../BestPractices/Testing_TDD_BDD|TDD]], [[../ModernArchitectures/Monolith_Microservices#Domain-Driven Design|DDD]], and [[../Principles/SOLID#Dependency Inversion Principle|dependency inversion]].

---

## 4. Layered Architecture

**Concept:** Organizes code into horizontal layers, each with a specific role.

**Common Layers:**
1. **Presentation Layer:** UI and user interaction
2. **Business Logic Layer:** Core business rules
3. **Data Access Layer:** Database interaction
4. **Infrastructure Layer:** External services, frameworks

> [!note] Clear Boundaries
> Each layer depends only on the layer below it, creating clear separation of concerns.

**Pros:**
- Easy to understand
- Clear responsibility separation
- Layer isolation

**Cons:**
- Can become rigid
- Performance overhead from layer transitions

**Related:** Traditional approach before [[../ModernArchitectures/Monolith_Microservices|microservices]] and complements [[Hexagonal Architecture]].

---

## 5. Clean Architecture

**Concept:** Similar to Hexagonal Architecture, Clean Architecture emphasizes dependency rule: dependencies point inward toward business logic.

**Layers (inside to outside):**
1. **Entities:** Core business objects
2. **Use Cases:** Application-specific business rules
3. **Interface Adapters:** Controllers, presenters, gateways
4. **Frameworks & Drivers:** UI, database, external services

> [!success] Dependency Rule
> Source code dependencies must point only inward. Inner circles know nothing about outer circles.

**Related:** Implements [[../Principles/SOLID#Dependency Inversion Principle|DIP]] and supports [[../BestPractices/Testing_TDD_BDD|comprehensive testing]].

---

## 6. Event-Driven Architecture (EDA)

**Concept:** Components communicate through events rather than direct calls.

**Key Elements:**
- **Event Producers:** Generate events
- **Event Consumers:** React to events
- **Event Bus/Broker:** Routes events

> [!important] Asynchronous Communication
> EDA enables loose coupling and scalability. It's the foundation of [[../ModernArchitectures/Serverless_EventDriven|modern serverless systems]].

**Related:** See [[../ModernArchitectures/Serverless_EventDriven#Event-Driven|detailed event-driven patterns]] and [[../Principles/Functional_Reactive#Reactive|reactive principles]].

---

## Comparison Table

| Pattern | Focus | Best For | Testability | Complexity |
|---------|-------|----------|-------------|------------|
| **MVC** | UI separation | Web apps, traditional MVC frameworks | High | Low |
| **MVVM** | Data binding | Modern SPAs, mobile apps | High | Medium |
| **Hexagonal** | Domain isolation | Complex business logic, DDD | Very High | Medium-High |
| **Layered** | Horizontal separation | Enterprise apps, clear layers | High | Low-Medium |
| **Clean** | Dependency rule | Business-critical systems | Very High | High |
| **Event-Driven** | Async messaging | Scalable, distributed systems | Medium | Medium-High |

---

## Choosing an Architectural Pattern

> [!question] Which Pattern to Choose?
> - **MVC/MVVM:** Building UI-heavy applications
> - **Hexagonal/Clean:** Business logic must be framework-independent
> - **Layered:** Simple enterprise applications with clear layers
> - **Event-Driven:** Need scalability and asynchronous processing

---

## Further Reading

- Apply with [[../Principles/SOLID|SOLID principles]]
- Explore [[../ModernArchitectures/Monolith_Microservices|modern architectural approaches]]
- Implement [[../BestPractices/Testing_TDD_BDD|TDD]] with these patterns
- Learn [[../ModernArchitectures/Serverless_EventDriven|event-driven architecture]] in depth
- Study [[../Cybersecurity/SecureCoding|secure architecture practices]]

**Tags:** #architecture #patterns #mvc #mvvm #hexagonal #clean-architecture #event-driven
