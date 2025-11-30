# API and Microservice Security

#security #api #microservices #cybersecurity

> [!important] Distributed System Security
> Microservices and APIs introduce unique security challenges. Each service boundary is a potential attack surface that must be properly secured.

**Related:** [[SecureCoding|Secure Coding]] · [[Auth_Authorization|Authentication]] · [[../ModernArchitectures/Monolith_Microservices|Microservices]] · [[../BestPractices/Scalability_Resilience#Rate Limiting|Rate Limiting]]

---

## API Gateway Security

> [!success] Central Security Layer
> API Gateways provide a single entry point to enforce authentication, rate limiting, and monitoring.

**Responsibilities:**
- Authentication/authorization
- Rate limiting
- Request/response transformation
- SSL termination
- Logging and monitoring

**Tools:** Kong, AWS API Gateway, Azure API Management, Nginx

**Related:** Foundation of [[../ModernArchitectures/Monolith_Microservices#API Gateway|microservices architecture]].

---

## Authentication Patterns

### 1. API Keys

**Use Case:** Simple, non-human clients (scripts, IoT devices).

**Implementation:**
```
GET /api/users
X-API-Key: abc123xyz456
```

> [!warning] Limited Security
> API keys don't identify users, only applications. Not suitable for user-facing APIs.

**Best Practices:**
- Rotate regularly
- Use HTTPS only
- Rate limit per key

---

### 2. OAuth 2.0

**Use Case:** User-authorized third-party access.

**Client Credentials Flow (M2M):**
```python
# Service-to-service authentication
response = requests.post('https://auth.example.com/token', data={
    'grant_type': 'client_credentials',
    'client_id': 'service-a',
    'client_secret': 'secret123'
})
access_token = response.json()['access_token']
```

> [!success] Industry Standard
> OAuth 2.0 is the gold standard for API authorization, especially for [[../ModernArchitectures/Monolith_Microservices#Microservices|microservices]].

**Related:** See [[Auth_Authorization#OAuth 2.0|OAuth details]].

---

### 3. Mutual TLS (mTLS)

**Concept:** Both client and server present certificates.

**Use Case:** Service-to-service communication in zero-trust environments.

> [!important] Zero Trust
> mTLS provides strong authentication without relying on network security. Perfect for [[../ModernArchitectures/CloudNative|service meshes]].

**Tools:** Istio, Linkerd, Consul Connect

---

## Rate Limiting

> [!tip] Protect Your Resources
> Rate limiting prevents abuse, DDoS attacks, and ensures fair usage.

**Strategies:**

| Strategy | Description | Use Case |
|----------|-------------|----------|
| **Fixed Window** | N requests per fixed time window | Simple APIs |
| **Sliding Window** | N requests in rolling time window | More accurate |
| **Token Bucket** | Refilling bucket of tokens | Handle bursts |
| **Leaky Bucket** | Smooth request rate | Steady throughput |

**Implementation Example:**
```python
from flask_limiter import Limiter

limiter = Limiter(app, key_func=lambda: request.headers.get('X-API-Key'))

@app.route('/api/users')
@limiter.limit("100 per hour")
def get_users():
    return jsonify(users)
```

**Related:** Part of  [[../BestPractices/Scalability_Resilience#Rate Limiting|resilience patterns]].

---

## Input Validation

> [!danger] Never Trust Input
> All API input must be validated. This prevents injection, XSS, and malformed data from breaking your system.

**Validation Checklist:**
- Type checking (string, number, boolean)
- Length/size limits
- Format validation (email, URL, UUID)
- Allowlist validation (enum values)
- Sanitization (remove dangerous characters)

**Example (Python with Pydantic):**
```python
from pydantic import BaseModel, EmailStr, constr

class UserCreate(BaseModel):
    email: EmailStr
    name: constr(min_length=1, max_length=100)
    age: int = Field(ge=0, le=150)
```

**Related:** Critical for [[SecureCoding#Injection|preventing injection attacks]].

---

## API Versioning

> [!note] Breaking Changes
> Versioning allows clients to migrate gradually while maintaining backward compatibility.

**Strategies:**
- URL path: `/api/v1/users`, `/api/v2/users`
- Header: `Accept: application/vnd.myapi.v1+json`
- Query parameter: `/api/users?version=1`

---

## CORS (Cross-Origin Resource Sharing)

**Problem:** Browsers block cross-origin requests for security.

**Solution:** Configure CORS headers to allow specific origins.

```python
@app.after_request
def after_request(response):
    response.headers.add('Access-Control-Allow-Origin', 'https://trusted-site.com')
    response.headers.add('Access-Control-Allow-Headers', 'Content-Type,Authorization')
    response.headers.add('Access-Control-Allow-Methods', 'GET,POST,PUT,DELETE')
    return response
```

> [!warning] Avoid Wildcard
> Never use `Access-Control-Allow-Origin: *` for APIs that require authentication.

---

## Security Headers

**Essential Headers:**

| Header | Purpose |
|--------|---------|
| `Content-Security-Policy` | Prevent XSS |
| `X-Frame-Options` | Prevent clickjacking |
| `X-Content-Type-Options` | Prevent MIME sniffing |
| `Strict-Transport-Security` | Force HTTPS |

---

## API Security Checklist

> [!success] Production Readiness
> - [ ] All endpoints require authentication
> - [ ] Authorization checks on every resource
> - [ ] Rate limiting implemented
> - [ ] Input validation on all inputs
> - [ ] HTTPS only (no HTTP)
> - [ ] Security headers configured
> - [ ] Logging authentication events
> - [ ] API versioning strategy
> - [ ] CORS properly configured
> - [ ] Secrets in environment variables (not code)

---

## Further Reading

- Implement [[Auth_Authorization|OAuth 2.0 flows]]
- Secure with [[SecureCoding|OWASP best practices]]
- Monitor via [[../BestPractices/Observability|distributed tracing]]
- Test [[../BestPractices/Testing_TDD_BDD|API security]]
- Deploy with [[../ModernArchitectures/CloudNative|service mesh]]

**Tags:** #security #api #microservices #oauth #rate-limiting #api-gateway
