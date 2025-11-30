# Edge Computing

#edge-computing #iot #cdn #distributedcomputing #trends

> [!important] Computing at the Edge
> Edge computing brings computation and data storage closer to data sources, reducing latency and bandwidth usage. It's transforming IoT, CDNs, and latency-sensitive applications.

**Related:** [[../ModernArchitectures/Serverless_EventDriven|Serverless]] · [[../ModernArchitectures/CloudNative|Cloud-Native]] · [[../BestPractices/Scalability_Resilience|Scalability]]

---

## Core Concept

**Definition:** Computing done at or near the source of data, instead of relying on centralized cloud data centers.

**Shift:** From Cloud-Only → Cloud + Edge hybrid architecture

> [!success] Closer to Users
> By processing data closer to users or devices, edge computing dramatically reduces latency and improves user experience.

---

## Key Benefits

| Benefit | Description | Use Case |
|---------|-------------|----------|
| **Low Latency** | Millisecond response times | Gaming, AR/VR, autonomous vehicles |
| **Bandwidth Savings** | Process locally, send summaries to cloud | IoT sensors, video analytics |
| **Privacy** | Sensitive data processed locally | Healthcare devices, surveillance |
| **Offline Capability** | Works without internet | Manufacturing, remote locations |
| **Cost Reduction** | Less data transfer to cloud |  Video streaming, IoT fleets |

**Related:** Critical for [[DataDrivenArch|data-driven architectures]].

---

## Architecture

```
[IoT Devices/Sensors] 
        ↓
[Edge Gateway/Server]  ← Local processing, filtering, aggregation
        ↓
[Regional Edge]        ← ML inference, caching
        ↓
[Cloud Data Centers]   ← Long-term storage, training, analytics
```

> [!note] Hierarchical Processing
> Data is processed at multiple tiers. Only relevant/summarized data reaches the cloud.

---

## Use Cases

###  IoT and Industrial

**Smart Factories:**
- Real-time quality control
- Predictive maintenance
- Process optimization

**Autonomous Vehicles:**
- Sensor data processing (cameras, lidar)
- Real-time decision making
- Can't afford cloud latency

> [!warning] Mission Critical
> Safety-critical applications like autonomous driving CANNOT rely on cloud latency—edge processing is mandatory.

---

### CDN Edge Functions

**Concept:** Run code at CDN edge locations for dynamic content.

**Platforms:** AWS Lambda@Edge, Cloudflare Workers, Fastly Compute@Edge

**Use Cases:**
- A/B testing
- Personalization
- Authentication
- Request/response transformation
- Bot detection

**Example (Cloudflare Worker):**
```javascript
addEventListener('fetch', event => {
  event.respondWith(handleRequest(event.request))
})

async function handleRequest(request) {
  // Run at  edge, close to user
  const country = request.cf.country
  
  if (country === 'US') {
    return fetch('https://us-api.example.com')
  } else {
    return fetch('https://eu-api.example.com')
  }
}
```

**Related:** Extends [[../ModernArchitectures/Serverless_EventDriven#Serverless|serverless computing]].

---

### 5G and Mobile Edge

**MEC (Multi-Access Edge Computing):** Compute at cellular base stations.

**Use Cases:**
- AR/VR streaming
- Mobile gaming
- Real-time video analytics

---

## Edge vs Cloud Comparison

| Aspect | Cloud | Edge |
|--------|-------|------|
| **Latency** | 50-200ms | 1-10ms |
| **Bandwidth** | High | Limited |
| **Compute Power** | Massive, scalable | Limited per device |
| **Cost** | Pay-per-use | Hardware investment |
| **Management** | Centralized | Distributed (harder) |
| **Security** | Centralized | Distributed (more attack surface) |

---

## Challenges

> [!warning] Edge Complexity
> Edge computing introduces significant operational complexity.

**Key Challenges:**
- **Maintenance:** Updating software on distributed devices
- **Security:** Each edge device is a potential attack surface
- **Orchestration:** Managing thousands of edge nodes
- **Connectivity:** Handling intermittent network
- **Resource Constraints:** Limited compute/storage per device

**Related:** Requires robust [[../BestPractices/Observability|observability]] and [[../Cybersecurity/Data_Cloud_Security|security practices]].

---

## Edge ML

**Concept:** Run ML inference on edge devices (phones, cameras, drones).

**Benefits:**
- Privacy (data never leaves device)
- Low latency
- Offline capability

**Tools:** TensorFlow Lite, ONNX Runtime, Core ML (iOS)

> [!success] Privacy-First ML
> Edge ML enables AI applications without sending user data to the cloud.

**Related:** Part of [[../DataAndAI/MLOps|MLOps strategy]].

---

## Further Reading

- Architect with [[../ModernArchitectures/CloudNative|cloud-native principles]]
- Deploy with [[../BestPractices/CICD_DevOps|edge CI/CD]]
- Secure [[../Cybersecurity/Data_Cloud_Security|distributed systems]]
- Monitor [[../BestPractices/Observability|edge infrastructure]]
- Build ML with [[../DataAndAI/ML_DL_Patterns|optimization patterns]]

**Tags:** #edge-computing #iot #cdn #latency #distributed #5g
