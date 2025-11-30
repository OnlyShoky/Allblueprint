# Secure Coding and OWASP Top 10

## OWASP Top 10 (Key Vulnerabilities)

### 1. Injection (SQLi, Command Injection)
**Risk:** Untrusted data is sent to an interpreter as part of a command or query.
**Prevention:** Use parameterized queries (Prepared Statements).

```python
# Bad
cursor.execute("SELECT * FROM users WHERE name = '" + user_input + "'")

# Good
cursor.execute("SELECT * FROM users WHERE name = %s", (user_input,))
```

### 2. Broken Access Control
**Risk:** Users acting outside of their intended permissions.
**Prevention:** Deny by default. Implement role-based access control (RBAC) on every endpoint.

### 3. Cryptographic Failures
**Risk:** Exposure of sensitive data (passwords, health records).
**Prevention:**
- Encrypt data at rest and in transit (TLS).
- Use strong hashing algorithms (Argon2, bcrypt) for passwords.

### 4. Insecure Design
**Risk:** Flaws in architecture (e.g., lack of rate limiting).
**Prevention:** Threat modeling during design phase.

### 5. Security Misconfiguration
**Risk:** Default passwords, verbose error messages, open cloud storage.
**Prevention:** Automate hardening, remove unused features.

## General Secure Coding Guidelines
- **Input Validation:** Validate all input against a strict allowlist.
- **Output Encoding:** Encode data before rendering to prevent XSS.
- **Error Handling:** Do not leak stack traces to users.
- **Least Privilege:** Run services with minimum necessary permissions.
