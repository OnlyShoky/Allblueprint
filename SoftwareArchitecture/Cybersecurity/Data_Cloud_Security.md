# Data and Cloud Security

## Data Security

### Encryption
- **At Rest:** Encrypting data stored on disk (DB, S3). Use AES-256.
- **In Transit:** Encrypting data moving over network. Use TLS 1.2+.

### Hashing vs. Encryption
- **Encryption:** Reversible (with key). Used for data you need to read back.
- **Hashing:** One-way. Used for passwords.

### Sensitive Data Protection
- **PII (Personally Identifiable Information):** Names, emails, SSNs.
- **Masking/Redaction:** Hide parts of data in logs/UI (e.g., `****-****-****-1234`).
- **Tokenization:** Replace sensitive data with a non-sensitive equivalent.

## Cloud Security Best Practices

### Shared Responsibility Model
- **Provider:** Security *of* the cloud (Hardware, Network).
- **Customer:** Security *in* the cloud (Data, Config, OS).

### IAM (Identity and Access Management)
- **Principle of Least Privilege:** Grant only permissions necessary for the task.
- **Roles vs. Users:** Assign permissions to roles, assume roles from compute resources (e.g., EC2 Instance Profile).

### Network Security
- **VPC (Virtual Private Cloud):** Isolate resources.
- **Security Groups:** Firewall rules (allow only specific ports/IPs).
- **Bastion Hosts:** Jump servers for SSH access (or use Systems Manager).
