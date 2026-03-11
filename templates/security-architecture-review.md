# Security Architecture Review

## Document Control

| Field | Value |
|-------|-------|
| **Review ID** | *SAR-YYYY-NNN* |
| **System Name** | *Name of system or service under review* |
| **System Owner** | *Name, title, team* |
| **Review Requested By** | *Name, title* |
| **Reviewer(s)** | *Security architect(s) conducting the review* |
| **Review Date** | *YYYY-MM-DD* |
| **Target Deployment Date** | *YYYY-MM-DD* |
| **Document Status** | Draft / In Review / Final |

---

## 1. System Overview

**Description:** *Provide a 2-3 sentence summary of the system's purpose, key functionality, and users.*

**Architecture Diagram:** *Insert or link architecture diagram here. Include data flows, trust boundaries, and external integrations.*

| Attribute | Details |
|-----------|---------|
| **Environment** | *Production / Staging / Dev* |
| **Hosting** | *AWS / Azure / GCP / On-Prem / Hybrid* |
| **Data Classification** | *Public / Internal / Confidential / Restricted* |
| **User Population** | *Internal employees / External customers / Both* |
| **Estimated User Count** | *Number* |
| **Third-Party Integrations** | *List external services, APIs, SaaS dependencies* |
| **Previous Review** | *Link to prior review or "N/A — initial review"* |

---

## 2. Authentication & Authorization

- [ ] Authentication mechanism identified (*SSO / OIDC / SAML / local credentials / API keys*)
- [ ] Multi-factor authentication enforced for all human users
- [ ] MFA enforced for privileged / administrative access
- [ ] Session timeout configured (*specify duration: _____ minutes*)
- [ ] Session tokens are invalidated on logout
- [ ] Password policy meets organizational standards (length, complexity, rotation)
- [ ] Authorization model defined (*RBAC / ABAC / ACL*)
- [ ] Least privilege enforced — roles documented and reviewed
- [ ] Role definitions avoid overly broad permissions
- [ ] API authentication uses short-lived tokens (not static keys where avoidable)
- [ ] Service-to-service authentication uses mutual TLS or workload identity
- [ ] Broken access control tested (IDOR, privilege escalation, horizontal access)
- [ ] Account lockout / brute force protection in place

**Notes:** *Document any exceptions, compensating controls, or open questions.*

---

## 3. Network Security

- [ ] Network segmentation enforces trust boundaries shown in architecture diagram
- [ ] All external traffic terminates at a load balancer, WAF, or API gateway
- [ ] TLS 1.2+ enforced on all external-facing endpoints
- [ ] Internal service-to-service traffic encrypted (mTLS, service mesh, or VPN)
- [ ] No unnecessary ports or protocols exposed to the internet
- [ ] Ingress rules follow default-deny with explicit allow lists
- [ ] Egress traffic is filtered (no unrestricted outbound access)
- [ ] DNS resolution is controlled (internal DNS, no public resolvers from private subnets)
- [ ] DDoS protection enabled for public-facing endpoints
- [ ] VPN or zero-trust network access required for administrative access
- [ ] Network flow logs are enabled and forwarded to SIEM

**Notes:** *Document any exceptions, compensating controls, or open questions.*

---

## 4. Data Protection

- [ ] Data classification applied to all stored and processed data
- [ ] Encryption at rest enabled for all datastores (*specify: AES-256, KMS, etc.*)
- [ ] Encryption keys are managed through a dedicated KMS (not application code)
- [ ] Key rotation policy defined and automated (*rotation period: _____*)
- [ ] PII, PHI, or financial data identified and subject to additional controls
- [ ] Data masking or tokenization used where full data access is unnecessary
- [ ] Backups are encrypted and stored in a separate region / account
- [ ] Backup restoration tested within the last *_____ days*
- [ ] Data retention policy defined (*retention period: _____*)
- [ ] Data deletion / purge process exists and is tested
- [ ] No sensitive data in logs, error messages, or URLs

**Notes:** *Document any exceptions, compensating controls, or open questions.*

---

## 5. Logging & Monitoring

- [ ] Authentication events logged (success, failure, MFA challenges)
- [ ] Authorization failures logged
- [ ] Administrative actions logged (configuration changes, user management)
- [ ] Data access events logged for sensitive resources
- [ ] Logs include: timestamp, source IP, user identity, action, resource, outcome
- [ ] Logs are forwarded to centralized SIEM (*specify platform: _____*)
- [ ] Log integrity protected (immutable storage, separate account)
- [ ] Log retention meets compliance requirements (*retention period: _____*)
- [ ] Alerting rules defined for critical security events
- [ ] On-call rotation or escalation path documented for security alerts
- [ ] No sensitive data (passwords, tokens, PII) written to logs

