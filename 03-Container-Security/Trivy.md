- **Trivy** is an open-source, all-in-one security scanner developed by Aqua Security that detects vulnerabilities, misconfigurations, secrets, and software licenses in container images, filesystems, Git repositories, and cloud infrastructure.

### Core Components
```bash
1. Scanner Engine      - Orchestrates scanning process
2. Vulnerability DB    - Built-in vulnerability database
3. Policy Engine       - Checks against security policies
4. Report Generator    - Multiple output formats
```

### **1. Container Image Scanning**
```bash
# Scan a Docker image
trivy image nginx:latest

# Scan with specific severity
trivy image --severity HIGH,CRITICAL alpine:latest
trivy image --severity CRITICAL --exit-code 1 nginx:latest

# Scan and save report
trivy image -f json -o report.json ubuntu:20.04

# Using Docker config
trivy image --dockerfile ./Dockerfile private.registry.com/app:latest

# Include all vulnerability types
trivy image --vuln-type os,library nginx:latest

trivy image --scanners vuln --vuln-type os nginx:latest
```

### **2. Filesystem Scanning**
```bash
# Scan local directory
trivy fs /path/to/project

# Exclude dev dependencies
trivy fs --skip-files go.sum /app

# Ignore files
trivy fs --ignorefile .trivyignore .
```
### **4. Repository Scanning**
```bash
# Scan GitHub repository
trivy repo https://github.com/owner/repo

# Scan with git branch
trivy repo --branch main https://github.com/owner/repo
```

### 5. Specific Scanning like (secret, licenses)
```bash
# Scan Vulns,secret,license and config scan 
trivy fs --scanners vuln,secret,license,config .

# If found the secret its fail scan 
trivy fs --exit-code 1 --scanners secret .
```

### 6. Output Formate
```bash
trivy image -f json -o result.json nginx:latest
trivy image -f table nginx:latest
trivy image -f sarif -o trivy.sarif nginx:latest
```

### 7. Secrets Scanning
```bash
trivy fs --scanners secret .

# Disable secrets scan
trivy image --scanners vuln nginx:latest

# Combine Scan 
trivy image --scanners vuln,secret,config,license myimage:latest
```

### 8. Infrastructure & Misconfigure Scanning 
```bash
# Scan dockerfiles
trivy config Dockerfile

# kubernetes YAML 
trivy config k8s/

# Terraform 
trivy config terraform/

# Scan Kubernetes cluster
trivy k8s --report summary cluster

# Scan Terraform files
trivy config /path/to/terraform

# Scan AWS account
trivy aws --region us-east-1
```

----
---

## TRIVY SERVER

- Is a **centralized vulnerability scanning service** for container images and other artifacts.
- - **Runs continuously**
- **Maintains updated vulnerability databases**
- **Processes scan requests from clients** 
- **Caches results for faster responses**

### Start Trivy Server
```bash
trivy server
# start the trivy server with default port -> localhost:4954

# specific custom PORT
trivy server --listen localhost:8080

# Check if server is running or not
curl -s 0.0.0.0:8080/healthz
```

### Scan using Trivy Client
```bash
trivy fs . --server http://localhost:4954
trivy image --server http://localhost:4954 alpine:3.10
```

### Authentication implement
```bash
# start a server with authentication
trivy server --listen localhost:8080 --token dummy

# Peform Scan using token
trivy image --server http://localhost:8080 --token dummy alpine:3.10
```