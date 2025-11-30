# CI/CD and DevOps

#cicd #devops #automation #deployment #best-practices

> [!important] Automation First
> CI/CD and DevOps culture transform how teams deliver software—from manual, error-prone deployments to automated, reliable pipelines that ship code multiple times per day.

**Related:** [[Testing_TDD_BDD|Testing]] · [[../ ModernArchitectures/CloudNative|Cloud-Native]] · [[Observability|Observability]] · [[../DataAndAI/MLOps|MLOps]]

---

## Continuous Integration (CI)

**Practice:** Developers frequently merge code changes into a central repository where automated builds and tests run.  
**Goal:** Find and fix bugs quicker, improve software quality.

> [!success] Fast Feedback
> CI provides fast feedback on code quality. Failing tests are caught within minutes, not days.

**Pipeline Steps:**
1. Code Commit (Git push)
2. Linting & Static Analysis
3. Unit Tests
4. Build Artifact (e.g., Docker image)
5. Report results

**Related:** Requires comprehensive [[Testing_TDD_BDD|automated testing]] and [[../Principles/SOLID|clean code]].

---

## Continuous Delivery/Deployment (CD)

**Continuous Delivery:** Code changes are automatically built, tested, and prepared for release to production. Requires manual approval to deploy.

**Continuous Deployment:** Every change that passes all stages is released to customers automatically (no manual gate).

**Pipeline Steps:**
1. Integration Tests
2. Deploy to Staging
3. E2E Tests
4. Security Scans
5. Deploy to Production (auto or manual)

> [!warning] Deployment vs Delivery
> Delivery keeps code *deployable*. Deployment *automatically deploys*. Choose based on risk tolerance and compliance needs.

**Related:**  [[Scalability_Resilience|Resilience patterns]] for safe deployments.

---

## DevOps Culture

**Philosophy:** Collaboration between Development and Operations teams to deliver faster, more reliably.

**Practices:**
- Infrastructure as Code (IaC) - Terraform, Ansible
- Automated Monitoring - Prometheus, Datadog
- Short Feedback Loops - Deploy often, learn fast
- Shared Responsibility - Developers own operational metrics

> [!tip] You Build It, You Run It
> DevOps breaks down silos. Teams that write code also monitor and operate it in production.

**Related:** Essential for [[../ModernArchitectures/Monolith_Microservices#Microservices|microservices]] and [[../ModernArchitectures/CloudNative|cloud-native apps]].

---

## Example: GitHub Actions Workflow

```yaml
name: CI/CD Pipeline
on: [push]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Run Linter
        run: npm run lint
      - name: Run Tests
        run: npm test
      - name: Build Docker Image
        run: docker build -t myapp:latest .
      - name: Push to Registry
        run: docker push myapp:latest
```

**Related:** Implement with [[../ModernArchitectures/CloudNative#Infrastructure as Code|IaC tools]].

---

## Best Practices

| Practice | Description | Benefit |
|----------|-------------|---------|
| **Trunk-Based Development** | Merge to main frequently | Fewer merge conflicts |
| **Feature Flags** | Deploy code disabled, enable later | Safe rollouts |
| **Blue-Green Deployment** | Two identical environments, switch traffic | Zero downtime |
| **Canary Releases** | Gradual rollout to subset of users | Risk mitigation |

**Related:** [[Scalability_Resilience#Deployment Strategies|Deployment patterns]].

---

## Further Reading

- Test with [[Testing_TDD_BDD|TDD/BDD]]
- Monitor via [[Observability|observability tools]]
- Secure [[../Cybersecurity/SecureCoding|CI/CD pipelines]]
- Apply to [[../DataAndAI/MLOps|ML workflows]]

**Tags:** #cicd #devops #automation #deployment #infrastructure-as-code
