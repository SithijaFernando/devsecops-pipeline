FROM debian:bookworm

# Fail fast and avoid interactive installs
ENV DEBIAN_FRONTEND=noninteractive
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Base system dependencies
RUN apt-get update && apt-get install -y \
    ca-certificates \
    curl \
    git \
    jq \
    python3 \
    python3-pip \
    python3-venv \
    pipx \
    openjdk-17-jre \
    docker.io \
    unzip \
 && rm -rf /var/lib/apt/lists/*

# pipx configuration
ENV PIPX_HOME=/opt/pipx
ENV PIPX_BIN_DIR=/usr/local/bin
ENV PATH="${PIPX_BIN_DIR}:${PATH}"


# Semgrep 
RUN pipx install semgrep


# Gitleaks
RUN curl -fsSL https://github.com/gitleaks/gitleaks/releases/download/v8.30.0/gitleaks_8.30.0_linux_arm64.tar.gz \
    | tar -xz -C /usr/local/bin gitleaks \
 && chmod +x /usr/local/bin/gitleaks

# Trivy
RUN curl -fsSL https://raw.githubusercontent.com/aquasecurity/trivy/main/contrib/install.sh \
    | sh -s -- -b /usr/local/bin


# OWASP Dependency-Check
RUN curl -fsSL https://github.com/jeremylong/DependencyCheck/releases/download/v12.1.0/dependency-check-12.1.0-release.zip \
    -o dc.zip \
 && unzip dc.zip -d /opt \
 && rm dc.zip \
 && ln -s /opt/dependency-check/bin/dependency-check.sh /usr/local/bin/dependency-check

# SonarScanner (CLI)

RUN curl -fsSL https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-8.0.1.6346.zip \
    -o sonar-scanner.zip \
 && unzip sonar-scanner.zip -d /opt \
 && rm sonar-scanner.zip \
 && ln -s /opt/sonar-scanner-linux/bin/sonar-scanner /usr/local/bin/sonar-scanner

# Cosign
RUN curl -fsSL https://github.com/sigstore/cosign/releases/latest/download/cosign-linux-amd64 \
    -o /usr/local/bin/cosign \
 && chmod +x /usr/local/bin/cosign
