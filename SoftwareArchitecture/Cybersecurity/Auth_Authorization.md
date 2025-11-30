# Authentication and Authorization

#security #auth #oauth #jwt #cybersecurity

> [!important] Identity and Access Control
> Authentication verifies WHO a user is. Authorization determines WHAT they can do. Both are critical security layers that must be implemented correctly.

**Related:** [[SecureCoding|Secure Coding]] · [[API_Microservice_Security|API Security]] · [[Data_Cloud_Security|Cloud Security]]

---

## Authentication (AuthN)

**Definition:** Verifying *who* a user is.

### Session-Based Authentication

**How it works:** Server stores session ID in cookie/memory. Stateful.

**Pros:** Simple, revocable  
**Cons:** Doesn't scale horizontally without shared session store

> [!note] Traditional Web Apps
> Session-based auth is common in traditional server-rendered web applications.

---

### Token-Based Authentication (JWT)

**How it works:** Server issues a signed token. Stateless.

**JWT Structure:** `Header.Payload.Signature`

```json
{
  "sub": "1234567890",
  "name": "John Doe",
  "iat": 1516239022,
  "exp": 1516242622
}
```

> [!success] Scalability
> JWT enables stateless authentication, perfect for [[../ModernArchitectures/Monolith_Microservices#Microservices|microservices]] and [[../ModernArchitectures/CloudNative|cloud-native apps]].

**Usage:** Passed in `Authorization: Bearer <token>` header.

**Example (Python JWT decode):**
```python
import jwt

def verify_token(token, secret):
    try:
        payload = jwt.decode(token, secret, algorithms=["HS256"])
        return payload
    except jwt.ExpiredSignatureError:
        return None
```

**Pros:** Stateless, scalable, cross-domain  
**Cons:** Can't revoke easily, token size

**Related:** Essential for [[API_Microservice_Security|API security]].

---

### SSO (Single Sign-On)

**Concept:** User logs in once to access multiple applications.

**Examples:** Google Sign-In, Okta, Azure AD

> [!tip] User Experience
> SSO dramatically improves UX and reduces password fatigue while centralizing security.

**Related:** Commonly uses [[#OAuth 2.0|OAuth 2.0]] and [[#SAML|SAML]].

---

## Authorization (AuthZ)

**Definition:** Verifying *what* a user can do.

### OAuth 2.0

**Role:** Authorization framework (NOT authentication).

**Flow (Authorization Code):**
1. User clicks "Login with Google"
2. App redirects to Google
3. User approves permissions
4. Google redirects back with `code`
5. App exchanges `code` for `access_token`
6. App uses token to access user's Google resources

> [!important] OAuth  is for Authorization
> OAuth 2.0 is often misused for authentication. Use OpenID Connect (OIDC) for authentication on top of OAuth.

**Grant Types:**
- Authorization Code (most secure, for web apps)
- Client Credentials (machine-to-machine)
- Refresh Token (long-lived access)

**Related:** Critical for [[API_Microservice_Security#OAuth|API authorization]].

---

### RBAC (Role-Based Access Control)

**Concept:** Permissions assigned to roles, users assigned to roles.

**Example:**
- Role: `admin` → Permissions: `read`, `write`, `delete`
- Role: `viewer` → Permissions: `read`
- User: John → Roles: `admin`

> [!success] Scalable Permissions
> RBAC scales better than per-user permissions. Add users to roles instead of managing individual permissions.

**Implementation:**
```python
def require_role(role):
    def decorator(f):
        def wrapper(*args, **kwargs):
            if current_user.role != role:
                abort(403)
            return f(*args, **kwargs)
        return wrapper
    return decorator

@app.route('/admin')
@require_role('admin')
def admin_panel():
    return "Admin Area"
```

**Related:** Foundation of [[../ModernArchitectures/Monolith_Microservices#Microservices|microservices security]].

---

### ABAC (Attribute-Based Access Control)

**Concept:** Fine-grained access control based on attributes (user attributes, resource attributes, environment).

**Example:** Allow access if:
- User department = "Sales"
- Resource owner = user
- Time = business hours

> [!note] More Flexible Than RBAC
> ABAC handles complex scenarios where RBAC becomes unwieldy.

---

## Security Best Practices

| Practice | Description | Why |
|----------|-------------|-----|
| **Always use HTTPS** | Encrypt all traffic | Prevent token interception |
| **HttpOnly Cookies** | Store tokens in HttpOnly cookies | Prevent XSS attacks |
| **Short-lived Tokens** | JWT expires in 15-60 min | Limit damage if compromised |
| **Refresh Tokens** | Long-lived, can be revoked | Balance security and UX |
| **MFA (Multi-Factor)** | Require 2+ auth factors | Prevent credential stuffing |
| **Rate Limiting** | Limit login attempts | Prevent brute force |

> [!warning] Token Storage
> **Never** store JWTs in localStorage on web. Use HttpOnly cookies or sessionStorage with appropriate security headers.

---

## Common Vulnerabilities

> [!danger] Security Pitfalls
> - **Client-side validation only:** Always validate on server
> - **Weak password policies:** Enforce strong passwords + MFA
> - **Session fixation:** Regenerate session IDs after login
> - **CSRF attacks:** Use CSRF tokens for state-changing operations

---

## Further Reading

- Implement [[SecureCoding|secure coding practices]]
- Secure [[API_Microservice_Security|microservices with OAuth]]
- Protect [[Data_Cloud_Security|data with encryption]]
- Test [[../BestPractices/Testing_TDD_BDD|authentication flows]]
- Monitor [[../BestPractices/Observability|auth events]]

**Tags:** #security #authentication #authorization #oauth #jwt #rbac
