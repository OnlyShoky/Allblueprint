# Structural Design Patterns

Structural patterns explain how to assemble objects and classes into larger structures while keeping these structures flexible and efficient.

## 1. Adapter
**Intent:** Convert the interface of a class into another interface clients expect.

**Diagram:**
```
Client -> Target Interface
              ^
              |
           Adapter -> Adaptee
```

**Example (Python):**
```python
class OldSystem:
    def specific_request(self):
        return "Old System Response"

class Target:
    def request(self):
        pass

class Adapter(Target):
    def __init__(self, adaptee):
        self.adaptee = adaptee
    
    def request(self):
        return self.adaptee.specific_request()

adaptee = OldSystem()
adapter = Adapter(adaptee)
print(adapter.request())
```

**Pros:** Allows incompatible classes to work together.
**Cons:** Increases complexity by adding new classes.

## 2. Composite
**Intent:** Compose objects into tree structures to represent part-whole hierarchies.

**Example (Python):**
```python
class Component:
    def operation(self): pass

class Leaf(Component):
    def operation(self):
        return "Leaf"

class Composite(Component):
    def __init__(self):
        self.children = []
    
    def add(self, component):
        self.children.append(component)
    
    def operation(self):
        results = [child.operation() for child in self.children]
        return f"Branch({'+'.join(results)})"
```

**Pros:** Easier to work with complex tree structures.
**Cons:** Can make design overly general.

## 3. Decorator
**Intent:** Attach additional responsibilities to an object dynamically.

**Example (Python):**
```python
class Coffee:
    def cost(self): return 5

class MilkDecorator:
    def __init__(self, coffee):
        self.coffee = coffee
    
    def cost(self):
        return self.coffee.cost() + 2

my_coffee = Coffee()
my_coffee_with_milk = MilkDecorator(my_coffee)
print(my_coffee_with_milk.cost()) # 7
```

**Pros:** More flexible than inheritance for extending functionality.
**Cons:** Can result in many small objects.
