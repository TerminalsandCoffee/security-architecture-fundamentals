# Risk Assessment

## Document Control

| Field | Value |
|-------|-------|
| **Assessment ID** | *RA-YYYY-NNN* |
| **Assessment Title** | *Brief title describing what is being assessed* |
| **Prepared By** | *Name, title* |
| **Reviewed By** | *Name, title* |
| **Assessment Date** | *YYYY-MM-DD* |
| **Next Review Date** | *YYYY-MM-DD* |
| **Document Status** | Draft / In Review / Final |

---

## 1. Scope & Context

**Purpose:** *Describe why this assessment is being performed (new system, annual review, incident-driven, regulatory requirement).*

**Scope:** *Define what is included and excluded. Specify systems, environments, data types, and organizational boundaries.*

| Attribute | Details |
|-----------|---------|
| **Business Unit** | *Team or department* |
| **Systems in Scope** | *List systems, services, applications* |
| **Environments** | *Production / Staging / Dev / All* |
| **Data Types** | *PII, financial, health, IP, public* |
| **Out of Scope** | *Explicitly list exclusions* |
| **Assessment Method** | *Qualitative / Quantitative / Hybrid* |

**Business Context:** *Describe the business function these assets support and the impact of disruption.*

---

## 2. Asset Inventory

| Asset ID | Asset Name | Type | Owner | Data Classification | Criticality | Location |
|----------|-----------|------|-------|--------------------:|-------------|----------|
| A-001 | *Asset name* | Application / Server / Database / Network / Data | *Name* | Public / Internal / Confidential / Restricted | Critical / High / Medium / Low | *Cloud region, data center, etc.* |
| A-002 | *Asset name* | *Type* | *Name* | *Classification* | *Criticality* | *Location* |
| A-003 | *Asset name* | *Type* | *Name* | *Classification* | *Criticality* | *Location* |

---

## 3. Threat Identification

| Threat ID | Threat | Threat Source | Likelihood | Description |
|-----------|--------|--------------|------------|-------------|
| T-001 | *Unauthorized access to database* | External attacker | *High / Medium / Low* | *Attacker exploits weak credentials or SQL injection to access sensitive data* |
| T-002 | *Insider data exfiltration* | Malicious insider | *High / Medium / Low* | *Privileged user copies data to personal storage* |
| T-003 | *Ransomware deployment* | External attacker | *High / Medium / Low* | *Attacker encrypts production systems after initial access via phishing* |
| T-004 | *Supply chain compromise* | Third-party vendor | *High / Medium / Low* | *Compromised dependency or vendor introduces malicious code* |
| T-005 | *Service disruption* | External attacker / Natural | *High / Medium / Low* | *DDoS attack or infrastructure failure causes prolonged outage* |

*Add or remove rows as needed. Reference MITRE ATT&CK or STRIDE for systematic threat enumeration.*

---

## 4. Vulnerability Identification

| Vuln ID | Vulnerability | Affected Asset(s) | Current Controls | Control Effectiveness |
|---------|--------------|-------------------|------------------|-----------------------|
| V-001 | *Default credentials on admin interface* | *A-001* | *Password policy in place but not enforced on this system* | Weak / Partial / Strong |
| V-002 | *Unencrypted data at rest* | *A-002* | *Network segmentation limits access* | Weak / Partial / Strong |
| V-003 | *Missing MFA on VPN access* | *A-003* | *Strong password policy, IP allowlist* | Weak / Partial / Strong |
| V-004 | *Unpatched third-party library* | *A-001* | *WAF in place, vulnerability scanning quarterly* | Weak / Partial / Strong |

---

## 5. Risk Calculation Matrix

Use the following 5x5 matrix to determine risk level from likelihood and impact scores.

**Likelihood Scale:**

| Score | Rating | Description |
|-------|--------|-------------|
| 5 | Almost Certain | Expected to occur in most circumstances (>90%) |
| 4 | Likely | Will probably occur in most circumstances (60-90%) |
| 3 | Possible | Might occur at some time (30-60%) |
| 2 | Unlikely | Could occur but not expected (10-30%) |
| 1 | Rare | May occur only in exceptional circumstances (<10%) |

**Impact Scale:**

| Score | Rating | Description |
|-------|--------|-------------|
| 5 | Critical | Existential threat — regulatory action, massive breach, business failure |
| 4 | Major | Significant financial loss, large-scale data exposure, extended outage |
| 3 | Moderate | Material financial loss, limited data exposure, service degradation |
| 2 | Minor | Small financial loss, minimal data involved, brief disruption |
| 1 | Negligible | No meaningful business impact, easily contained |

**Risk Matrix:**

| | Impact 1 (Negligible) | Impact 2 (Minor) | Impact 3 (Moderate) | Impact 4 (Major) | Impact 5 (Critical) |
|---|:---:|:---:|:---:|:---:|:---:|
| **Likelihood 5 (Almost Certain)** | Medium (5) | High (10) | High (15) | Critical (20) | Critical (25) |
| **Likelihood 4 (Likely)** | Low (4) | Medium (8) | High (12) | High (16) | Critical (20) |
| **Likelihood 3 (Possible)** | Low (3) | Medium (6) | Medium (9) | High (12) | High (15) |
| **Likelihood 2 (Unlikely)** | Low (2) | Low (4) | Medium (6) | Medium (8) | High (10) |
| **Likelihood 1 (Rare)** | Low (1) | Low (2) | Low (3) | Low (4) | Medium (5) |

