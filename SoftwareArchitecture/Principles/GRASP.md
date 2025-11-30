# GRASP (General Responsibility Assignment Software Patterns)

#principles #oop #design #responsibility

> [!important] Assigning Responsibilities Wisely
> GRASP consists of guidelines for assigning responsibility to classes and objects in object-oriented design. These patterns help you decide "who should do what" in your system.

**Related Topics:** [[SOLID|SOLID Principles]] · [[DRY_KISS_YAGNI|DRY/KISS/YAGNI]] · [[../DesignPatterns/Architectural|Architectural Patterns]]

---

## Key Patterns

### 1. Information Expert

**Principle:** Assign a responsibility to the class that has the information necessary to fulfill the responsibility.

**Why:** Encapsulation is maintained; objects do their own work.

> [!tip] Best Practice
> If a class has the data needed to perform a task, it should perform that task. This keeps related data and behavior together.

**Example:**
```python
class Order:
    def __init__(self, items):
        self.items = items
    
    # Order has the item data, so it calculates total
    def calculate_total(self):
        return sum(item.price for item in self.items)
```

**Related:** Aligns with [[SOLID#Single Responsibility Principle|SRP]].

---

### 2. Creator

**Principle:** Who should create instance A? B should create A if:
- B contains or compositely aggregates A
- B records A
- B closely uses A
- B has the initializing data for A

> [!note] Object Creation Responsibility
> Assign creation responsibility to classes that have a strong relationship with the created object.

**Example:**
```python
class Order:
    def __init__(self):
        self.items = []
    
    # Order creates OrderItems because it contains them
    def add_item(self, product, quantity):
        item = OrderItem(product, quantity)
        self.items.append(item)
```

**Related:** See [[../DesignPatterns/Creational#Factory|Factory pattern]] for more complex creation logic.

---

### 3. Controller

**Principle:** Assign the responsibility for handling a system event to a class representing the system or a use case scenario.

**Why:** Decouples UI from business logic.

> [!important] Separation of Concerns
> Controllers handle system events and coordinate responses without implementing business logic themselves.

**Related:** Foundation of [[../DesignPatterns/Architectural#MVC|MVC pattern]] and [[../ModernArchitectures/Monolith_Microservices#Microservices|API design]].

---

### 4. Low Coupling

**Principle:** Assign responsibilities so that coupling remains low.

**Why:** Lower dependency between classes makes reuse and testing easier.

> [!tip] Minimize Dependencies
> Classes should depend on as few other classes as possible. Use interfaces and abstractions to reduce coupling.

**Related:** Essential for [[SOLID#Dependency Inversion Principle|DIP]], [[../BestPractices/Testing_TDD_BDD|testability]], and [[../ModernArchitectures/Monolith_Microservices|microservices]].

---

### 5. High Cohesion

**Principle:** Assign responsibilities so that cohesion remains high.

**Why:** Classes are easier to understand and maintain when they do one thing well.

> [!success] Focused Classes
> Each class should have a clear, focused purpose. High cohesion means all methods in a class work toward the same goal.

**Related:** Directly supports [[SOLID#Single Responsibility Principle|SRP]].

---

### 6. Polymorphism

**Principle:** Assign responsibility for behavior using polymorphic operations for the types of objects that vary.

**Why:** Handles alternatives based on type without `if-else` or `switch` statements.

**Example:**
```python
class Payment(ABC):
    @abstractmethod
    def process(self): pass

class CreditCardPayment(Payment):
    def process(self):
        # Credit card logic
        pass

class PayPalPayment(Payment):
    def process(self):
        # PayPal logic
        pass
```

**Related:** Core to [[SOLID#Open-Closed Principle|OCP]] and [[../DesignPatterns/Behavioral#Strategy|Strategy pattern]].

---

### 7. Pure Fabrication

**Principle:** Assign a highly cohesive set of responsibilities to an artificial or convenience class that does not represent a problem domain concept.

**Why:** Sometimes you need utility classes that don't map to real-world objects but improve design.

**Example:** `Logger`, `DatabaseAdapter`, `ConfigManager`

> [!note] Utility Classes
> Pure fabrications are invented classes that help achieve low coupling and high cohesion, even though they don't represent domain concepts.

**Related:** See [[../DesignPatterns/Structural#Adapter|Adapter pattern]].

---

### 8. Indirection

**Principle:** Assign responsibility to an intermediate object to mediate between other components or services so that they are not directly coupled.

**Why:** Reduces coupling and increases flexibility.

**Example:** Using an adapter or wrapper to access a third-party API.

**Related:** [[../DesignPatterns/Structural#Adapter|Adapter]], [[../DesignPatterns/Structural#Proxy|Proxy]], and [[../DesignPatterns/Structural#Facade|Facade patterns]].

---

### 9. Protected Variations

**Principle:** Identify points of predicted variation or instability; assign responsibilities to create a stable interface around them.

**Why:** Protects the system from changes by wrapping unstable parts behind stable interfaces.

> [!important] Design for Change
> Use interfaces and abstractions to protect against changes in implementation or external dependencies.

**Example:** Using interfaces for external services (payment gateways, email providers) so you can swap implementations.

**Related:** Foundation of [[SOLID#Open-Closed Principle|OCP]] and [[SOLID#Dependency Inversion Principle|DIP]].

---

## Summary Table

| Pattern | Purpose | Key Benefit |
|---------|---------|-------------|
| **Information Expert** | Assign to class with needed data | Strong encapsulation |
| **Creator** | Assign creation to related class | Logical object creation |
| **Controller** | Handle system events | UI/logic separation |
| **Low Coupling** | Minimize dependencies | Easier testing & reuse |
| **High Cohesion** | Focus class purpose | Maintainability |
| **Polymorphism** | Use type-based behavior | Eliminate conditionals |
| **Pure Fabrication** | Create utility classes | Better design |
| **Indirection** | Mediate with intermediate | Reduced coupling |
| **Protected Variations** | Wrap unstable points | Change resilience |

---

## Further Reading

- Compare with [[SOLID|SOLID principles]]
- Apply in [[../DesignPatterns/|design patterns]]
- Use for [[../ModernArchitectures/Monolith_Microservices|architectural decisions]]
- Essential for [[../BestPractices/Testing_TDD_BDD|testable code]]

**Tags:** #principles #grasp #oop #responsibility #design
