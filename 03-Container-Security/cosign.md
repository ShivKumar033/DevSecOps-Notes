**cosign** is a tool from the **Sigstore** project used to **sign, verify, and attest container images** (OCI images).  
It helps ensure:

- Image **integrity** (was it modified?)
- **Provenance** (who built it?)
- **Supply-chain security** (SLSA-style workflows)

Signatures are stored **alongside the image in the registry**, not inside the image.

### Basic image signing (keyless – recommended)
```bash
cosign sign ghcr.io/myorg/myimage:1.0.0
```

### Verify a signed image (keyless)
```bash
cosign verify \
  --certificate-identity user@company.com \
  --certificate-oidc-issuer https://accounts.google.com \
  ghcr.io/myorg/myimage:1.0.0
```

### Key-based signing (traditional)
```bash
cosign generate-key-pair

#### SIGN ###########
cosign sign --key cosign.key ghcr.io/myorg/myimage:1.0.0

######### VERIFY ##########
cosign verify --key cosign.pub ghcr.io/myorg/myimage:1.0.0
```

