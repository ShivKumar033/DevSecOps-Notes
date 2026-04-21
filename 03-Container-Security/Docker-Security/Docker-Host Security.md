## 🔐 Secure Docker Daemon (`dockerd`)
### 1️⃣ Don’t Expose Docker API (TCP)

```bash
# ❌ BAD
dockerd -H tcp://0.0.0.0:2375
```

- No auth
- Remote root access

✅ **GOOD**

```bash
dockerd -H unix:///var/run/docker.sock
```

✅ **If remote access is required → TLS**

```bash
dockerd --tlsverify --tlscacert=ca.pem --tlscert=server-cert.pem --tlskey=server-key.pem -H=0.0.0.0:2376
```

✔ Only trusted clients can talk to daemon

---
### 2️⃣ Enable Rootless Docker (BIG WIN)

✅ **Rootless mode**

```bash
dockerd-rootless-setuptool.sh install
```

**Why**
- Docker daemon runs as **user**
- docker.sock ≠ root anymore

✔ Reduces full-host takeover impact

---
### 3️⃣ Harden Daemon Config

```bash
/etc/docker/daemon.json
```

✅ **Secure baseline**

```bash
{   
	"icc": false,   
	"live-restore": true,   
	"no-new-privileges": true,   
	"userns-remap": "default",   
	"log-level": "info" 
}
```

**Why**
- `icc:false` → containers can’t freely talk
- `userns-remap` → container root ≠ host root
- `no-new-privileges` → blocks privilege escalation

Restart:
```bahs
systemctl restart docker
```
---

### 4️⃣ Restrict Docker Group

```bash
# ❌ BAD
usermod -aG docker user
```

Why bad:
- `docker` group = root

✅ **GOOD**
- Remove unnecessary users
- Use `sudo docker` instead

```bash
gpasswd -d user docker
```

## Secure `/var/run/docker.sock`
### 5️⃣ Never Mount docker.sock Into Containers

```bash
# ❌ CRITICAL MISCONFIG
docker run -v /var/run/docker.sock:/var/run/docker.sock evil
```

**Exploit**

```bash
docker run -v /:/host alpine chroot /host /bin/bash # → root on host
```

✅ **GOOD**

- Don’t mount it
- Use Docker API proxies with auth if required

---

### 6️⃣ Use Docker Socket Proxy (If Needed)

Example: **read-only proxy**

```bash
docker run -d -p 127.0.0.1:2375:2375 -e CONTAINERS=1 -e IMAGES=1 tecnativa/docker-socket-proxy
```

✔ Limits API surface  
✔ No container creation / exec


## 🧱 Create `/etc/docker/daemon.json` 
- when you want custom security configuration of docker.
- Global Docker security policy

### Create the files
```bash
sudo nano /etc/docker/daemon.json
```

### Add namespace-related config (example)
```bash
{
  "userns-remap": "default",
  "no-new-privileges": true,
  "icc": false
}
```

### Restart the Docker Daemon
```bash
sudo systemctl restart docker
systemctl status docker
```

### Verify It Worked
```bash
### Check user namespace
docker info | grep -i userns

### Check dockremap user
getent passwd dockremap

### Check UID mappings
cat /etc/subuid
cat /etc/subgid
```

### Test Namespace Isolation
```bash
docker run --rm alpine id

# On Host machine Command:
ps -eo pid,user,cmd | grep containerd

➡️ Container root ≠ host root (mapped UID)
```

---
## ✅ Example: **Security-Hardened daemon.json**
```bash
{
  "userns-remap": "default",
  "no-new-privileges": true,
  "icc": false,
  "live-restore": true,

  "log-driver": "json-file",
  "log-opts": {
    "max-size": "10m",
    "max-file": "3"
  },

  "iptables": true,
  "ip-forward": true,
  "ip-masq": true,

  "default-ulimits": {
    "nofile": {
      "Name": "nofile",
      "Hard": 64000,
      "Soft": 64000
    }
  },

  "exec-opts": ["native.cgroupdriver=systemd"],

  "storage-driver": "overlay2",

  "seccomp-profile": "/etc/docker/seccomp.json"
}
```

## 🧠 Pentester’s Mental Model
- If attacker controls **docker.sock**,  
- daemon.json no longer matters.