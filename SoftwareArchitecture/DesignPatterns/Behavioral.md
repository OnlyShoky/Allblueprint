# Behavioral Design Patterns

Behavioral patterns are concerned with algorithms and the assignment of responsibilities between objects.

## 1. Observer
**Intent:** Define a one-to-many dependency between objects so that when one object changes state, all its dependents are notified.

**Diagram:**
```
Subject <---- Observer
   |             ^
   |             |
ConcreteSubject  ConcreteObserver
```

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

## 2. Strategy
**Intent:** Define a family of algorithms, encapsulate each one, and make them interchangeable.

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

## 3. Command
**Intent:** Encapsulate a request as an object, thereby letting you parameterize clients with different requests.

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
