# Cloud Security Pre-Deployment Checklist

## Document Control

| Field | Value |
|-------|-------|
| **Project / Service** | *Name of the workload being deployed* |
| **Cloud Provider(s)** | *AWS / Azure / GCP / Multi-Cloud* |
| **Account / Subscription** | *Account ID, subscription name, or project ID* |
| **Environment** | *Production / Staging / Dev* |
| **Completed By** | *Name, title* |
| **Reviewed By** | *Name, title* |
| **Date** | *YYYY-MM-DD* |

**Instructions:** Complete each section before promoting to production. Mark items as checked when validated. Add notes for any exceptions or compensating controls. Items marked N/A must include justification.

---

## 1. Identity & Access Management

### Root / Super-Admin Account
- [ ] Root account (AWS) / Global Admin (Azure) / Super Admin (GCP) has MFA enabled
- [ ] Root account is not used for daily operations
- [ ] Root account credentials are stored in a secure, break-glass process
- [ ] Root account email uses a distribution list, not an individual mailbox

### User & Role Management
- [ ] Federated identity configured (SSO via SAML/OIDC to corporate IdP)
- [ ] No long-lived IAM user credentials for human access
- [ ] MFA enforced for all human users (hardware key for privileged access)
- [ ] Roles follow least privilege — no `*` actions or `*` resources without justification
- [ ] Unused roles and users removed or disabled
- [ ] Permissions reviewed within the last *_____ days*
- [ ] Cross-account / cross-project access explicitly documented and justified

### Service Accounts & Workload Identity
- [ ] Service accounts use workload identity / instance profiles / managed identity (not static keys)
- [ ] Service account keys rotated automatically (if static keys are unavoidable)
- [ ] Each service has its own dedicated identity (no shared service accounts)
- [ ] Service account permissions scoped to specific resources

| Platform | Workload Identity Service | Key Service |
|----------|--------------------------|-------------|
| AWS | IAM Roles for EC2/ECS/Lambda | Secrets Manager |
| Azure | Managed Identity | Key Vault |
| GCP | Workload Identity, Service Account | Secret Manager |

**Notes:** *Document any exceptions or open items.*

---

## 2. Network Security

### VPC / VNet Design
- [ ] Dedicated VPC/VNet for this workload (not shared default VPC)
- [ ] Subnets segmented by tier (public, private, data)
- [ ] Private subnets have no direct internet gateway route
- [ ] NAT gateway or equivalent for outbound-only internet access from private subnets

### Firewall & Security Groups
- [ ] Security groups / NSGs follow default-deny inbound
- [ ] No security group rules allow `0.0.0.0/0` inbound on management ports (22, 3389)
- [ ] Security group rules reference specific CIDR blocks or security group IDs
- [ ] Unused security groups identified and removed

### Public Exposure
- [ ] All public-facing endpoints sit behind a load balancer, CDN, or API gateway
- [ ] WAF enabled on public-facing endpoints
- [ ] No databases, caches, or internal services directly exposed to the internet
- [ ] Public IP addresses are intentional and documented

### Egress & DNS
- [ ] Outbound traffic is filtered (egress security groups, firewall rules, or proxy)
- [ ] DNS resolution uses private hosted zones for internal services
- [ ] No public DNS records for internal-only resources
- [ ] DNS logging enabled

| Platform | VPC Flow Logs | WAF Service | DNS Security |
|----------|--------------|-------------|-------------|
| AWS | VPC Flow Logs | AWS WAF | Route 53 Resolver Logs |
| Azure | NSG Flow Logs | Azure Front Door / App Gateway WAF | Azure DNS Analytics |
| GCP | VPC Flow Logs | Cloud Armor | Cloud DNS Logging |

**Notes:** *Document any exceptions or open items.*

---

## 3. Data Protection

### Encryption at Rest
- [ ] All storage services encrypted at rest (block storage, object storage, databases)
- [ ] Customer-managed keys (CMK) used for sensitive data (not just provider-managed defaults)
- [ ] Key rotation enabled (*rotation period: _____*)
- [ ] Key access policies restrict decryption to authorized roles only

