# Edge Computing

**Definition:** Computing that is done at or near the source of the data, instead of relying on the cloud at one of a dozen data centers to do all the work.

## Key Concepts
- **Latency:** Reduced by processing data closer to the user.
- **Bandwidth:** Less data needs to be sent to the cloud.
- **Privacy:** Sensitive data can be processed locally.

## Use Cases
- **IoT:** Smart factories, autonomous vehicles.
- **CDN:** Edge functions (AWS Lambda@Edge, Cloudflare Workers) for dynamic content.

## Architecture
```
[IoT Device] --> [Edge Gateway/Server] --> [Cloud]
   (Sensors)      (Local Processing)     (Long-term storage, Aggregation)
```

**Pros:**
- Low latency.
- Bandwidth savings.
- Offline capabilities.

**Cons:**
- Maintenance of distributed infrastructure.
- Security at the edge.
