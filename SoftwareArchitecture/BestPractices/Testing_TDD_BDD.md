# Testing, TDD, and BDD

#testing #tdd #bdd #quality #best-practices

> [!important] Quality Assurance Foundation
> Testing is not just about finding bugs—it's about building confidence in your code, enabling refactoring, and serving as living documentation. TDD and BDD take this further by making tests drive your design.

**Related Topics:** [[../Principles/SOLID|SOLID Principles]] · [[CICD_DevOps|CI/CD]] · [[../DesignPatterns/Behavioral#Command|Command Pattern]] · [[../Principles/DRY_KISS_YAGNI#KISS|KISS]]

---

## Testing Levels

### 1. Unit Testing

**Scope:** Individual functions, methods, or classes.  
**Goal:** Verify logic in isolation.  
**Tools:** Jest (JS), Pytest (Python), JUnit (Java), xUnit (.NET)

> [!tip] Fast and Focused
> Unit tests should be fast (milliseconds), isolated, and test a single unit of behavior. Mock dependencies to keep tests focused.

```python
# Pytest Example
def add(a, b):
    return a + b

def test_add():
    assert add(2, 3) == 5
```

**Related:** Supports [[../Principles/SOLID#Single Responsibility Principle|SRP]] and enables safe refactoring.

---

### 2. Integration Testing

**Scope:** Interaction between modules or services (e.g., API + Database).  
**Goal:** Verify data flow and interfaces.

> [!note] Real Dependencies
> Integration tests use real or test versions of external dependencies (databases, APIs) to verify components work together.

**Use Cases:** API endpoints, database queries, message queue interactions.

**Related:** Critical for [[../ModernArchitectures/Monolith_Microservices#Microservices|microservices]] and [[../DataAndAI/DataEngineering|data pipelines]].

---

### 3. End-to-End (E2E) Testing

**Scope:** Entire application flow from user perspective.  
**Goal:** Verify system works as a whole.  
**Tools:** Cypress, Selenium, Playwright, Puppeteer

> [!warning] Slow but Comprehensive
> E2E tests are slower and more brittle. Use them sparingly for critical user journeys. Rely more on unit and integration tests.

**Related:** Complements [[CICD_DevOps|CI/CD pipelines]] for deployment validation.

---

## Test-Driven Development (TDD)

**Cycle:** Red → Green → Refactor

1. **Red:** Write a failing test that defines desired behavior
2. **Green:** Write just enough code to make the test pass
3. **Refactor:** Improve code quality while keeping tests green

> [!success] Design Through Testing
> TDD forces you to think about interfaces and design before implementation. It naturally leads to more [[../Principles/SOLID|SOLID]] code.

**Pros:**
- High code coverage (by design)
- Better design (code must be testable)
- Living documentation through tests
- Confidence in refactoring

**Cons:**
- Initial learning curve
- Can slow down prototyping
- Requires discipline

**Related:** Pairs excellently with [[../Principles/SOLID#Dependency Inversion Principle|DIP]] and [[../DesignPatterns/Creational#Factory|factory patterns]].

---

## Behavior-Driven Development (BDD)

**Concept:** Extension of TDD that uses natural language to describe system behavior.  
**Format:** Given-When-Then (Gherkin syntax)

> [!tip] Collaboration Tool
> BDD bridges the gap between technical and non-technical stakeholders. Everyone understands the behavior being tested.

**Example (Gherkin):**
```gherkin
Feature: Login
  Scenario: Successful login
    Given I am on the login page
    When I enter valid credentials
    Then I should be redirected to the dashboard
```

**Tools:** Cucumber, Behave, SpecFlow

**Related:** Aligns with [[../DesignPatterns/Architectural#Hexagonal|hexagonal architecture]] for acceptance testing.

---

## Testing Best Practices

| Practice | Description | Benefit |
|----------|-------------|---------|
| **Arrange-Act-Assert** | Structure tests in three parts | Clear, readable tests |
| **Test Isolation** | Each test runs independently | Reliable, parallelizable |
| **Mock External Dependencies** | Use mocks/stubs for APIs, DBs | Fast, deterministic tests |
| **Test One Thing** | Each test verifies single behavior | Easy debugging |
| **Descriptive Names** | `test_user_cannot_login_with_invalid_password` | Self-documenting |

---

## Testing Pyramid

```
        /\
       /E2E\      < Few (slow, brittle, high value)
      /------\
     /Integr.\   < Some (medium speed, medium value)
    /----------\
   /   Unit     \ < Many (fast, stable, foundational)
  /--------------\
```

> [!important] Build Your Foundation
> Most tests should be fast unit tests. Use fewer integration tests and even fewer E2E tests. This creates a stable, fast test suite.

---

## Further Reading

- Apply [[../Principles/SOLID|SOLID principles]] for testable code
- Automate with [[CICD_DevOps|CI/CD pipelines]]
- Use [[../DesignPatterns/Creational#Builder|Builder pattern]] for test data
- Implement [[../Cybersecurity/SecureCoding|security testing]]
- Test [[../DataAndAI/MLOps|ML models]] with specialized frameworks

**Tags:** #testing #tdd #bdd #quality #unit-tests #integration-tests
