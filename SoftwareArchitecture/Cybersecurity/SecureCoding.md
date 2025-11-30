# Secure Coding and OWASP Top 10

#security #owasp #secure-coding #vulnerabilities #cybersecurity

> [!important] Security First
> Secure coding isn't optional—it's foundational. The OWASP Top 10 represents the most critical security risks to web applications. Understanding and mitigating these vulnerabilities is essential for every developer.

**Related:** [[Auth_Authorization|Authentication]] · [[API_Microservice_Security|API Security]] · [[Data_Cloud_Security|Cloud Security]] · [[../BestPractices/Testing_TDD_BDD|Security Testing]]

---

## OWASP Top 10 (2021)

### 1. Broken Access Control

**Risk:** Users acting outside of their intended permissions.

> [!danger] Critical Vulnerability
> Access control failures jumped to #1 in 2021. Always implement authorization checks on every endpoint.

**Prevention:**
- Deny by default (whitelist, not blacklist)
- Implement role-based access control (RBAC)
- Log access control failures
- Validate permissions on server-side (never trust client)

**Related:** See [[Auth_Authorization|Authentication & Authorization patterns]].

---

### 2. Cryptographic Failures

**Risk:** Exposure of sensitive data (passwords, credit cards, health records).

> [!warning] Data At Risk
> Formerly "Sensitive Data Exposure." Focus on protecting data in transit and at rest.

**Prevention:**
- Encrypt data at rest and in transit (TLS 1.2+)
- Use strong hashing algorithms (Argon2, bcrypt, scrypt) for passwords
- Never store passwords in plain text
- Use HTTPS everywhere
- Implement HSTS (HTTP Strict Transport Security)

**Related:** [[Data_Cloud_Security|Data encryption strategies]].

---

### 3. Injection (SQL, Command, LDAP)

**Risk:** Untrusted data sent to an interpreter as part of a command or query.

> [!danger] Still Dangerous
> Despite being known for decades, injection remains a top threat. SQLi can lead to complete database compromise.

**Prevention:** Use parameterized queries (Prepared Statements).

```python
# Bad - SQL Injection Vulnerable
cursor.execute("SELECT * FROM users WHERE name = '" + user_input + "'")

# Good - Parameterized Query
cursor.execute("SELECT * FROM users WHERE name = %s", (user_input,))
```

**Related:** Essential for [[../DataAndAI/DataEngineering|data pipeline security]].

---

### 4. Insecure Design

**Risk:** Flaws in architecture (e.g., lack of rate limiting, no threat modeling).

> [!important] Shift Left
> Security must be considered during design phase, not bolted on after.

**Prevention:**
- Threat modeling during design
- Secure design patterns  
- Security requirements in user stories
- Implement [[../BestPractices/Scalability_Resilience#Rate Limiting|rate limiting]]

**Related:** Apply [[../DesignPatterns/Architectural|architectural patterns]] with security in mind.

---

### 5. Security Misconfiguration

**Risk:** Default passwords, verbose error messages, open cloud storage, unnecessary features enabled.

> [!tip] Harden Everything
> Most breaches involve misconfiguration, not novel exploits.

**Prevention:**
- Automate hardening with IaC
- Remove unused features, frameworks, dependencies
- Implement security headers (CSP, X-Frame-Options)
- Regular security audits
- Never expose stack traces to users

**Related:** [[../ModernArchitectures/CloudNative#Infrastructure as Code|IaC best practices]].

---

### 6. Vulnerable and Outdated Components

**Risk:** Using libraries with known vulnerabilities.

**Prevention:**
- Regular dependency updates
- Use dependency scanning (Snyk, Dependabot)
- Remove unused dependencies
- Monitor CVE databases

**Related:** Integrate into [[../BestPractices/CICD_DevOps|CI/CD pipelines]].

---

### 7. Identification and Authentication Failures

**Risk:** Weak passwords, session hijacking, credential stuffing.

**Prevention:**
- Implement MFA (Multi-Factor Authentication)
- Use strong password policies
- Implement account lockout
- Secure session management
- Use secure, random session IDs

**Related:** See [[Auth_Authorization|comprehensive auth patterns]].

---

### 8. Software and Data Integrity Failures

**Risk:** Insecure CI/CD, unsigned updates, untrusted deserialization.

**Prevention:**
- Sign releases and verify signatures
- Use integrity checks (checksums, digital signatures)
- Secure CI/CD pipelines
- Review third-party code

**Related:** [[../BestPractices/CICD_DevOps|Secure CI/CD practices]].

---

### 9. Security Logging and Monitoring Failures

**Risk:** Insufficient logging makes breaches undetectable.

**Prevention:**
- Log all authentication events
- Log access control failures
- Centralized log management
- Real-time alerting
- Regular log review

**Related:** [[../BestPractices/Observability|Comprehensive observability]].

---

### 10. Server-Side Request Forgery (SSRF)

**Risk:** Attacker tricks server into making requests to unintended locations.

**Prevention:**
- Validate and sanitize all user input
- Use allowlists for permitted destinations
- Disable unnecessary URL schemas
- Segment networks

**Related:** Critical for [[API_Microservice_Security|API security]].

---

## General Secure Coding Guidelines

> [!success] Security Checklist
> Apply these principles to every feature you build.

| Practice | Description |
|----------|-------------|
| **Input Validation** | Validate all input against strict allowlist |
| **Output Encoding** | Encode data before rendering to prevent XSS |
| **Error Handling** | Never leak stack traces to users |
| **Least Privilege** | Run services with minimum necessary permissions |
| **Defense in Depth** | Multiple layers of security |
| **Fail Securely** | Fail closed, not open |

---

## Further Reading

- Implement [[Auth_Authorization|robust authentication]]
- Secure [[API_Microservice_Security|APIs and microservices]]
- Protect [[Data_Cloud_Security|data in cloud]]
- Test with [[../BestPractices/Testing_TDD_BDD|security testing frameworks]]
- Monitor via [[../BestPractices/Observability|security logging]]

**Tags:** #security #owasp #secure-coding #vulnerabilities #injection #xss
