- Is a powerful `secrets managemnet tool` use to securely store, manage, and control access to sensitive data like passwords, API keys, certificates, and tokens in cloud-native.

Why its is used?

- Centeralization
- Security
- Automation
- Scalability

## List of the HashiCorp Vault Mode

### 1️⃣ **Dev Mode**
- In-memory vault
- Auto-unsealed and Single root token
**Use Case:-**
- Local Testing 
- Learning Vault CLI/UI
- Demos and POCs
```bash
vault server -dev
```

### 2. 2️⃣ **Server (Production) Mode**
- In-memory Vault
- Auto-unsealed
- Single root token
**Use Case:-**
- Real applications
- Cloud / on-prem deployments
- Secure secrets at scale
```bash
vault server -config=vault.hcl
```

### 3️⃣ **Sealed Mode**
- Vault is locked
- Secrets are encrypted
- No read/write allowed
**Use Case:-**
- Startup security
- Protection after restart
- Prevent data access without unseal keys
```bash
vault status
vault operator unseal
```

### 4️⃣ **Unsealed Mode**
- Vault is active
- Secrets can be accessed
- Requires unseal keys or auto-unseal
**Use Case:-**
- Normal operational state
- App authentication
- Secret retrieval

### 5️⃣ **HA (High Availability) Mode**
- Multiple Vault nodes
- One active, others standby
**Use Case:-**
- Fault tolerance
- Zero downtime
- Enterprise environments
**Examples:-** Consul, Raft and Cloud storage

### 6️⃣ **Performance Replication Mode**
- Read-only replicas
- Sync secrets from primary
**Use Case:-**
- Multi-region reads
- Reduce latency
- Scale globally

### 7️⃣ **Disaster Recovery (DR) Mode**
- Passive replica
- Used only if primary fails
**Use Case:-**
- Backup strategy
- Business continuity