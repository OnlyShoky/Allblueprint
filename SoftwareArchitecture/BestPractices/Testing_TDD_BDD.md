# Testing, TDD, and BDD

## Testing Levels

### 1. Unit Testing
**Scope:** Individual functions, methods, or classes.
**Goal:** Verify logic in isolation.
**Tools:** Jest (JS), Pytest (Python), JUnit (Java).

```python
# Pytest Example
def add(a, b):
    return a + b

def test_add():
    assert add(2, 3) == 5
```

### 2. Integration Testing
**Scope:** Interaction between modules or services (e.g., API + Database).
**Goal:** Verify data flow and interfaces.

### 3. End-to-End (E2E) Testing
**Scope:** Entire application flow from user perspective.
**Goal:** Verify system works as a whole.
**Tools:** Cypress, Selenium, Playwright.

## TDD (Test-Driven Development)
**Cycle:** Red -> Green -> Refactor
1. **Red:** Write a failing test.
2. **Green:** Write just enough code to pass the test.
3. **Refactor:** Improve code quality while keeping tests passing.

**Pros:**
- High code coverage.
- Better design (testable code).
- Documentation via tests.

## BDD (Behavior-Driven Development)
**Concept:** Extension of TDD that uses natural language to describe system behavior.
**Format:** Given-When-Then.

**Example (Gherkin):**
```gherkin
Feature: Login
  Scenario: Successful login
    Given I am on the login page
    When I enter valid credentials
    Then I should be redirected to the dashboard
```
**Tools:** Cucumber, Behave.
