# Devsecops pipeline on a linux VM 

This repository shows how to run a complete DevSecOps pipeline on a single VM using Docker Compose. 
It is designed for Linux inside VirtualBox.

## Features
- Github -> Jenkins CI trigger on push to 'main'
- SAST : Sonarqube + Semgrep
- Secrets : Gitleaks
- Dependency scanning : OWASP Dependency-Check
- Container scanning + SBOM (Software Bill of Materials) : Trivy (Fail on HIGH/CRITICAL)
- Image signing + SBOM attestation : Cosign 
- "GitOps-ish" CD : Jenkins updates a deploy repo and deploys via Docker Compose
- Post-deploy DAST : OWASP ZAP
- Runtime detection : Falco 

## Documentation 
- docs/01-vm-setup.md
- docs/02-platform-up.md
- docs/03-jenkins-setup.md
- docs/04-github-webhook.md
- docs/05-pipeline.md
- docs/06-deploy-repo.md
- docs/07-falco.md

## Notes
- This repo includes a template deploy repo under 'deploy-repo-template/'.<br>
In real usage, create a seperate GitHub repo (e.g., 'example-deploy') and copy that template in.
- If your Jenkins VM is not publicly reachable, GitHub webhooks won't reach it. <br>
Use one of: <br>(a) Bridge networking
<br> (b) Port forwarding + public IP, 
<br> (c) Tunnel