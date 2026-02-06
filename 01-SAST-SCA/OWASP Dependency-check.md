- **OWASP Dependency-Check** is a **Software Composition Analysis (SCA)** tool that:
- 🔍 **Finds known vulnerabilities in third-party libraries** used by your application.

#### Use Case
- Catch vulnerable libraries before production
- Shift-left Security (DevOps)
- Compliance & Audits

### Scan a Project (CLI)
```bash
dependency-check \
  --project "MyApp" \
  --scan . \
  --format HTML \
  --out reports/
  
  # Fail build on HIGH severity (CVSS>=7)
  dependency-check \
  --scan . \
  --failOnCVSS 7
```

### Jenkinsfile example
```bash
stage('Dependency Check') {
  steps {
    sh '''
      dependency-check \
        --scan . \
        --format HTML \
        --failOnCVSS 7 \
        --out dependency-report
    '''
  }
  post {
    always {
      archiveArtifacts 'dependency-report/*'
    }
  }
}

```

