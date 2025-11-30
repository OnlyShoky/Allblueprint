# GRASP (General Responsibility Assignment Software Patterns)

GRASP consists of guidelines for assigning responsibility to classes and objects in object-oriented design.

## Key Patterns

### 1. Information Expert
**Principle:** Assign a responsibility to the class that has the information necessary to fulfill the responsibility.
**Why:** Encapsulation is maintained; objects do their own work.

### 2. Creator
**Principle:** Who should create instance A? B should create A if:
- B contains or compositely aggregates A
- B records A
- B closely uses A
- B has the initializing data for A

### 3. Controller
**Principle:** Assign the responsibility for handling a system event to a class representing the system or a use case scenario.
**Why:** Decouples UI from business logic.

### 4. Low Coupling
**Principle:** Assign responsibilities so that coupling remains low.
**Why:** Lower dependency between classes makes reuse and testing easier.

### 5. High Cohesion
**Principle:** Assign responsibilities so that cohesion remains high.
**Why:** Classes are easier to understand and maintain when they do one thing well.

### 6. Polymorphism
**Principle:** Assign responsibility for behavior using polymorphic operations for the types of objects that vary.
**Why:** Handles alternatives based on type without `if-else` or `switch` statements.

### 7. Pure Fabrication
**Principle:** Assign a highly cohesive set of responsibilities to an artificial or convenience class that does not represent a problem domain concept.
**Example:** `Logger`, `DatabaseAdapter`.

### 8. Indirection
**Principle:** Assign responsibility to an intermediate object to mediate between other components or services so that they are not directly coupled.
**Example:** Adapter pattern.

### 9. Protected Variations
**Principle:** Identify points of predicted variation or instability; assign responsibilities to create a stable interface around them.
**Example:** Interfaces, Polymorphism.
