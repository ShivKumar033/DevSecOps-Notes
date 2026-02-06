## Quick hardening checklist ✅

	-  Minimal base image
	-  Multi-stage build
	-  Non-root user
	-  No shell/package manager
	-  Read-only filesystem
	-  Drop capabilities
	-  Seccomp/AppArmor enabled
	-  Vulnerability scanning
	-  Image signing (cosign)
	-  SBOM attached

#### 1. Never Run as root user
```bash
docker run -u 1000 --rm -it image bin/bash
```

#### 2. No user `--privileged` flag
```bash
# NEVER USE --privileged flag      X
```

#### 3. Prevents privilege escalation via SUID binaries.
```bash
--security-opt no-new-privileges
```

#### 4. Drop all Linux capabilities, add only required ones
```bash
docker run --cap-drop=ALL --cap-add=NET_BIND_SERVICE --rm -it image bin/bash

### BAD CAP ####
SYS_ADMIN
SYS_PTRACE
DAC_READ_SEARCH
NET_ADMIN
```

#### 5. Make a Immutable Container FS
```bash
--read-only
```

#### 6. Writable tmpfs only where needed
```bash
--tmpfs /tmp:rw,noexec,nosuid
```

#### 7. CPU / memory Resource limits enforced
```bash
--memory 512m --cpus 1

# Memory limit with swap
--memory="512m" --memory-swap="512m"

# PID Limitation
--pids-limit=100
```

#### 8. Writable cgroups = breakout risk
```bash
# inside container 
ls -ld /sys/fs/cgroup    drwxrwxrwx    # BAD Permission.

# Enforce cgroup namespace
--cgroupns=private
```

#### final example of docker 
```bash
docker run -d \
  --read-only \
  --cap-drop=ALL \
  --security-opt no-new-privileges \
  --pids-limit=100 \
  --memory=512m \
  --cpus=1 \
  --user 1001 \
  myimage
  
# Gold-Standard Secure Run Command
  docker run -d \
  --read-only \
  --cap-drop=ALL \
  --security-opt no-new-privileges \
  --security-opt seccomp=custom.json \
  --pids-limit=100 \
  --memory=512m \
  --cpus=1 \
  --cgroupns=private \
  --user 1001 \
  --tmpfs /tmp:rw,noexec,nosuid \
  myimage@sha256:<digest>
```