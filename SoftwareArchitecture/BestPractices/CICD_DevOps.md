# CI/CD and DevOps

## Continuous Integration (CI)
**Practice:** Developers frequently merge code changes into a central repository where automated builds and tests run.
**Goal:** Find and fix bugs quicker, improve software quality.

**Pipeline Steps:**
1. Code Commit
2. Linting & Static Analysis
3. Unit Tests
4. Build Artifact (e.g., Docker image)

## Continuous Delivery/Deployment (CD)
**Continuous Delivery:** Code changes are automatically built, tested, and prepared for a release to production. Requires manual approval to deploy.
**Continuous Deployment:** Every change that passes all stages of your production pipeline is released to your customers automatically.

**Pipeline Steps:**
1. Integration Tests
2. Deploy to Staging
3. E2E Tests
4. Deploy to Production

## DevOps Culture
**Philosophy:** Collaboration between Development and Operations teams.
**Practices:**
- Infrastructure as Code (IaC)
- Automated Monitoring
- Short Feedback Loops

**Example GitHub Actions Workflow:**
```yaml
name: CI/CD
on: [push]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Run Tests
        run: npm test
      - name: Build
        run: npm run build
```
