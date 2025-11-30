# Authentication and Authorization

## Authentication (AuthN)
**Definition:** Verifying *who* a user is.

### Mechanisms
- **Session-based:** Server stores session ID in cookie/memory. Stateful.
- **Token-based (JWT):** Server issues a signed token. Stateless.
- **SSO (Single Sign-On):** User logs in once to access multiple applications (e.g., Google Sign-In).

## Authorization (AuthZ)
**Definition:** Verifying *what* a user can do.

### OAuth 2.0
**Role:** Authorization framework.
**Flow (Authorization Code):**
1. User clicks "Login with Google".
2. App redirects to Google.
3. User approves.
4. Google redirects back with `code`.
5. App exchanges `code` for `access_token`.

### JWT (JSON Web Token)
**Structure:** `Header.Payload.Signature`
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

## Best Practices
- Always use HTTPS.
- Store tokens securely (HttpOnly cookies preferred over localStorage for web).
- Implement MFA (Multi-Factor Authentication).
