# Data and Cloud Security

#security #cloud #encryption #cybersecurity #data-protection

> [!important] Protecting Data Everywhere
> Data security is about protecting information at rest, in transit, and in use. Cloud security extends this to shared responsibility models and cloud-specific threats.

**Related:** [[SecureCoding|Secure Coding]] · [[Auth_Authorization|Authentication]] · [[API_Microservice_Security|API Security]] · [[../ModernArchitectures/CloudNative|Cloud-Native]]

---

## Data Security

### Encryption

> [!success] Encryption is Non-Negotiable
> All sensitive data must be encrypted. This is the last line of defense if other controls fail.

**At Rest:** Encrypting data stored on disk (databases, S3 buckets, file systems).  
**Standard:** AES-256

**In Transit:** Encrypting data moving over networks.  
**Standard:** TLS 1.2+ (deprecate TLS 1.0/1.1)

**Example (Python with cryptography):**
```python
from cryptography.fernet import Fernet

# Generate key
key = Fernet.generate_key()
cipher = Fernet(key)

# Encrypt
encrypted = cipher.encrypt(b"Sensitive data")
# Decrypt
decrypted = cipher.decrypt(encrypted)
```

**Related:** Essential for [[../DataAndAI/DataEngineering|data pipelines]] and [[../DataAndAI/DataQuality_Governance|data governance]].

---

### Hashing vs. Encryption

| Aspect | Hashing | Encryption |
|--------|---------|------------|
| **Purpose** | One-way transformation | Reversible transformation |
| **Use Case** | Passwords, integrity checks | Data you need to read back |
| **Reversible** | No | Yes (with key) |
| **Algorithms** | bcrypt, Argon2, SHA-256 | AES, RSA |

> [!warning] Never Encrypt Passwords
> Always **hash** passwords with bcrypt or Argon2. Never use MD5 or SHA-1 for passwords—they're broken.

---

### Sensitive Data Protection

**PII (Personally Identifiable Information):**
- Names, emails, phone numbers, SSNs, addresses
- Medical records, financial data

**Protection Strategies:**

| Strategy | Description | Use Case |
|----------|-------------|----------|
| **Masking/Redaction** | Hide parts in logs/UI | `****-****-****-1234` |
| **Tokenization** | Replace with non-sensitive token | Payment processing |
| **Anonymization** | Remove identifying fields | Analytics, research |
| **Pseudonymization** | Replace with fake but consistent values | GDPR compliance |

**Related:** Critical for [[../DataAndAI/DataQuality_Governance|data governance]].

---

## Cloud Security Best Practices

### Shared Responsibility Model

> [!important] Know Your Responsibilities
> Cloud security is SHARED between provider and customer. Understand where your responsibility starts.

**Provider (Security OF the cloud):**
- Hardware, network infrastructure
- Physical facilities
- Hypervisor

**Customer (Security IN the cloud):**
- Data, applications, configurations
- Operating systems, firewalls
- Identity and access management
- Encryption

---

### IAM (Identity and Access Management)

**Principle of Least Privilege:** Grant only permissions necessary for the task.

> [!tip] Start with Deny All
> Begin with no permissions, then add only what's needed. Never grant broad permissions like `*:*`.

**Example (AWS IAM Policy):**
```json
{
  "Version": "2012-10-17",
  "Statement": [{
    "Effect": "Allow",
    "Action": [
      "s3:GetObject",
      "s3:PutObject"
    ],
    "Resource": "arn:aws:s3:::my-bucket/*"
  }]
}
```

**Roles vs. Users:**
- Assign permissions to **roles**
- Services assume roles (e.g., EC2 Instance Profile, Lambda execution role)
- Use identity federation for human access (SSO)

**Related:** Implements [[Auth_Authorization#RBAC|RBAC patterns]].

---

### Network Security

**VPC (Virtual Private Cloud):** Isolate resources in private networks.

**Security Groups:** Firewall rules controlling inbound/outbound traffic.

```
# Example Security Group Rule
Type: HTTPS
Protocol: TCP
Port: 443
Source: 0.0.0.0/0  # Allow from anywhere (for web servers)

Type: SSH
Protocol: TCP
Port: 22
Source: 10.0.0.0/16  # Only from VPC (internal only)
```

> [!warning] Never Expose Everything
> Default deny all, then explicitly allow only required traffic. Never use `0.0.0.0/0` for SSH/RDP.

**Bastion Hosts:** Jump servers for SSH access (or better: use AWS Systems Manager Session Manager for SSH-less access).

**Related:** Foundation of [[../ModernArchitectures/CloudNative|cloud-native security]].

---

### Secrets Management

> [!danger] Never Hardcode Secrets
> API keys, passwords, and certificates must NEVER be in code or version control.

**Solutions:**
- AWS Secrets Manager, Azure Key Vault, HashiCorp Vault
- Environment variables (for less sensitive configs)
- Encrypted parameter stores

**Example (Python with AWS Secrets Manager):**
```python
import boto3

secrets = boto3.client('secretsmanager')
response = secrets.get_secret_value(SecretId='prod/db/password')
db_password = response['SecretString']
```

---

### Cloud-Specific Threats

| Threat | Description | Mitigation |
|--------|-------------|------------|
| **Misconfigured S3 Buckets** | Public buckets exposing data | Use bucket policies, block public access |
| **Over-Privileged IAM** | Excessive permissions | Least privilege, regular audits |
| **Unencrypted Data** | Data at rest not encrypted | Enable encryption by default |
| **Shared Tenancy Risks** | Data leakage in multi-tenant | Use dedicated instances for sensitive workloads |

---

## Compliance and Regulations

**Key Frameworks:**
- **GDPR:** EU data protection
- **HIPAA:** Healthcare data (US)
- **PCI-DSS:** Payment card data
- **SOC 2:** Security controls audit

> [!note] Compliance as Code
> Implement compliance checks in [[../BestPractices/CICD_DevOps|CI/CD pipelines]] using tools like AWS Config, Azure Policy, or Open Policy Agent.

---

## Security Checklist

> [!success] Cloud Security Essentials
> - [ ] All data encrypted at rest and in transit
> - [ ] MFA enabled for all users
> - [ ] Least privilege IAM policies
> - [ ] Security groups properly configured
> - [ ] No hardcoded secrets
> - [ ] Logging enabled (CloudTrail, GuardDuty)
> - [ ] Regular security audits
> - [ ] Backup and disaster recovery tested
> - [ ] Network segmentation implemented
> - [ ] Compliance requirements met

---

## Further Reading

- Implement [[SecureCoding|secure development practices]]
- Secure [[API_Microservice_Security|cloud APIs]]
- Use [[Auth_Authorization|strong authentication]]
- Monitor with [[../BestPractices/Observability|cloud observability]]
- Govern data with [[../DataAndAI/DataQuality_Governance|data governance]]

**Tags:** #security #cloud #encryption #iam #compliance #data-protection