**Notes:** *Document any exceptions, compensating controls, or open questions.*

---

## 6. Infrastructure Security

- [ ] OS and middleware patching cadence defined (*frequency: _____*)
- [ ] Automated vulnerability scanning in place (infrastructure and dependencies)
- [ ] Container images scanned for vulnerabilities before deployment
- [ ] Base images sourced from trusted registries and regularly updated
- [ ] CIS benchmarks or equivalent hardening standards applied
- [ ] Secrets stored in a secrets manager (*specify: Vault, AWS Secrets Manager, etc.*)
- [ ] No secrets in source code, environment variables, or CI/CD logs
- [ ] Infrastructure defined as code (Terraform, CloudFormation, Pulumi)
- [ ] IaC scanned for misconfigurations (tfsec, Checkov, KICS)
- [ ] CI/CD pipeline has security gates (SAST, SCA, secret scanning)
- [ ] Deployment pipeline uses immutable artifacts (no runtime modifications)
- [ ] SSH and RDP access disabled or restricted to break-glass scenarios

**Notes:** *Document any exceptions, compensating controls, or open questions.*

---

## 7. Cloud-Specific Review

- [ ] IAM policies follow least privilege (no `*:*` or overly broad wildcards)
- [ ] No resources are unintentionally publicly accessible (S3, storage blobs, databases)
- [ ] Resource policies (bucket policies, KMS policies) reviewed for cross-account exposure
- [ ] Cloud-native security services enabled:
  - [ ] AWS: GuardDuty, Security Hub, Config | Azure: Defender for Cloud, Sentinel | GCP: SCC, Chronicle
- [ ] Service control policies or organizational policies restrict dangerous actions
- [ ] Cloud audit trail enabled (CloudTrail / Activity Log / Audit Logs)
- [ ] Unused resources, roles, and permissions identified and removed
- [ ] Cross-account or cross-tenant access is explicitly justified and documented
- [ ] Managed services preferred over self-managed where security posture is equivalent or better

**Notes:** *Document any exceptions, compensating controls, or open questions.*

---

## 8. Compliance Requirements

| Regulation / Standard | Applicable? | Relevant Controls | Notes |
|----------------------|-------------|-------------------|-------|
| *SOC 2* | Yes / No | *List control IDs* | *Notes* |
| *PCI DSS* | Yes / No | *List requirements* | *Notes* |
| *HIPAA* | Yes / No | *List safeguards* | *Notes* |
| *GDPR* | Yes / No | *List articles* | *Notes* |
| *FedRAMP* | Yes / No | *List control families* | *Notes* |
| *Internal Policy* | Yes / No | *List policy sections* | *Notes* |

---

## 9. Risk Summary

| # | Finding | Severity | Recommendation | Owner | Due Date | Status |
|---|---------|----------|----------------|-------|----------|--------|
| 1 | *Description of finding* | Critical / High / Medium / Low | *Specific remediation action* | *Name* | *YYYY-MM-DD* | Open |
| 2 | *Description of finding* | Critical / High / Medium / Low | *Specific remediation action* | *Name* | *YYYY-MM-DD* | Open |
| 3 | *Description of finding* | Critical / High / Medium / Low | *Specific remediation action* | *Name* | *YYYY-MM-DD* | Open |

---

## 10. Verdict & Recommendation

**Overall Assessment:** *Approved / Conditionally Approved / Not Approved*

**Conditions (if conditionally approved):**
1. *Must-fix item before deployment — describe specific requirement and deadline*
2. *Must-fix item before deployment — describe specific requirement and deadline*

**Accepted Risks:**
1. *Risk accepted with justification — describe the risk and why it is acceptable*

---

## 11. Sign-Off

| Role | Name | Signature / Approval | Date |
|------|------|---------------------|------|
| **Security Reviewer** | *Name* | | *YYYY-MM-DD* |
| **System Owner** | *Name* | | *YYYY-MM-DD* |
| **Engineering Lead** | *Name* | | *YYYY-MM-DD* |
| **CISO / Security Manager** | *Name* | | *YYYY-MM-DD* |

**Next Review Date:** *YYYY-MM-DD (recommended: 12 months or upon significant architecture change)*
