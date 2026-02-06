### Step 1. Install Vault (Linux / Kali)
```bash
sudo apt update
sudo apt install -y gnupg software-properties-common curl

curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
sudo apt-add-repository \
  "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"

sudo apt update
sudo apt install vault
```

Verify
```bash
vault version
```
---
### Step 2. Start Vault (Dev Mode)
```bash
vault server -dev
```
Copy:-
- **Root Token**
- **Vault Address** (`http://127.0.0.1:8200`)

New Terminal
```bash
export VAULT_ADDR=http://127.0.0.1:8200
export VAULT_TOKEN=s.xxxxx
```

Check Status of Vault:-
```bash
vault status
```
#### What You Do With Vault (IN SHORT)
Vault = **Store → Control → Rotate → Audit secrets**

---
### Step 3. Store Secrets (Basic Use)
Enable KV engine:
```bash
# KV engine = a secure key-value store inside HashiCorp Vault
vault secrets enable kv

# Example 
db_password → S3cr3tP@ss
api_key     → sk_live_xxx
```

Puts Secrets:-
```bash
vault kv put secret/api key=ABC123
```

Read secret:
```bash
vault kv get secret/api
```



