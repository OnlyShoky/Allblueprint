# DRY, KISS, YAGNI

Core principles for writing clean, maintainable, and efficient code.

## 1. DRY (Don't Repeat Yourself)
**Definition:** Every piece of knowledge must have a single, unambiguous, authoritative representation within a system.

**Why:** Reduces maintenance effort. If logic is duplicated, you have to fix bugs in multiple places.

**Example (JavaScript):**

```javascript
// Bad
function calculateTaxUS(price) { return price * 0.1; }
function calculateTaxUK(price) { return price * 0.2; }

// Good
function calculateTax(price, rate) {
    return price * rate;
}
```

## 2. KISS (Keep It Simple, Stupid)
**Definition:** Most systems work best if they are kept simple rather than made complicated.

**Why:** Simple code is easier to understand, debug, and maintain.

**Example (Python):**

```python
# Bad: Over-engineered
def get_day(day_num):
    days = {1: 'Mon', 2: 'Tue', 3: 'Wed'}
    try:
        return days[day_num]
    except KeyError:
        return None

# Good: Simple
def get_day(day_num):
    days = ['Mon', 'Tue', 'Wed']
    if 1 <= day_num <= 3:
        return days[day_num - 1]
    return None
```

## 3. YAGNI (You Aren't Gonna Need It)
**Definition:** Always implement things when you actually need them, never when you just foresee that you need them.

**Why:** Prevents over-engineering and wasting time on features that might never be used.

**Application:**
- Don't add a caching layer until you have performance issues.
- Don't make a class generic until you have a second use case for it.
