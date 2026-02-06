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
---
### Step 3. Store Secrets and Delete Secrets (Basic Use)
Enable KV engine:
```bash
# KV engine = a secure key-value store inside HashiCorp Vault
# Default make a kv Engine path name kv..
vault secrets enable kv

# Make a own kv Engine path to store data.
vault secrets enable -path=path-name kv
```

Puts Secrets:-
```bash
# This store a Inside the kv path
vault kv put secret/api key=ABC123

# Store data own your path
vault kv put path-name/aws username-s3=imagesStore
```

Read secret:
```bash
vault kv get secret/api

# Read the secrets in Json Formate
vault kv get -formate=json secret/api

# To list the all secrets Path
vault secrets list
```

Delete:- 
```bash
# Delete the least version secrets -- Older secrets are still avaiable.
vault kv delete secret/api

# Remove secrets Only version -- Other version stay.
vault kv delete -versions=1 secret/api

# Remove Data + Metadat Fully delete all
vault kv metadata delete secret/api
```

---
---
### Step 4.  Enable a secrets engine (Different Different Engine Use)

```bash
vault secrets enable -path=custom-name <engine>

# Example:----------
vault secrets enable kv
vault secrets enable database
vault secrets enable pki
```

**KV (Key-Value) — static secrets**
```bash
vault kv put secret/api key=abcd
vault kv get secret/api
vault kv delete secret/api
```

---
**Database — dynamic DB creds**
```bash
# 👉 Auto-generated, time-limited users
vault secrets enable database

```
Configure DB:
```bash
vault write database/config/mysql \
  plugin_name=mysql-database-plugin \
  connection_url="{{username}}:{{password}}@tcp(127.0.0.1:3306)/" \
  allowed_roles="readonly"
```
Create role:
```bash
vault write database/roles/readonly \
  db_name=mysql \
  creation_statements="CREATE USER '{{name}}'@'%' IDENTIFIED BY '{{password}}';" \
  default_ttl="1h"
```
Get creds:
```bash
vault read database/creds/readonly
```

---
**AWS — dynamic cloud creds**
```bash
# 👉 IAM users/STS tokens
vault secrets enable aws
```

```bash
vault write aws/config/root \
  access_key=AKIA... \
  secret_key=xxxx
```

```bash
vault write aws/roles/s3-role \
  credential_type=iam_user \
  policy_document=@policy.json
```

```bash
vault read aws/creds/s3-role
```

---
**PKI — certificates**
```bash
# 👉 TLS certs
vault secrets enable pki
```

```bash
vault write pki/root/generate/internal \
  common_name=example.com \
  ttl=8760h
```

Issue cert:
```bash
vault write pki/issue/web \
  common_name=app.example.com
```

**SSH — dynamic SSH access**
```bash
# 👉 OTP or CA-based SSH
vault secrets enable ssh
```

```bash
vault write ssh/roles/otp-role \
  key_type=otp \
  default_user=ubuntu
```

```bash
vault write ssh/creds/otp-role ip=10.10.10.10
```

---
**Disable an engine (cleanup)**
```bash
vault secrets disable <path>

# Example:---------
vault secrets disable aws/
```

---
---
### Step 5. Control Access (Most Important)
Create policy:
```bash
nano read-api.hcl
```

```
path "secret/data/api" {
   capabilities = ["read"] 
}
```

Apply:
```
vault policy write read-api read-api.hcl
```

Create limited token:
```bash
vault token create -policy=read-api
```

Test:
```bash
export VAULT_TOKEN=s.limitedtoken vault kv get secret/api
```

**You learn:** least privilege & blast radius control.

---
---

### Step 6. App Authentication (Real Use Case)

Enable AppRole:
```bash
vault auth enable approle
```

Create role:
```bash
vault write auth/approle/role/myapp \
   token_policies=read-api \   
   token_ttl=1h
```

Get credentials:
```bash
vault read auth/approle/role/myapp/role-id vault write -f auth/approle/role/myapp/secret-id
```

Login as app:
```bash
vault write auth/approle/login \
    role_id=XXXX \
	secret_id=YYYY
```

**You learn:** how apps authenticate **without passwords**.

---
---
### Step 7.  Dynamic Secrets (🔥 Killer Feature)

Enable DB secrets (example):
```bash 
vault secrets enable database
```

Vault can:
- Create DB users on demand
- Auto-expire them
- Rotate creds automatically

**You learn:** secrets **should not be static**.

---
---
### Step 8. Environment Variable Injection
```bash
export DB_PASS=$(vault kv get -field=password secret/db)
```

Use in app:
```bash
python app.py
```
**You learn:** secure secret delivery.

---
### Step 8. Audit Logging (Blue Team Angle)

```bash
vault audit enable file file_path=/tmp/vault.log
```
**You learn:** who accessed what & when.

---
## 🌐 Vault UI (Optional but Useful)
Open:

```bash
http://127.0.0.1:8200
```

Login with root token.


