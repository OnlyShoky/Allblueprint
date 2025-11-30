# Structural Design Patterns

#design-patterns #structural #composition

> [!important] Assembling Objects and Classes
> Structural patterns explain how to assemble objects and classes into larger structures while keeping these structures flexible and efficient. They focus on class and object composition.

**Related Topics:** [[Creational|Creational Patterns]] · [[Behavioral|Behavioral Patterns]] · [[../Principles/GRASP|GRASP]]

---

## 1. Adapter

**Intent:** Convert the interface of a class into another interface clients expect.

**Diagram:**
```
Client -> Target Interface
              ^
              |
           Adapter -> Adaptee
```

> [!tip] Integration Pattern
> Adapter is essential when integrating third-party libraries or legacy code that doesn't match your interface expectations.

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

**Related:** Critical for [[../Principles/GRASP#Indirection|indirection in GRASP]] and [[../ModernArchitectures/Monolith_Microservices#Anti-Corruption Layer|anti-corruption layers]].

---

## 2. Composite

**Intent:** Compose objects into tree structures to represent part-whole hierarchies.

> [!success] Uniform Treatment
> Composite lets clients treat individual objects and compositions of objects uniformly. Perfect for tree structures like file systems or UI component hierarchies.

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

**Related:** Common in [[../TrendsAndInnovations/MicroFrontends|UI component trees]] and [[../DataAndAI/DataModeling|hierarchical data models]].

---

## 3. Decorator

**Intent:** Attach additional responsibilities to an object dynamically.

> [!important] Flexible Alternative to Inheritance
> Decorator provides a flexible alternative to subclassing for extending functionality. It follows the [[../Principles/SOLID#Open-Closed Principle|Open/Closed Principle]].

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

**Related:** Used in [[../BestPractices/Observability#Middleware|middleware patterns]] and [[../Cybersecurity/API_Microservice_Security#Rate Limiting|API rate limiting]].

---

## 4. Proxy

**Intent:** Provide a surrogate or placeholder for another object to control access to it.

> [!note] Access Control
> Proxy adds a level of indirection to control access, add lazy initialization, or implement caching.

**Types:**
- **Virtual Proxy:** Lazy initialization
- **Protection Proxy:** Access control
- **Remote Proxy:** Represents object in different address space

**Example (Python):**

```python
class RealService:
    def request(self):
        return "RealService: Handling request"

class Proxy:
    def __init__(self):
        self._real_service = None
    
    def request(self):
        if self._real_service is None:
            self._real_service = RealService()
        return self._real_service.request()

proxy = Proxy()
print(proxy.request())  # Lazy loads RealService
```

**Pros:** Controls access without changing client code.  
**Cons:** May introduce latency.

**Related:** Essential for [[../Cybersecurity/Auth_Authorization|authentication/authorization]] and [[../ModernArchitectures/Monolith_Microservices#API Gateway|API gateways]].

---

## 5. Facade

**Intent:** Provide a unified interface to a set of interfaces in a subsystem.

> [!tip] Simplification Layer
> Facade simplifies complex subsystems by providing a higher-level interface. It's all about making things easier for the client.

**Example (Python):**

```python
class SubsystemA:
    def operation_a(self): return "A"

class SubsystemB:
    def operation_b(self): return "B"

class Facade:
    def __init__(self):
        self.a = SubsystemA()
        self.b = SubsystemB()
    
    def simple_operation(self):
        return f"{self.a.operation_a()} + {self.b.operation_b()}"

facade = Facade()
print(facade.simple_operation())
```

**Pros:** Simplifies interface, reduces dependencies.  
**Cons:** Can become a "god object" if overused.

**Related:** Common in [[../ModernArchitectures/Monolith_Microservices#BFF|Backend for Frontend]] and [[../Principles/DRY_KISS_YAGNI#KISS|KISS principle]].

---

## 6. Bridge

**Intent:** Decouple an abstraction from its implementation so the two can vary independently.

> [!important] Separation of Concerns
> Bridge separates abstraction from implementation, allowing you to change both independently.

**Use Case:** Platform-independent UI libraries, database drivers.

**Related:** Supports [[../Principles/SOLID#Dependency Inversion Principle|DIP]] and [[../ModernArchitectures/CloudNative|multi-cloud strategies]].

---

## Summary Table

| Pattern | Intent | Use When | Principle |
|---------|--------|----------|-----------|
| **Adapter** | Interface compatibility | Integrating incompatible interfaces | [[../Principles/GRASP#Indirection\|Indirection]] |
| **Composite** | Tree structures | Part-whole hierarchies | - |
| **Decorator** | Dynamic responsibilities | Runtime behavior extension | [[../Principles/SOLID#Open-Closed Principle\|OCP]] |
| **Proxy** | Access control | Lazy loading, access control | - |
| **Facade** | Simplified interface | Complex subsystem simplification | [[../Principles/DRY_KISS_YAGNI#KISS\|KISS]] |
| **Bridge** | Decouple abstraction/implementation | Platform independence | [[../Principles/SOLID#Dependency Inversion Principle\|DIP]] |

---

## Further Reading

- Combine with [[Creational|Creational Patterns]] for powerful designs
- Apply [[../Principles/SOLID|SOLID principles]] when using these patterns
- See in [[../ModernArchitectures/Monolith_Microservices|microservices architecture]]
- Use with [[../BestPractices/Testing_TDD_BDD|TDD]] for maintainable code

**Tags:** #design-patterns #structural #adapter #decorator #proxy #facade
