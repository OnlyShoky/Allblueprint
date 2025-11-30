# Functional and Reactive Principles

## Functional Programming Principles

### 1. Immutability
**Concept:** Data cannot be changed after creation.
**Why:** Eliminates side effects, makes code thread-safe and easier to reason about.

```javascript
// Bad (Mutation)
const arr = [1, 2];
arr.push(3);

// Good (Immutable)
const arr = [1, 2];
const newArr = [...arr, 3];
```

### 2. Pure Functions
**Concept:** Functions that always produce the same output for the same input and have no side effects.
**Why:** Easy to test and cache (memoization).

```javascript
// Pure
const add = (a, b) => a + b;
```

### 3. Higher-Order Functions
**Concept:** Functions that take other functions as arguments or return them.
**Why:** Enables powerful abstractions like `map`, `filter`, `reduce`.

## Reactive Principles (The Reactive Manifesto)

### 1. Responsive
The system responds in a timely manner if at all possible. Latency is minimized.

### 2. Resilient
The system stays responsive in the face of failure. Failures are contained, isolated, and delegated.

### 3. Elastic
The system stays responsive under varying workload. It scales up and down resources automatically.

### 4. Message Driven
Reactive systems rely on asynchronous message-passing to establish a boundary between components. This ensures loose coupling, isolation, and location transparency.

**Use Case:** Real-time data processing, high-concurrency web applications (e.g., chat apps, stock tickers).
