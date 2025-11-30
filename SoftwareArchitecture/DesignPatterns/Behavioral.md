# Behavioral Design Patterns

#design-patterns #behavioral #communication

> [!important] Object Communication
> Behavioral patterns are concerned with algorithms and the assignment of responsibilities between objects. They focus on how objects interact and communicate with each other.

**Related Topics:** [[Creational|Creational Patterns]] · [[Structural|Structural Patterns]] · [[../Principles/GRASP|GRASP]]

---

## 1. Observer

**Intent:** Define a one-to-many dependency between objects so that when one object changes state, all its dependents are notified.

**Diagram:**
```
Subject <---- Observer
   |             ^
   |             |
ConcreteSubject  ConcreteObserver
```

> [!success] Event-Driven Communication
> Observer is the foundation of event-driven architectures and reactive programming. It supports the [[../Principles/SOLID#Open-Closed Principle|Open/Closed Principle]].

**Example (Python):**

```python
class Subject:
    def __init__(self):
        self._observers = []
    
    def attach(self, observer):
        self._observers.append(observer)
    
    def notify(self, message):
        for observer in self._observers:
            observer.update(message)

class Observer:
    def update(self, message):
        print(f"Received: {message}")

s = Subject()
o1 = Observer()
s.attach(o1)
s.notify("Hello World")
```

**Pros:** Open/Closed Principle support.  
**Cons:** Subscribers are notified in random order.

**Related:** Foundation of [[../ModernArchitectures/Serverless_EventDriven#Event-Driven|event-driven architecture]] and [[../Principles/Functional_Reactive#Reactive|reactive systems]].

---

## 2. Strategy

**Intent:** Define a family of algorithms, encapsulate each one, and make them interchangeable.

> [!tip] Runtime Behavior Selection
> Strategy lets you swap algorithms at runtime without changing the client code. Perfect for implementing [[../Principles/SOLID#Open-Closed Principle|OCP]].

**Example (Python):**

```python
class PaymentStrategy:
    def pay(self, amount): pass

class CreditCard(PaymentStrategy):
    def pay(self, amount):
        print(f"Paid {amount} via Credit Card")

class PayPal(PaymentStrategy):
    def pay(self, amount):
        print(f"Paid {amount} via PayPal")

class ShoppingCart:
    def __init__(self, strategy):
        self.strategy = strategy
    
    def checkout(self, amount):
        self.strategy.pay(amount)
```

**Pros:** Cleanly separates algorithms from the context.  
**Cons:** Clients must know the differences between strategies.

**Related:** Essential for [[../Principles/GRASP#Polymorphism|polymorphism in GRASP]] and [[../BestPractices/Testing_TDD_BDD|testable code]].

---

## 3. Command

**Intent:** Encapsulate a request as an object, thereby letting you parameterize clients with different requests.

> [!important] Request as Object
> Command pattern supports undo/redo operations, queuing requests, and logging requests. It's the basis for many UI frameworks.

**Example (Python):**

```python
class Command:
    def execute(self): pass

class LightOnCommand(Command):
    def __init__(self, light):
        self.light = light
    def execute(self):
        self.light.turn_on()

class RemoteControl:
    def submit(self, command):
        command.execute()
```

**Pros:** Decouples invoker from receiver. Supports undo/redo.  
**Cons:** Code can become complicated with many command classes.

**Related:** Used in [[../BestPractices/CICD_DevOps|CI/CD pipelines]], [[../DataAndAI/MLOps|MLOps workflows]], and [[../ModernArchitectures/Serverless_EventDriven#Event Sourcing|event sourcing]].

---

## 4. Iterator

**Intent:** Provide a way to access elements of an aggregate object sequentially without exposing its underlying representation.

> [!note] Sequential Access
> Iterator abstracts the traversal of collections, making client code independent of the collection type.

**Example (Python):**

```python
class NumberCollection:
    def __init__(self):
        self._numbers = []
    
    def add(self, number):
        self._numbers.append(number)
    
    def __iter__(self):
        return iter(self._numbers)

collection = NumberCollection()
collection.add(1)
collection.add(2)

for num in collection:
    print(num)
```

**Pros:** Simplifies collection traversal.  
**Cons:** May be overkill for simple collections.

**Related:** Built into [[../Principles/Functional_Reactive#Higher-Order Functions|functional programming]] and [[../DataAndAI/DataEngineering|data pipelines]].

---

## 5. Template Method

**Intent:** Define the skeleton of an algorithm in an operation, deferring some steps to subclasses.

> [!tip] Algorithm Structure
> Template Method lets subclasses redefine specific steps of an algorithm without changing its structure.

**Example (Python):**

```python
from abc import ABC, abstractmethod

class DataProcessor(ABC):
    def process(self):
        data = self.load_data()
        data = self.transform_data(data)
        self.save_data(data)
    
    @abstractmethod
    def load_data(self): pass
    
    @abstractmethod
    def transform_data(self, data): pass
    
    @abstractmethod
    def save_data(self, data): pass

class CSVProcessor(DataProcessor):
    def load_data(self):
        return "CSV data"
    def transform_data(self, data):
        return data.upper()
    def save_data(self, data):
        print(f"Saving: {data}")
```

**Pros:** Reuses common code, enforces algorithm structure.  
**Cons:** Clients must know about template steps.

**Related:** Common in [[../DataAndAI/DataEngineering|ETL pipelines]] and [[../BestPractices/Testing_TDD_BDD|test frameworks]].

---

## 6. State

**Intent:** Allow an object to alter its behavior when its internal state changes.

> [!success] Behavior Based on State
> State pattern eliminates complex conditional logic by delegating behavior to state objects.

**Use Case:** Authentication flows, order processing, UI state management.

**Related:** Critical for [[../ModernArchitectures/Serverless_EventDriven#State Machines|state machines]] and [[../TrendsAndInnovations/MicroFrontends|frontend state management]].

---

## 7. Chain of Responsibility

**Intent:** Avoid coupling the sender of a request to its receiver by giving more than one object a chance to handle the request.

> [!note] Request Handling Chain
> Chain of Responsibility creates a pipeline of handlers, each deciding whether to process the request or pass it along.

**Use Case:** Middleware chains, approval workflows, logging chains.

**Related:** Foundation of [[../BestPractices/Observability#Middleware|middleware patterns]] and [[../Cybersecurity/API_Microservice_Security|API request filtering]].

---

## Summary Table

| Pattern | Intent | Use When | Principle |
|---------|--------|----------|-----------|
| **Observer** | One-to-many notifications | Event-driven systems | [[../Principles/SOLID#Open-Closed Principle\|OCP]] |
| **Strategy** | Interchangeable algorithms | Runtime algorithm selection | [[../Principles/SOLID#Open-Closed Principle\|OCP]] |
| **Command** | Encapsulate requests | Undo/redo, queuing, logging | - |
| **Iterator** | Sequential access | Collection traversal | - |
| **Template Method** | Algorithm skeleton | Common algorithm steps | [[../Principles/DRY_KISS_YAGNI#DRY\|DRY]] |
| **State** | Behavior based on state | Complex state transitions | - |
| **Chain of Responsibility** | Handler chain | Multi-step processing | [[../Principles/GRASP#Low Coupling\|Low Coupling]] |

---

## Further Reading

- Apply [[../Principles/SOLID|SOLID principles]] with behavioral patterns
- Combine with [[../ModernArchitectures/Serverless_EventDriven|event-driven architecture]]
- Use in [[../BestPractices/Testing_TDD_BDD|test-driven development]]
- Essential for [[../DataAndAI/MLOps|MLOps workflows]]

**Tags:** #design-patterns #behavioral #observer #strategy #command