### Encryption in Transit
- [ ] TLS 1.2+ enforced on all endpoints (no TLS 1.0/1.1, no plaintext HTTP)
- [ ] Internal service-to-service traffic encrypted (mTLS, service mesh, or VPN)
- [ ] Database connections use TLS (verify `require_ssl` or equivalent is set)
- [ ] Certificate management automated (ACM, Let's Encrypt, managed certs)

### Data Handling
- [ ] Data classification applied to storage resources (tags/labels)
- [ ] PII, PHI, or financial data identified with appropriate access controls
- [ ] Object storage buckets / blobs have public access explicitly blocked at the account or bucket level
- [ ] Versioning enabled on critical object storage buckets
- [ ] Backup strategy defined and tested (*RPO: _____, RTO: _____*)
- [ ] Backups encrypted and stored in a separate region or account
- [ ] Data retention and deletion policies defined and automated

| Platform | KMS | Certificate Management | Storage Access Control |
|----------|-----|----------------------|----------------------|
| AWS | KMS | ACM | S3 Block Public Access |
| Azure | Key Vault | App Service Certs | Storage Account firewall |
| GCP | Cloud KMS | Certificate Manager | Uniform bucket-level access |

**Notes:** *Document any exceptions or open items.*

---

## 4. Compute Security

### VM / Instance Security
- [ ] Base images sourced from trusted, approved sources (golden AMIs, hardened images)
- [ ] CIS benchmark or organizational hardening standard applied
- [ ] OS-level patching automated (*patch window: _____*)
- [ ] No SSH keys baked into images — use instance metadata or session manager for access
- [ ] Instance metadata service v2 (IMDSv2) enforced (AWS) or equivalent protections

### Container Security
- [ ] Container images scanned for vulnerabilities before deployment
- [ ] Images pulled from private registry only (no direct Docker Hub pulls in production)
- [ ] Containers run as non-root user
- [ ] Read-only root filesystem where possible
- [ ] Resource limits (CPU, memory) set to prevent noisy-neighbor or DoS
- [ ] No privileged containers unless explicitly justified
- [ ] Container orchestrator (EKS/AKS/GKE) runs latest supported version

### Serverless / FaaS
- [ ] Function IAM roles scoped to minimum required permissions
- [ ] Function timeout and memory limits configured
- [ ] No secrets in environment variables — use secrets manager references
- [ ] Function code dependencies scanned for vulnerabilities
- [ ] Concurrency limits set to prevent runaway invocations

**Notes:** *Document any exceptions or open items.*

---

## 5. Logging & Monitoring

### Audit Trails
- [ ] Cloud provider audit logging enabled and immutable:
  - [ ] AWS: CloudTrail (all regions, management + data events for sensitive resources)
  - [ ] Azure: Activity Log + Diagnostic Settings forwarded to Log Analytics
  - [ ] GCP: Admin Activity + Data Access audit logs enabled
- [ ] Audit logs shipped to a separate, restricted account/project for tamper resistance
- [ ] Log retention meets compliance requirements (*retention period: _____*)

### Network & Application Logs
- [ ] VPC/VNet flow logs enabled for all subnets
- [ ] Load balancer access logs enabled
- [ ] Application logs include: timestamp, request ID, user identity, action, outcome
- [ ] No secrets, tokens, or PII written to logs

### SIEM & Alerting
- [ ] Logs forwarded to centralized SIEM (*platform: _____*)
- [ ] Alert rules defined for: unauthorized API calls, root/admin usage, security group changes, public exposure changes
- [ ] Alerting targets configured (PagerDuty, Slack, email — *specify: _____*)
- [ ] Alert escalation path documented and tested
- [ ] Dashboard created for security-relevant metrics

| Platform | Audit Service | SIEM Integration | Threat Detection |
|----------|--------------|-----------------|-----------------|
| AWS | CloudTrail | Security Hub, S3 export | GuardDuty |
| Azure | Activity Log | Sentinel | Defender for Cloud |
| GCP | Audit Logs | Chronicle, SCC | Security Command Center |

**Notes:** *Document any exceptions or open items.*

---

## 6. Incident Response Readiness

- [ ] IR plan exists and covers this workload / cloud account
- [ ] IR team has access to cloud environment (break-glass roles provisioned)
- [ ] Forensic capability: ability to snapshot instances, capture memory, preserve logs
- [ ] Isolation playbook: can quarantine compromised resources without destroying evidence
- [ ] Communication plan: internal escalation path + external notification (legal, customers, regulators)
- [ ] IR tabletop exercise conducted within the last *_____ months*
- [ ] Automated response actions configured where appropriate (e.g., auto-revoke leaked keys)
- [ ] Contact list for cloud provider support (enterprise support, abuse team)

**Notes:** *Document any exceptions or open items.*

---

## 7. Compliance & Governance

### Organizational Policies
- [ ] Service Control Policies (AWS) / Azure Policy / Organization Policies (GCP) enforce guardrails
- [ ] Denied actions include: disabling logging, creating public resources, deploying to unapproved regions
- [ ] Approved cloud regions defined and enforced (*regions: _____*)

### Resource Management
- [ ] Tagging / labeling standard applied (owner, environment, cost center, data classification)
- [ ] Cost alerts and budgets configured
- [ ] Unused resources identified and scheduled for removal
- [ ] Infrastructure defined as code — no manual console changes in production

### Regulatory Requirements
- [ ] Applicable regulations identified (*list: _____*)
- [ ] Compliance scanning enabled (AWS Config Rules / Azure Policy Compliance / GCP SCC)
- [ ] Evidence collection automated for audit purposes
- [ ] Data residency requirements mapped to cloud regions

**Notes:** *Document any exceptions or open items.*

---

## Summary & Risk Rating

### Checklist Completion

| Domain | Total Items | Completed | Non-Compliant | N/A | Compliance % |
|--------|:-----------:|:---------:|:-------------:|:---:|:------------:|
| Identity & Access Management | | | | | *___%* |
| Network Security | | | | | *___%* |
| Data Protection | | | | | *___%* |
| Compute Security | | | | | *___%* |
| Logging & Monitoring | | | | | *___%* |
| Incident Response | | | | | *___%* |
| Compliance & Governance | | | | | *___%* |
| **Total** | | | | | *___%* |

### Overall Risk Rating

| Rating | Criteria |
|--------|----------|
| **Low** | >90% compliance, no critical or high findings |
| **Medium** | 75-90% compliance, or high findings with mitigation plan |
| **High** | 50-75% compliance, or critical findings present |
| **Critical** | <50% compliance, or unmitigated critical findings — do not deploy |

**This Workload's Rating:** *Low / Medium / High / Critical*

**Blocking Issues (must resolve before deployment):**
1. *Describe blocking issue and required remediation*
2. *Describe blocking issue and required remediation*

**Non-Blocking Issues (track for remediation post-deployment):**
1. *Describe issue, owner, and target date*
2. *Describe issue, owner, and target date*

---

## Sign-Off

| Role | Name | Approval | Date |
|------|------|----------|------|
| **Security Engineer** | *Name* | | *YYYY-MM-DD* |
| **Cloud Engineer / Architect** | *Name* | | *YYYY-MM-DD* |
| **Engineering Manager** | *Name* | | *YYYY-MM-DD* |
| **CISO / Security Lead** | *Name* | | *YYYY-MM-DD* |
