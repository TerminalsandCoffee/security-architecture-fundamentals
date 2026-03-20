# Security Architecture Fundamentals

Practical security architecture reference — from core fundamentals to cloud security, with interview prep for architect roles.

## Who This Is For

- **Beginners** breaking into security who want to understand how systems are secured at an architectural level
- **Mid-level engineers** preparing for security architect interviews or transitioning into architecture roles
- **Anyone** who needs a quick, opinionated reference on security architecture decisions

## How to Use This Repo

- **Learning path**: Start with [Fundamentals](#fundamentals), then move to [Cloud](#cloud-security), then [Frameworks](#frameworks)
- **Interview prep**: Jump straight to [Interview Prep](#interview-prep) for questions, scenarios, and whiteboard exercises
- **On the job**: Grab a [Template](#templates) for your next security review or threat model

---

## Fundamentals

Core security architecture concepts every practitioner needs to know.

| Topic | Description |
|-------|-------------|
| [Defense in Depth](fundamentals/defense-in-depth.md) | Layered security controls — why one wall isn't enough |
| [Zero Trust](fundamentals/zero-trust.md) | Never trust, always verify — architecture and implementation |
| [Least Privilege](fundamentals/least-privilege.md) | Minimum access, maximum security |
| [Threat Modeling](fundamentals/threat-modeling.md) | Finding what can go wrong before it does |
| [Secure SDLC](fundamentals/secure-sdlc.md) | Building security into the development lifecycle |
| [Identity & Access Management](fundamentals/identity-and-access-management.md) | Authentication, authorization, and identity architecture |
| [Network Security Architecture](fundamentals/network-security-architecture.md) | Segmentation, firewalls, and network design |
| [Data Protection](fundamentals/data-protection.md) | Encryption, classification, and data lifecycle |
| [Logging & Monitoring](fundamentals/logging-and-monitoring.md) | Visibility, detection, and audit trails |
| [Incident Response Architecture](fundamentals/incident-response-architecture.md) | Designing systems that support fast response |
| [API Security](fundamentals/api-security.md) | Securing APIs — OWASP Top 10, gateways, and authentication patterns |
| [Security Automation & Orchestration](fundamentals/security-automation-and-orchestration.md) | SOAR, IaC security, CI/CD pipelines, and detection-as-code |
| [Vendor Risk Management](fundamentals/vendor-risk-management.md) | Third-party risk lifecycle — assess, contract, monitor |
| [Security Policy Development](fundamentals/security-policy-development.md) | Policy hierarchy, governance, and writing enforceable policies |

## Cloud Security

Security architecture in cloud environments — AWS, Azure, and GCP patterns.

| Topic | Description |
|-------|-------------|
| [Shared Responsibility Model](cloud/shared-responsibility-model.md) | Who secures what in cloud environments |
| [Cloud Identity & IAM](cloud/cloud-identity-and-iam.md) | Identity federation, roles, and cloud-native IAM |
| [Network Segmentation in Cloud](cloud/network-segmentation-cloud.md) | VPCs, security groups, and micro-segmentation |
| [Secure Cloud Storage](cloud/secure-cloud-storage.md) | Object storage, encryption, and access policies |
| [Container & Serverless Security](cloud/container-and-serverless-security.md) | Securing modern compute patterns |
| [Cloud Logging & SIEM](cloud/cloud-logging-and-siem.md) | Centralized logging and detection in the cloud |
| [Multi-Cloud Considerations](cloud/multi-cloud-considerations.md) | Architecture decisions across cloud providers |

## Frameworks

Industry frameworks and how they map to real architecture decisions.

| Topic | Description |
|-------|-------------|
| [NIST CSF](frameworks/nist-csf.md) | The Cybersecurity Framework — Identify, Protect, Detect, Respond, Recover |
| [CIS Controls](frameworks/cis-controls.md) | Prioritized security actions that work |
| [MITRE ATT&CK](frameworks/mitre-attack.md) | Adversary tactics and techniques — the defender's playbook |
| [Zero Trust Architecture (NIST 800-207)](frameworks/zero-trust-architecture-nist-800-207.md) | The formal ZTA reference architecture |
| [ISO 27001 / 27002](frameworks/iso-27001-27002.md) | International ISMS standard — certification, controls, and PDCA |


## Templates

Fork these and use them on the job.

| Template | Use Case |
|----------|----------|
| [Threat Model Template](templates/threat-model-template.md) | Structured threat modeling for any system |
| [Security Architecture Review](templates/security-architecture-review.md) | Checklist for reviewing system designs |
| [Risk Assessment Template](templates/risk-assessment-template.md) | Lightweight risk assessment framework |
| [Cloud Security Checklist](templates/cloud-security-checklist.md) | Pre-deployment cloud security validation |

---

## Contributing

Found an error? Have a better way to explain something? PRs welcome.

## License

MIT — use it, fork it, learn from it.
