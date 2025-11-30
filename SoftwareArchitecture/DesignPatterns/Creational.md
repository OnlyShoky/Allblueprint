# Creational Design Patterns

Creational patterns deal with object creation mechanisms, trying to create objects in a manner suitable to the situation.

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

## 2. Factory Method
**Intent:** Define an interface for creating an object, but let subclasses decide which class to instantiate.

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

## 3. Builder
**Intent:** Separate the construction of a complex object from its representation.

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
