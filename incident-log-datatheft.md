# Incident Journal

---

## Journal Entry

| Field | Details |
|-------|---------|
| **Date** | `2022-12-28` |
| **Entry #** | `004` |
| **Scenario** | Data theft through forced browsing |

---

### Description

A data breach occurred due to a web application vulnerability that allowed unauthorized access to customer PII and financial data via URL manipulation, also known as forced browsing. Approximately 50,000 records were exposed, resulting in financial and reputational impact.

---

### Tools Used

| Tool | Purpose |
|------|---------|
| `Web Server Logs` | `Identify abnormal access patterns and confirm exploitation` |
| `Manual Log Analysis` | `Trace attacker activity and scope of data exposure` |

---

### The 5 W's

**Who** caused the incident?
> An external attacker exploited a web application vulnerability.

**What** happened?
> The attacker performed a forced browsing attack by modifying URL parameters to access customer purchase confirmation pages, leading to large-scale data exfiltration.

**When** did it occur?
> Initial activity began on December 22, 2022, with confirmed escalation and response on December 28-31, 2022.

**Where** did it happen?
> Within the organization's e-commerce web application and associated web server environment.

**Why** did it happen?
> A lack of proper access controls and input validation allowed unauthorized users to access sensitive data through predictable URL patterns.

---

### Additional Notes

> - The attacker demonstrated proof of access via extortion emails requesting cryptocurrency.
> - High-volume sequential access in logs was a key detection indicator.
> - The root cause highlights a failure in authorization controls, not authentication alone.
> - Remediation included disclosure, customer protection services, and implementation of stricter access controls such as allowlisting and authentication enforcement.
> - Future prevention depends on routine security testing, including vulnerability scans and penetration testing, plus improved application design.

---
