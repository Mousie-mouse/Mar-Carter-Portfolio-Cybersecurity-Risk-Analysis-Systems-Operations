# Incident Journal

---

## Journal Entry

| Field | Details |
|-------|---------|
| **Date** | `2026-05-02` |
| **Entry #** | `002` |
| **Scenario** | Malicious password-protected spreadsheet and file hash investigation |

---

### Description

An alert was generated when an employee opened a password-protected spreadsheet and entered a password provided in a phishing email. When the employee opened the file, a malicious payload executed on the employee's computer. The incident triggered the IDS, which alerted the SOC.

---

### Tools Used

| Tool | Purpose |
|------|---------|
| `VirusTotal` | Check the SHA256 file hash `54e6ea47eb...` |

![VT Behavior](./assets/vt-behavior.gif)

---

### The 5 W's

**Who** caused the incident?
> An external threat actor delivered a malicious payload via a phishing email; the internal employee unknowingly triggered the execution.

**What** happened?
> A password-protected malicious spreadsheet attachment was delivered via email. After the employee opened it using the provided password, a hidden payload executed, resulting in the creation of multiple unauthorized executable files on the host and triggering an IDS alert.

**When** did it occur?
> - 1:11 p.m. (email received)
> - 1:13 p.m. (file opened/execution)
> - 1:15 p.m. (malicious file creation)
> - 1:20 p.m. (alert triggered)

**Where** did it happen?
> On an employee's workstation within the organization's internal network environment.

**Why** did it happen?
> The attack succeeded due to social engineering combined with a password-protected attachment, which likely bypassed email security controls and relied on user interaction to execute the malicious payload.

---

### Additional Notes

> - The use of a password-protected attachment suggests intentional evasion of email scanning tools.
> - The rapid timeline, about seven minutes from delivery to detection, indicates automated or pre-staged payload execution.
> - The creation of multiple executables suggests a multi-stage infection or loader behavior, consistent with earlier analysis of the hash.
> - The SHA256 hash (54e6ea47...) should be used to pivot in threat intelligence platforms (e.g., VirusTotal) to identify related samples and infrastructure.
> - Recommended follow-up checks include persistence mechanisms, outbound network connections, and lateral movement indicators.

![Incident log walkthrough](./assets/incident-log.gif)

![Pyramid of Pain](./assets/pyramid-of-pain.gif)

---

### Reflections / Notes

**Were there any specific activities that were challenging for you? Why or why not?**
> File hashing, checksums, and fingerprinting, are really hard to comprehend, but they are so worth understanding.

**Has your understanding of incident detection and response changed since taking this course?**
> This activity made me realize how often I see these concepts everywhere when using a computer. It is strange knowing what they actually do. 

**Was there a specific tool or concept that you enjoyed the most? Why?**
> I really leaned into Github commits via the terminal for the Incident Handler's Journal, and I am really glad that I did. I have learned a lot about how Saas works. 
