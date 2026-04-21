## 1️⃣ Host & Docker daemon auditing (baseline security)

### Tool: **Docker Bench for Security**

Checks Docker against **CIS Docker Benchmark**

### Run (read-only, safe)
```bash
docker run --rm -it \
  --net host \
  --pid host \
  --userns host \
  --cap-add audit_control \
  -v /etc:/etc:ro \
  -v /usr/bin/containerd:/usr/bin/containerd:ro \
  -v /usr/bin/runc:/usr/bin/runc:ro \
  -v /var/lib:/var/lib:ro \
  -v /var/run/docker.sock:/var/run/docker.sock:ro \
  docker/docker-bench-security
```

### 🔍 Example findings
```bash
[WARN] 2.2 Ensure the Docker daemon is not exposed
[WARN] 4.1 Ensure images are not run as root
[PASS] 5.3 Ensure no privileged containers
```

### 🚩 Red flags I care about

- Docker socket exposed
- Containers running as root
- Privileged containers
- No user namespace remapping

 **Report note**

> Host does not comply with CIS Docker Benchmark, increasing risk of container escape.

---

## 2️⃣ Docker image auditing (before deployment)

### Tool: **Trivy**

Scans:

- OS packages
- App dependencies
- Secrets
- Misconfigurations

### Scan image
```
trivy image nginx:latest
```

### Misconfig + vuln scan (recommended)
```bash
trivy image --severity HIGH,CRITICAL --misconfig nginx:latest
```

### 🔍 Example output
```bash
CRITICAL: openssl CVE-2023-0464 HIGH: libxml2 CVE-2022-40304
```

**Report note**
> Image contains critical vulnerabilities exploitable for RCE.

---

## 3️⃣ Dockerfile auditing (static analysis)

### Tool: **Hadolint**

### Scan Dockerfile

```bash
hadolint Dockerfile
```

### 🔍 Example output
```bash
DL3002: Last USER should not be root DL3007: Using latest tag is discouraged
```

### 🚩 Common findings

- `USER root`
- `FROM ubuntu:latest`
- Missing `HEALTHCHECK`

 **Fix example**
```bash
FROM ubuntu:22.04 
RUN useradd -m appuser 
USER appuser
```

---

## 4️⃣ Image hardening & bloat analysis

### Tool: **Dockle**

Checks:
- Root usage
- Capabilities
- Sensitive files
- Best practices

### Run
```bash
dockle nginx:latest
```

### 🔍 Example output
```bash
WARN - CIS-DI-0001: Container runs as root WARN - CIS-DI-0005: No HEALTHCHECK
```

---

### Tool: **Dive**

### Run
```bash
dive nginx:latest
```

### What I look for
- Secrets in layers
- Large unused packages
- `.ssh`, `.env`, API keys baked in