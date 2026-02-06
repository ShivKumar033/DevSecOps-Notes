- An SBOM is a detailed list of everything inside a piece of software, used to manage risk, security, and transparency.
The **SBOM** would list something like:
```bash
Banking App v1.2
- Java 17
- Spring Boot 3.1
- Log4j 2.17
- Jackson 2.15
- PostgreSQL JDBC 42.6
```

# 📦 Types of SBOM

| Type              | When It Is Created  | Use Case                                                     |
| ----------------- | ------------------- | ------------------------------------------------------------ |
| **Design SBOM**   | Before coding       | Plan secure dependencies and  choose safe libraries          |
| **Build SBOM**    | During CI build     | Catch vulnerable libs early and break pipeline on risky CVEs |
| **Source SBOM**   | From source code    | Find risky packages                                          |
| **Binary SBOM**   | From compiled files | Detect hidden components and and detect tampering            |
| **Runtime SBOM**  | While app running   | Monitor real attack surface and detect memory-only malware   |
| **Deployed SBOM** | After release       | Incident response & patching, emergency CVE response         |
### Common SBOM Formate

### 1. **SPDX** (Software Package data Exchange)
- Maintain by linux foundation
- Older and more formal
- Focus on Licenses and Compliance
- Used in Heavily in enterprise and legal audit

Best Suitable for:
- Licenses Compliance 
- Legal review
- Regulatory environment
### 2. **CycloneDX**
- Created by OWASP 
- Designed for application security
- Lightweight & Mordern

Best Suitable for:
- Vulnerability Management
- CI/CD pipelines
- Cloud-Native applicaton