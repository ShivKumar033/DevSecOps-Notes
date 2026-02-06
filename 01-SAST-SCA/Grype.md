- Its scan software artifacts to find knows vulnerability.
- Its scan container images, docker images, file system, SBOMs, or packages.

### Scan target 
```bash
grype nginx:latest
grype dir:/path/to/app
grype archive:/path/image.tar
grype sbom:sbom.json
```

### Output Formate
```bash
grype nginx:latest -o table
grype nginx:latest -o json
grype nginx:latest -o cyclonedx
```

### Severity & Filtering
```bash
# Fail only on High or Critial vulnerbaility
grype nginx:latest --fail-on high

# To show onlly high/medium vulernability
grype nginx:latest --file grype.yaml

# file grype.gaml
ignore:
  - severity: low
  - severity: critical
```

### Full build-history scan 
```bash
grype myimage:latest --scope all-layers
grype myimage:latest -o json -q --fail-on medium

```