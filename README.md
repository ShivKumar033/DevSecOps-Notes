# DevSecOps – Short Notes

## What is DevSecOps

DevSecOps = **Dev + Sec + Ops**  
Security is **automated** and integrated into the CI/CD pipeline.

[00-CI/CD](/main/00-CI-CD)
[01-SAST-SCA](/main/01-SAST-SCA)
[03-Container-Security](/main/03-Container-Security)
[04-kubernetes-security](/main/04-kubernetes-security)
[05-iac-security](/main/05-iac-security)
[06-cloud-security](/main/06-cloud-security)
[07-Secret-management-tools](/main/07-Secret-management-tools)
[08-Source%20Code%20Review](/main/08-Source%20Code%20Review)
[Project-List](/main/Project)
[Supply%20Chain%20Security](/main/Supply%20Chain%20Security)

---
## Principles

- Shift Left
- Automate security
- Least privilege
- IaC everywhere
- Continuous monitoring

---
## Lifecycle

```php
Code → Build → Test → Deploy → Monitor  SAST   SCA    DAST
```

---
## Skills

- Linux + Networking
- Git + CI/CD
- Cloud IAM
- Docker & Kubernetes
- OWASP Top 10
- IaC (Terraform)
- Logging & IR

---
## Tools (Must-Know)

**CI/CD:** GitHub Actions, GitLab CI, Jenkins  
**SAST:** Semgrep, SonarQube, Fortify, CodeQL, FindSecBugs, Bandit (Python)
**DAST:** OWASP ZAP, Burp  Suite
**SCA:** Trivy, Snyk, OWASP Dependency-Check, Syft, Grype, Black Duck, GitHub Dependabot
**Container:** Trivy, Falco  
**IaC:** tfsec, Checkov  
**Secrets:** Hashicorp Vault, Cloud Secrets  
**Monitor:** Prometheus, Grafana, ELK

---
## Minimal Pipeline

```php
Git → SAST → SCA → Build → Scan → Deploy → Alert
```
