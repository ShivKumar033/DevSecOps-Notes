[[https://owasp.org/www-project-secure-coding-practices-quick-reference-guide/stable-en/02-checklist/05-checklist#input-validation]]
## 1. Application Recon & Structure

- ☐ Identify language, framework, version
- ☐ Locate routes / controllers / endpoints
- ☐ Identify auth middleware
- ☐ Identify user roles
- ☐ Identify external integrations
- ☐ Map trust boundaries    

---

## 2. Authentication

- ☐ Passwords hashed securely (bcrypt/argon2)
- ☐ No plaintext passwords
- ☐ No weak hashing (MD5/SHA1)
- ☐ Rate limiting on login
- ☐ Account lockout / CAPTCHA
- ☐ No username/email enumeration
- ☐ MFA implemented (if required)    

---

## 3. Session & Token Management

- ☐ Secure session IDs
- ☐ Session invalidation on logout
- ☐ No session fixation
- ☐ JWT:
    - ☐ Strong secret / key
    - ☐ `alg=none` not allowed
    - ☐ Expiration enforced
    - ☐ Audience & issuer validated        

---

## 4. Authorization / Access Control

- ☐ Role checks on every sensitive action
- ☐ Object ownership enforced
- ☐ No IDOR vulnerabilitie
- ☐ No privilege escalation
- ☐ Backend does NOT trust frontend roles
- ☐ Admin-only routes protected    

---

## 5. Injection Vulnerabilities

- ☐ SQL Injection
- ☐ NoSQL Injection
- ☐ OS Command Injection
- ☐ LDAP Injection
- ☐ XPath Injection
- ☐ Server-Side Template Injection (SSTI)
- ☐ Unsafe deserialization    

---

## 6. Cross-Site Scripting (XSS)

- ☐ Reflected XSS
- ☐ Stored XSS
- ☐ DOM-based XSS
- ☐ Output encoding applied
- ☐ Dangerous sinks avoided (`eval`, `innerHTML`)
- ☐ Content Security Policy (CSP)    

---

## 7. File Handling

- ☐ File upload validation
- ☐ MIME type not trusted alone
- ☐ Executable uploads blocked
- ☐ Upload directory not web-accessible
- ☐ Path traversal prevented (`../`)
- ☐ LFI / RFI protections
- ☐ Zip Slip protection    

---

## 8. SSRF & External Requests

- ☐ User input not used directly in requests
- ☐ URL allowlist enforced
- ☐ Protocol restrictions (http/https only)
- ☐ Internal IPs blocked
- ☐ Cloud metadata protected
- ☐ DNS rebinding mitigations    

---

## 9. Secrets & Sensitive Data

- ☐ No hardcoded secrets
- ☐ `.env` files not committed
- ☐ API keys secured
- ☐ Encryption keys protected
- ☐ Debug output disabled in prod
- ☐ Stack traces not exposed    

---

## 10. Security Configuration

- ☐ Debug mode OFF in production
- ☐ Proper error handling
- ☐ Secure CORS configuration
- ☐ Security headers present:
    - ☐ CSP
    - ☐ HSTS
    - ☐ X-Frame-Options
    - ☐ X-Content-Type-Options        

---

## 11. Business Logic

- ☐ Workflow enforcement
- ☐ Price/quantity tampering prevented
- ☐ State validation implemented
- ☐ Replay attacks prevented
- ☐ Race conditions handled
- ☐ Client-side validation not trusted    

---

## 🔌 12. API Security

- ☐ Authentication required
- ☐ Authorization enforced
- ☐ Mass assignment prevented
- ☐ Schema validation enabled
- ☐ Rate limiting enabled
- ☐ Proper API versioning    

---

## 13. Logging & Monitoring

- ☐ No sensitive data in logs
- ☐ Security events logged
- ☐ Log injection prevented
- ☐ Alerts for auth failures
- ☐ Tamper-resistant logs    

---

## 14. Dependencies & Supply Chain

- ☐ Dependencies up to date
- ☐ Known vulnerable libraries removed
- ☐ No untrusted packages
- ☐ Lockfiles used
- ☐ Build pipeline secured    

---

## 15. Final Review

- ☐ All user input validated
- ☐ All sensitive actions protected
- ☐ Attack paths mentally exploited
- ☐ Mapped to OWASP Top 10
- ☐ PoC feasible for findings