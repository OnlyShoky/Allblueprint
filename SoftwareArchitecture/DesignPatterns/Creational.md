# Creational Design Patterns

#design-patterns #creational #oop

> [!important] Object Creation Mechanisms
> Creational patterns deal with object creation mechanisms, trying to create objects in a manner suitable to the situation. They help make a system independent of how its objects are created, composed, and represented.

**Related Topics:** [[../Principles/SOLID|SOLID Principles]] · [[Structural|Structural Patterns]] · [[Behavioral|Behavioral Patterns]]

---

## 1. Singleton

**Intent:** Ensure a class has only one instance and provide a global point of access to it.

**Diagram:**
```
+-------------+
|  Singleton  |
+-------------+
| - instance  |
+-------------+
| + getInstance() |
+-------------+
```

> [!warning] Use Sparingly
> Singletons create global state, which can make testing difficult. Consider dependency injection as an alternative.

**Example (Python):**

```python
class Singleton:
    _instance = None

    def __new__(cls):
        if cls._instance is None:
            cls._instance = super(Singleton, cls).__new__(cls)
        return cls._instance

s1 = Singleton()
s2 = Singleton()
print(s1 is s2)  # True
```

**Pros:** Controlled access to sole instance.  
**Cons:** Global state can be hard to test.

**Related:** Common in [[../BestPractices/Observability#Logging|logging systems]] and [[../DataAndAI/DataEngineering|database connections]].

---

## 2. Factory Method

**Intent:** Define an interface for creating an object, but let subclasses decide which class to instantiate.

> [!tip] Flexibility Through Abstraction
> Factory Method supports the [[../Principles/SOLID#Open-Closed Principle|Open/Closed Principle]]—you can introduce new types without changing existing code.

**Example (Python):**

```python
class Animal:
    def speak(self): pass

class Dog(Animal):
    def speak(self): return "Woof"

class Cat(Animal):
    def speak(self): return "Meow"

class AnimalFactory:
    def create_animal(self, animal_type):
        if animal_type == "dog":
            return Dog()
        elif animal_type == "cat":
            return Cat()
        return None
```

**Pros:** Decouples creator from concrete products.  
**Cons:** Can lead to many subclasses.

**Related:** Essential for [[../Principles/SOLID#Dependency Inversion Principle|DIP]] and [[../BestPractices/Testing_TDD_BDD|testable code]].

---

## 3. Builder

**Intent:** Separate the construction of a complex object from its representation.

> [!success] Complex Object Construction
> Builder is perfect when an object requires many configuration steps. It provides a fluent interface for building objects step by step.

**Example (Python):**

```python
class Pizza:
    def __init__(self):
        self.toppings = []

class PizzaBuilder:
    def __init__(self):
        self.pizza = Pizza()
    
    def add_cheese(self):
        self.pizza.toppings.append("cheese")
        return self
    
    def add_pepperoni(self):
        self.pizza.toppings.append("pepperoni")
        return self
    
    def build(self):
        return self.pizza

pizza = PizzaBuilder().add_cheese().add_pepperoni().build()
```

**Pros:** Allows fine control over construction process.  
**Cons:** Requires creating a separate Builder class.

**Related:** Used in [[../ModernArchitectures/CloudNative#Configuration|configuration management]] and [[../DataAndAI/ML_DL_Patterns|ML model builders]].

---

## 4. Abstract Factory

**Intent:** Provide an interface for creating families of related or dependent objects without specifying their concrete classes.

> [!note] Family of Objects
> Abstract Factory creates groups of related objects (e.g., UI components for different operating systems).

**Example (Python):**

```python
from abc import ABC, abstractmethod

class Button(ABC):
    @abstractmethod
    def render(self): pass

class WindowsButton(Button):
    def render(self): return "Windows Button"

class MacButton(Button):
    def render(self): return "Mac Button"

class GUIFactory(ABC):
    @abstractmethod
    def create_button(self): pass

class WindowsFactory(GUIFactory):
    def create_button(self): return WindowsButton()

class MacFactory(GUIFactory):
    def create_button(self): return MacButton()
```

**Pros:** Ensures compatibility among created objects.  
**Cons:** Can become complex with many product families.

**Related:** Common in [[../TrendsAndInnovations/MicroFrontends|micro frontends]] and [[../ModernArchitectures/CloudNative|cloud-native]] multi-platform apps.

---

## 5. Prototype

**Intent:** Specify the kinds of objects to create using a prototypical instance, and create new objects by copying this prototype.

> [!tip] Cloning for Efficiency
> Prototype is useful when object creation is expensive. Clone existing objects instead of creating from scratch.

**Example (Python):**

```python
import copy

class Prototype:
    def clone(self):
        return copy.deepcopy(self)

class ConcretePrototype(Prototype):
    def __init__(self, field):
        self.field = field

original = ConcretePrototype("value")
cloned = original.clone()
```

**Pros:** Avoids expensive object creation.  
**Cons:** Cloning complex objects can be tricky.

**Related:** Used in [[../DataAndAI/ML_DL_Patterns|ML model templates]] and [[../BestPractices/CICD_DevOps|CI/CD pipelines]].

---

## Summary Table

| Pattern | Intent | Use When | Related Principle |
|---------|--------|----------|-------------------|
| **Singleton** | Single instance | Global resource needed | - |
| **Factory Method** | Subclass decides instantiation | Need flexibility in object creation | [[../Principles/SOLID#Open-Closed Principle\|OCP]] |
| **Builder** | Step-by-step construction | Complex object with many options | [[../Principles/SOLID#Single Responsibility Principle\|SRP]] |
| **Abstract Factory** | Family of related objects | Multiple related products | [[../Principles/SOLID#Open-Closed Principle\|OCP]] |
| **Prototype** | Clone existing objects | Object creation is expensive | - |

---

## Further Reading

- Understand [[../Principles/SOLID|SOLID principles]] that underpin these patterns
- Explore how these combine with [[Structural|Structural Patterns]]
- See patterns in action with [[../BestPractices/Testing_TDD_BDD|test-driven development]]
- Apply in [[../ModernArchitectures/Monolith_Microservices|microservices architecture]]

**Tags:** #design-patterns #creational #factory #singleton #builder
