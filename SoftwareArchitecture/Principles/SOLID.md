# SOLID Principles

#principles #architecture #oop

> [!important] Foundation of Clean Code
> The SOLID principles are five design principles intended to make software designs more understandable, flexible, and maintainable. They form the foundation of object-oriented programming and are essential for any software architect.

**Related Topics:** [[DRY_KISS_YAGNI|DRY/KISS/YAGNI]] · [[GRASP|GRASP]] · [[../DesignPatterns/Creational|Design Patterns]] · [[../BestPractices/Testing_TDD_BDD|Testing]]

---

## 1. Single Responsibility Principle (SRP)

**Definition:** A class should have one, and only one, reason to change.

**Why:** Reduces coupling. If a class handles multiple responsibilities, changing one might break others.

> [!tip] Best Practice
> Each class should focus on a single aspect of functionality. This makes code easier to test, understand, and modify.

**Example (Python):**

```python
# Bad: Mixed responsibilities
class UserSettings:
    def change_settings(self, settings):
        if self.verify_credentials():
            print("Settings updated")
    
    def verify_credentials(self):
        # Logic to verify credentials
        return True

# Good: Separated responsibilities
class UserAuth:
    def verify_credentials(self):
        return True

class UserSettings:
    def __init__(self, auth):
        self.auth = auth
        
    def change_settings(self, settings):
        if self.auth.verify_credentials():
            print("Settings updated")
```

**Related:** This principle pairs well with [[../DesignPatterns/Structural#Facade|Facade pattern]] and supports [[../BestPractices/Testing_TDD_BDD|unit testing]].

---

## 2. Open/Closed Principle (OCP)

**Definition:** Software entities should be open for extension, but closed for modification.

**Why:** Allows adding new functionality without changing existing code, preventing regression bugs.

> [!note] Key Insight
> Use abstraction and polymorphism to extend behavior without modifying existing classes.

**Example (Python):**

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height
    def area(self):
        return self.width * self.height

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius
    def area(self):
        return 3.14 * self.radius * self.radius

# We can add new shapes without modifying existing classes
```

**Related:** Essential for [[../DesignPatterns/Creational#Factory|Factory]] and [[../DesignPatterns/Behavioral#Strategy|Strategy patterns]].

---

## 3. Liskov Substitution Principle (LSP)

**Definition:** Subtypes must be substitutable for their base types without altering the correctness of the program.

**Why:** Ensures inheritance hierarchies are correct and predictable.

> [!warning] Common Violation
> Throwing exceptions in subclass methods that the base class doesn't throw is a common LSP violation.

**Example (Python):**

```python
class Bird:
    def fly(self):
        pass

# Bad: Ostrich cannot fly, violating LSP if it inherits from Bird
class Ostrich(Bird):
    def fly(self):
        raise Exception("Cannot fly")

# Good: Refactor hierarchy
class Bird:
    pass

class FlyingBird(Bird):
    def fly(self):
        pass

class Ostrich(Bird):
    pass
```

**Related:** Critical for [[../DesignPatterns/Behavioral|polymorphic behavior]] and [[../BestPractices/Testing_TDD_BDD|testing]].

---

## 4. Interface Segregation Principle (ISP)

**Definition:** Clients should not be forced to depend on interfaces they do not use.

**Why:** Prevents "fat" interfaces and unnecessary dependencies.

> [!tip] Design Tip
> Create small, focused interfaces rather than one large interface. This promotes flexibility and maintainability.

**Example (Python):**

```python
# Bad: Fat interface
class WorkerInterface:
    def work(self): pass
    def eat(self): pass

# Good: Segregated interfaces
class Workable:
    def work(self): pass

class Eatable:
    def eat(self): pass

class Robot(Workable):
    def work(self):
        print("Robot working")
```

**Related:** Supports [[../ModernArchitectures/Monolith_Microservices#Microservices|microservices architecture]] and [[Functional_Reactive#Functional|functional programming]].

---

## 5. Dependency Inversion Principle (DIP)

**Definition:** High-level modules should not depend on low-level modules. Both should depend on abstractions.

**Why:** Decouples modules, making the system easier to change and test.

> [!important] Architectural Impact
> DIP is fundamental to building flexible, testable architectures. It's the basis for dependency injection and inversion of control (IoC).

**Example (Python):**

```python
# Bad: High-level depends on low-level
class LightBulb:
    def turn_on(self): pass

class Switch:
    def __init__(self, bulb: LightBulb):
        self.bulb = bulb

# Good: Both depend on abstraction
from abc import ABC, abstractmethod

class Switchable(ABC):
    @abstractmethod
    def turn_on(self): pass

class LightBulb(Switchable):
    def turn_on(self): pass

class Switch:
    def __init__(self, device: Switchable):
        self.device = device
```

**Related:** Essential for [[../BestPractices/Testing_TDD_BDD#Mocking|unit testing with mocks]], [[../DesignPatterns/Creational|dependency injection]], and [[../ModernArchitectures/CloudNative#12-Factor|12-factor apps]].

---

## Summary Table

| Principle | Focus | Key Benefit |
|-----------|-------|-------------|
| **SRP** | Single responsibility per class | Easier to maintain and test |
| **OCP** | Extend without modifying | Reduces regression risk |
| **LSP** | Substitutability of subtypes | Predictable inheritance |
| **ISP** | Small, focused interfaces | Reduces coupling |
| **DIP** | Depend on abstractions | Flexibility and testability |

---

## Further Reading

> [!question] Want to Learn More?
> - Explore how SOLID applies to [[../DesignPatterns/Architectural|architectural patterns]]
> - See SOLID in action with [[../BestPractices/Testing_TDD_BDD|test-driven development]]
> - Learn about [[../Cybersecurity/SecureCoding|secure coding]] that respects SOLID
> - Understand [[GRASP|GRASP principles]] as a complement to SOLID

**Tags:** #principles #solid #oop #clean-code
