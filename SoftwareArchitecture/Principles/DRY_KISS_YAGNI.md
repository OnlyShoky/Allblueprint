# DRY, KISS, YAGNI

#principles #clean-code #simplicity

> [!note] Core Principles for Clean Code
> These three principles guide you toward writing maintainable, efficient, and understandable code. They complement [[SOLID|SOLID principles]] and form the foundation of pragmatic software development.

**Related Topics:** [[SOLID|SOLID Principles]] · [[GRASP|GRASP]] · [[../BestPractices/Testing_TDD_BDD|Testing]]

---

## 1. DRY (Don't Repeat Yourself)

**Definition:** Every piece of knowledge must have a single, unambiguous, authoritative representation within a system.

**Why:** Reduces maintenance effort. If logic is duplicated, you have to fix bugs in multiple places.

> [!important] The DRY Principle
> Don't duplicate logic—extract it into reusable functions, classes, or modules. Changes should only need to happen in one place.

**Example (JavaScript):**

```javascript
// Bad: Duplication
function calculateTaxUS(price) { return price * 0.1; }
function calculateTaxUK(price) { return price * 0.2; }

// Good: DRY
function calculateTax(price, rate) {
    return price * rate;
}

const usTax = calculateTax(100, 0.1);
const ukTax = calculateTax(100, 0.2);
```

**Related:** DRY supports [[SOLID#Single Responsibility Principle|SRP]] and [[../DesignPatterns/Structural#Decorator|decorator patterns]] for code reuse.

---

## 2. KISS (Keep It Simple, Stupid)

**Definition:** Most systems work best if they are kept simple rather than made complicated.

**Why:** Simple code is easier to understand, debug, and maintain.

> [!tip] Simplicity Wins
> Resist the urge to over-engineer. Write code that's easy for others (and future you) to understand. Complexity should only be added when absolutely necessary.

**Example (Python):**

```python
# Bad: Over-engineered
def get_day(day_num):
    days = {1: 'Mon', 2: 'Tue', 3: 'Wed'}
    try:
        return days[day_num]
    except KeyError:
        return None

# Good: Simple and clear
def get_day(day_num):
    days = ['Mon', 'Tue', 'Wed']
    if 1 <= day_num <= 3:
        return days[day_num - 1]
    return None
```

**Related:** KISS aligns with [[Functional_Reactive#Pure Functions|pure functions]] and [[../BestPractices/Testing_TDD_BDD|testable code]].

---

## 3. YAGNI (You Aren't Gonna Need It)

**Definition:** Always implement things when you actually need them, never when you just foresee that you need them.

**Why:** Prevents over-engineering and wasting time on features that might never be used.

> [!warning] Avoid Premature Optimization
> Don't build features "just in case." Wait until you have a real requirement. This saves time and keeps the codebase lean.

**Application:**
- Don't add a caching layer until you have performance issues
- Don't make a class generic until you have a second use case for it
- Don't build complex abstractions until patterns emerge

**Example:**
```python
# Bad: Building for imagined future needs
class UserService:
    def __init__(self, cache=None, logger=None, metrics=None):
        self.cache = cache  # Not used yet
        self.logger = logger  # Not used yet
        self.metrics = metrics  # Not used yet
    
    def get_user(self, id):
        return self.db.find(id)

# Good: Add complexity when needed
class UserService:
    def get_user(self, id):
        return self.db.find(id)
```

**Related:** YAGNI works well with [[../ModernArchitectures/Monolith_Microservices#Start with Monolith|starting with monoliths]] and [[../BestPractices/CICD_DevOps|iterative development]].

---

## Summary Table

| Principle | Focus | Key Benefit |
|-----------|-------|-------------|
| **DRY** | Eliminate duplication | Single source of truth, easier maintenance |
| **KISS** | Keep it simple | Easier to understand and debug |
| **YAGNI** | Build only what's needed | Avoid wasted effort, lean codebase |

---

## Practical Application

> [!tip] How to Apply These Principles
> 1. **Code Review:** Ask "Is this repeated?", "Is this simple?", "Do we need this now?"
> 2. **Refactoring:** Look for duplicated code blocks and extract them
> 3. **Feature Planning:** Challenge new features with "Do we really need this now?"

---

## Further Reading

- Apply these with [[SOLID|SOLID principles]]
- See how [[GRASP|GRASP patterns]] complement DRY/KISS/YAGNI
- Learn about [[../BestPractices/Testing_TDD_BDD|TDD]] to maintain simplicity
- Explore [[Functional_Reactive|functional programming]] for cleaner code

**Tags:** #principles #dry #kiss #yagni #clean-code
