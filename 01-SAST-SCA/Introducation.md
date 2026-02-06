- SAST is a White-box testing, its testing application source code/bytecode/binaries without runing the appication.
- Detects vulnerabilities, ite requries access to the source code.

#### what it Finds
- Sqli Injection
- Cross-site scripting ( XSS )
- Buffer Overflow
- Insecure data Handling 
- Hardcoded secrets(Password, secrets keys, API keys)
- Command Injection
- Weak crypto usage
- Auth / authorization flaws (limited)
- Insecure API usage

### Types / Technique of SAST
1. Manual Code Review (Human-Driven SAST)
2. Pattern-Based Static Analysis (Rule Matching)
3. Data Flow Analysis (Taint Analysis)
4. Control Flow Analysis
5. Semantic / Context-Aware Analysis
6. Secret & Configuration Analysis
7. Dependency / Library Analysis (SCA – Static)

### SAST Tools 

**Open-Source Tools**
1. Semgrep (Pattern + taint analysis, CI/CD friendly)
2. Bandit  ( python SAST )
3. OWASP Dependency-Check

**Commercial / Enterprise Tools**
1. Checkmarx
2. Fortify
3. SonarQube
4. Snyk

## SAST WorkFlow

1. Developer commits code
    
2. CI pipeline triggers SAST
    
3. Tool scans source
    
4. Findings generated
    
5. Security validates
    
6. Dev fixes
    
7. Re-scan
    
8. Deploy

