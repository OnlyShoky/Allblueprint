# API and Microservice Security

## API Security
- **Rate Limiting:** Prevent abuse and DDoS.
- **Input Validation:** Reject malformed JSON/XML.
- **Authentication:** Require API keys or tokens for all endpoints.

## Microservice Security Patterns

### 1. Zero Trust Architecture
**Principle:** Never trust, always verify. Every request between services must be authenticated and authorized.

### 2. mTLS (Mutual TLS)
**Concept:** Both client and server authenticate each other using certificates.
**Implementation:** Often handled by Service Mesh (Istio, Linkerd).

### 3. API Gateway
**Role:** Central entry point handling:
- SSL Termination.
- Authentication (offloading from services).
- Rate Limiting.

**Diagram:**
```
[Client] --(HTTPS)--> [API Gateway] --(mTLS)--> [Service A]
                                    --(mTLS)--> [Service B]
```

### 4. Token Propagation
**Flow:**
1. User authenticates with Gateway -> gets JWT.
2. Gateway passes JWT to Service A.
3. Service A passes JWT to Service B (downstream).
**Risk:** "Confused Deputy" problem. Ensure audience (`aud`) claim is checked.