**Risk Levels:** Critical (20-25) | High (10-16) | Medium (5-9) | Low (1-4)

---

## 6. Risk Register

| Risk ID | Description | Threat | Vuln | Likelihood (1-5) | Impact (1-5) | Risk Score | Risk Level | Treatment | Owner | Status | Review Date |
|---------|-------------|--------|------|:-:|:-:|:-:|-----------|-----------|-------|--------|-------------|
| R-001 | *Unauthorized database access via SQL injection* | T-001 | V-004 | *3* | *4* | *12* | High | Mitigate | *Name* | Open | *YYYY-MM-DD* |
| R-002 | *Data exfiltration by insider with broad access* | T-002 | V-001 | *2* | *5* | *10* | High | Mitigate | *Name* | Open | *YYYY-MM-DD* |
| R-003 | *VPN compromise due to missing MFA* | T-001 | V-003 | *3* | *3* | *9* | Medium | Mitigate | *Name* | Open | *YYYY-MM-DD* |
| R-004 | *Unencrypted backups exposed in breach* | T-001 | V-002 | *2* | *4* | *8* | Medium | Mitigate | *Name* | Open | *YYYY-MM-DD* |

---

## 7. Risk Treatment Plan

For each risk in the register, define the treatment approach and specific actions.

### Treatment Options

| Option | When to Use |
|--------|-------------|
| **Mitigate** | Implement controls to reduce likelihood or impact |
| **Accept** | Risk is within tolerance — document justification and monitor |
| **Transfer** | Shift risk to third party via insurance, outsourcing, or contract |
| **Avoid** | Eliminate the risk by removing the activity or asset |

### Treatment Actions

| Risk ID | Treatment | Specific Actions | Resources Required | Target Date | Success Criteria |
|---------|-----------|-----------------|-------------------|-------------|-----------------|
| R-001 | Mitigate | *1. Deploy parameterized queries. 2. Add WAF SQL injection rules. 3. Run DAST scan.* | *Engineering: 3 days. WAF license.* | *YYYY-MM-DD* | *Zero SQL injection findings on rescan* |
| R-002 | Mitigate | *1. Implement RBAC with least privilege. 2. Enable DLP on egress. 3. Review access quarterly.* | *IAM team: 2 days. DLP tool.* | *YYYY-MM-DD* | *No user has access beyond job function* |
| R-003 | Mitigate | *1. Enforce MFA on VPN. 2. Migrate to zero-trust access.* | *IT: 1 week. MFA licenses.* | *YYYY-MM-DD* | *100% MFA adoption on VPN* |
| R-004 | Accept | *Risk accepted: backups are in isolated account with no public access. Compensating control is network isolation.* | *None* | *N/A* | *Reviewed at next assessment* |

---

## 8. Residual Risk Summary

After treatment actions are implemented, re-evaluate each risk.

| Risk ID | Inherent Risk | Treatment Applied | Residual Likelihood | Residual Impact | Residual Risk Score | Residual Level | Acceptable? |
|---------|:---:|-------------------|:---:|:---:|:---:|-------------|:-----------:|
| R-001 | High (12) | *WAF + parameterized queries* | *2* | *4* | *8* | Medium | Yes / No |
| R-002 | High (10) | *RBAC + DLP* | *1* | *5* | *5* | Medium | Yes / No |
| R-003 | Medium (9) | *MFA enforced* | *1* | *3* | *3* | Low | Yes / No |
| R-004 | Medium (8) | *Accepted with compensating control* | *2* | *4* | *8* | Medium | Yes / No |

**Overall Residual Risk Posture:** *Low / Medium / High / Critical*

**Summary:** *Provide a 2-3 sentence summary of the overall risk posture after treatment. Highlight any critical or high residual risks that require executive attention.*

---

## 9. Risk Acceptance Sign-Off

By signing below, the risk owner acknowledges the residual risks documented in this assessment and accepts responsibility for monitoring and reviewing them.

| Role | Name | Accepted Risks | Signature / Approval | Date |
|------|------|---------------|---------------------|------|
| **Risk Owner** | *Name* | *R-004* | | *YYYY-MM-DD* |
| **System Owner** | *Name* | *All residual risks* | | *YYYY-MM-DD* |
| **Security Lead** | *Name* | *Assessment reviewed* | | *YYYY-MM-DD* |
| **CISO / Director** | *Name* | *Overall risk posture* | | *YYYY-MM-DD* |

---

## Appendix: References

- *Link to threat model*
- *Link to architecture diagram*
- *Link to previous risk assessment*
- *Link to compliance requirements*
- *NIST SP 800-30 Rev. 1 — Guide for Conducting Risk Assessments*
- *ISO 27005 — Information Security Risk Management*
