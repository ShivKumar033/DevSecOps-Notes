# DevSecOps – Short Notes

## What is DevSecOps

DevSecOps = **Dev + Sec + Ops**  
Security is **automated** and integrated into the CI/CD pipeline.

[CI/CD](https://example.com](https://github.com/ShivKumar033/DevSecOps-Notes/tree/main/00-CI-CD)

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
