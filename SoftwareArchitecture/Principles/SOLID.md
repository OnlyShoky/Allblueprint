# SOLID Principles

The SOLID principles are a set of five design principles intended to make software designs more understandable, flexible, and maintainable.

## 1. Single Responsibility Principle (SRP)
**Definition:** A class should have one, and only one, reason to change.

**Why:** Reduces coupling. If a class handles multiple responsibilities, changing one might break others.

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

## 2. Open/Closed Principle (OCP)
**Definition:** Software entities should be open for extension, but closed for modification.

**Why:** Allows adding new functionality without changing existing code, preventing regression bugs.

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

## 3. Liskov Substitution Principle (LSP)
**Definition:** Subtypes must be substitutable for their base types without altering the correctness of the program.

**Why:** Ensures inheritance hierarchies are correct and predictable.

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

## 4. Interface Segregation Principle (ISP)
**Definition:** Clients should not be forced to depend on interfaces they do not use.

**Why:** Prevents "fat" interfaces and unnecessary dependencies.

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

## 5. Dependency Inversion Principle (DIP)
**Definition:** High-level modules should not depend on low-level modules. Both should depend on abstractions.

**Why:** Decouples modules, making the system easier to change and test.

**Example (Python):**

```python
# Bad: High-level depends on low-level
class LightBulb:
    def turn_on(self): pass

class Switch:
    def __init__(self, bulb: LightBulb):
        self.bulb = bulb

# Good: Both depend on abstraction
class Switchable(ABC):
    @abstractmethod
    def turn_on(self): pass

class LightBulb(Switchable):
    def turn_on(self): pass

class Switch:
    def __init__(self, device: Switchable):
        self.device = device
```
