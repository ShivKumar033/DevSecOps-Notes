- **SLSA** is a **security framework** that defines _how trustworthy your build pipeline is_ — from source code to production artifact.

It answers one question:
	Can I trust this software was built securely and not tampered with?

- SLSA aims to increase transparency, reduce risk, and protect against potential tampering or compromise of software components.

**SLSA Protection adainst:-**
- Code modification
- Thread against the build platforms
- malware injection during build and release.

## 🔹 SLSA-1 – Build Scripted

- Build process is documented
- No protection from tampering

---
## 🔹 SLSA-2 – Source Controlled

- Code must come from Git    
- Commits are tracked & auditable

---
## 🔹 SLSA-3 – Tamper Resistant

- CI server protected
- Artifacts are signed
- Metadata generated automatically

---
## 🔹 SLSA-4 – Hermetic & Reproducible

- No internet during build    
- Same input = same output
- Maximum supply-chain security
