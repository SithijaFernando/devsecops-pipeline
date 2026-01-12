FROM debian:bookworm

RUN apt update && apt install -y \ 
    curl git jq python3 python3-pip python3-venv pipx openjdk-17-jre docker.io unzip ca-certificates \
 && rm -rf /var/lib/apt/lists/*

#Semgrep
ENV PIPX_BIN_DIR=/usr/local/bin
ENV PIPX_HOME=/opt/pipx

RUN pipx install semgrep

#Gitleaks
RUN curl -sL https://github.com/gitleaks/gitleaks/releases/latest/download/gitleaks-linux-amd64.tar.gz \
    | tar xz -C /usr/local/bin gitleaks 

#Trivy
RUN curl -sfL https://raw.githubusercontent.com/aquasecurity/trivy/main/contrib/install.sh \
    | sh -s -- -b /usr/local/bin 

#Dependency-Check
RUN curl -sL https://github.com/jeremylong/DependencyCheck/releases/latest/download/dependency-check-8.15.1-release.zip \
    -o dc.zip && unzip dc.zip -d /opt/ && rm dc.zip \
    && ln -s /opt/dependency-check/bin/dependency-check.sh /usr/local/bin/dependency-check

#SonarScanner
RUN curl -sL https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-4.7.0.2747-linux.zip \
    -o sonar-scanner.zip && unzip sonar-scanner.zip -d /opt/ && rm sonar-scanner.zip \
    && ln -s /opt/sonar-scanner-4.7.0.2747-linux/bin/sonar-scanner /usr/local/bin/sonar-scanner

# Cosign
RUN curl -sL https://github.com/sigstore/cosign/releases/latest/download/cosign-linux-amd64 \
    -o /usr/local/bin/cosign && chmod +x /usr/local/bin/cosign
