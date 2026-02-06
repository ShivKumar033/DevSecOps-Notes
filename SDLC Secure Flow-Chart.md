flowchart TD

    A[Requirements & Planning
    Skills:
    - Risk Assessment
    - Threat Modeling
    - OWASP Top 10
    Tools:
    - Threat Dragon
    - MS Threat Modeling] --> 

    B[Design
    Skills:
    - Secure Architecture
    - Auth & Encryption
    - Zero Trust
    Tools:
    - Architecture Diagrams
    - Security Checklists]

    B --> C[Development
    Skills:
    - Secure Coding
    - Code Review
    - Secrets Handling
    Tools:
    - SonarQube
    - Semgrep
    - GitGuardian]

    C --> D[Build & CI/CD
    Skills:
    - DevSecOps
    - Pipeline Security
    - Dependency Analysis
    Tools:
    - Snyk
    - OWASP Dependency-Check
    - GitHub Actions]

    D --> E[Testing
    Skills:
    - AppSec Testing
    - API Security
    - Pentesting Basics
    Tools:
    - OWASP ZAP
    - Burp Suite]

    E --> F[Deployment
    Skills:
    - Cloud Security
    - IaC Security
    - Secrets Management
    Tools:
    - Checkov
    - Vault
    - AWS Security Hub]

    F --> G[Operations & Monitoring
    Skills:
    - Incident Response
    - Log Analysis
    - Runtime Security
    Tools:
    - Splunk
    - ELK
    - Falco]

    G --> H[Maintenance & Feedback
    Skills:
    - Patch Management
    - Vulnerability Management
    Tools:
    - Nessus
    - Jira
    - HackerOne]


# Secure SDLC – Stages & Required Skills

## 1. Requirements & Planning (Security Starts Here)

### Security Activities

- Identify security requirements
    
- Define data sensitivity & compliance needs
    
- Perform **threat modeling (high-level)**
    
- Define security acceptance criteria
    

### Required Skills

**Technical / Security**

- Basic application security principles
    
- Risk assessment
    
- CIA triad (Confidentiality, Integrity, Availability)
    
- Compliance knowledge (ISO 27001, GDPR, PCI-DSS)
    

**Soft / Business**

- Stakeholder communication
    
- Translating business needs into security requirements
    
- Documentation
    

📌 **Who:** Security architects, senior developers, AppSec engineers

---

## 2. Design & Architecture

### Security Activities

- Threat modeling (STRIDE, PASTA)
    
- Secure architecture design
    
- Trust boundaries definition
    
- Authentication & authorization design
    
- Encryption strategy (data at rest & in transit)
    

### Required Skills

**Technical**

- Secure design principles
    
    - Least privilege
        
    - Defense in depth
        
    - Zero Trust
        
- Threat modeling tools & techniques
    
- Authentication protocols (OAuth2, OIDC, SAML)
    
- Cryptography basics
    
- API security design
    

📌 **Who:** Security architects, senior engineers

---

## 3. Development / Implementation

### Security Activities

- Secure coding practices
    
- Input validation & output encoding
    
- Secrets management
    
- Code reviews with security focus
    
- Dependency management
    

### Required Skills

**Technical**

- Secure coding (language-specific)
    
- OWASP Top 10
    
- Common vulnerability patterns
    
- Secure use of frameworks
    
- Static code analysis (SAST)
    
- Git, CI/CD security basics
    

**Developer Skills**

- Writing clean, testable code
    
- Understanding secure defaults
    
- Avoiding hardcoded secrets
    

📌 **Who:** Developers, AppSec engineers

---

## 4. Testing & Verification

### Security Activities

- Static testing (SAST)
    
- Dynamic testing (DAST)
    
- Interactive testing (IAST)
    
- Manual penetration testing
    
- Security regression testing
    

### Required Skills

**Technical**

- Vulnerability assessment
    
- Penetration testing
    
- OWASP Testing Guide
    
- Secure test case design
    
- Automation security tools
    

**Analytical**

- False positive validation
    
- Risk severity scoring (CVSS)
    

📌 **Who:** QA, AppSec, penetration testers

---

## 5. Deployment & Release

### Security Activities

- Secure CI/CD pipeline
    
- Environment hardening
    
- Secure configuration management
    
- Secrets rotation
    
- Access control enforcement
    

### Required Skills

**Technical**

- DevSecOps
    
- Infrastructure as Code (Terraform, CloudFormation)
    
- Container security (Docker, Kubernetes)
    
- Cloud security (AWS/Azure/GCP)
    
- Secure configuration benchmarks (CIS)
    

📌 **Who:** DevOps, Cloud Security Engineers

---

## 6. Operations & Maintenance

### Security Activities

- Logging & monitoring
    
- Incident detection & response
    
- Vulnerability patching
    
- Continuous security testing
    
- Bug bounty management
    

### Required Skills

**Technical**

- SIEM & SOC operations
    
- Incident response
    
- Log analysis
    
- Threat intelligence
    
- Patch management
    

**Process**

- Change management
    
- Risk acceptance
    

📌 **Who:** SOC, Security Operations, SRE

---

## 7. Decommissioning / End-of-Life

### Security Activities

- Secure data deletion
    
- Credential revocation
    
- Infrastructure teardown
    
- Compliance documentation
    

### Required Skills

**Technical**

- Data sanitization
    
- Backup verification
    
- Asset inventory management
    

**Compliance**

- Audit readiness
    
- Legal & regulatory understanding
    

📌 **Who:** IT, Security, Compliance teams