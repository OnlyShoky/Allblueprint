# Architectural Patterns

Architectural patterns are high-level strategies that concern large-scale components, the global properties and mechanisms of a system.

## 1. MVC (Model-View-Controller)
**Concept:** Separates application into three interconnected components.
- **Model:** Data and business logic.
- **View:** UI and presentation.
- **Controller:** Handles input and updates Model/View.

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

**Use Case:** Web frameworks (Django, Ruby on Rails).

## 2. MVVM (Model-View-ViewModel)
**Concept:** Facilitates separation of GUI development from business logic.
- **ViewModel:** Exposes data streams relevant to the View.
- **View:** Binds to ViewModel.

**Use Case:** Modern frontend frameworks (React, Vue, Angular), Mobile apps (Android Jetpack).

## 3. Hexagonal Architecture (Ports and Adapters)
**Concept:** Allows an application to be equally driven by users, programs, automated tests, or batch scripts, and to be developed and tested in isolation from its eventual run-time devices and databases.

**Structure:**
- **Core:** Domain logic.
- **Ports:** Interfaces defining how to interact with the core.
- **Adapters:** Implementations of ports (e.g., REST API adapter, SQL Database adapter).

**Diagram:**
```
      [ Adapter ] --> [ Port ] --> [ Domain Core ] <-- [ Port ] <-- [ Adapter ]
```

**Pros:**
- High testability.
- Independence from frameworks and external tools.
