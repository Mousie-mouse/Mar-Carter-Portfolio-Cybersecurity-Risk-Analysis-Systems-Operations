# Incident Journal

---

## Journal Entry

| Field | Details |
|-------|---------|
| **Date** | `2026-05-07` |
| **Entry #** | `004` |
| **Scenario** | Wazuh Filebeat ingestion failure on Linux VirtualBox host |

---

### Description

During a Wazuh SIEM lab activity, a Linux-hosted VirtualBox deployment was configured to ingest tutorial datasets into the Wazuh dashboard using Filebeat. The activity involved configuring shared folders, validating ingestion paths, modifying Filebeat YAML configurations, and troubleshooting ingestion failures.

The provided course instructions directed learners to mount the dataset using a VirtualBox shared folder (`/media/sf_buttercup-shared`) and configure Filebeat to send data using a Logstash output configuration.

Multiple environment-related failures were encountered during the investigation, including:

- Filebeat runtime crashes
- Golang panic traces
- Shared-folder permission inconsistencies
- Incomplete ingestion behavior
- Misleading monitoring telemetry
- Logstash connection failures
- Inconsistent indexing behavior inside Wazuh/OpenSearch

The investigation expanded beyond simple configuration troubleshooting into environment validation and infrastructure debugging.

Several remediation attempts were performed, including:

- validating ingestion paths,
- checking mounted shared folders,
- migrating datasets into native VM storage,
- testing Filebeat outputs,
- validating Elasticsearch/OpenSearch indices,
- reviewing kernel and journal diagnostics,
- and comparing expected architecture behavior against the actual Wazuh OVA deployment.

Although partial ingestion was achieved and Elasticsearch connectivity was confirmed, the activity could not be completed reliably due to repeated Filebeat instability and environmental inconsistencies.

The scenario was documented as a technical troubleshooting repository titled:

> "VirtualBox Ate My Homework?"

The repository included:

- screenshots,
- command output,
- configuration files,
- crash traces,
- and Linux-specific troubleshooting observations.

---

### Tools Used

| Tool | Purpose |
|------|---------|
| `Wazuh` | SIEM platform used for ingestion and log analysis |
| `Filebeat` | Log shipping and ingestion utility |
| `Oracle VirtualBox` | Virtual machine hypervisor used to host the Wazuh OVA |
| `Linux Terminal` | Executed troubleshooting, validation, and system inspection commands |
| `curl` | Queried Elasticsearch/OpenSearch indices directly |
| `journalctl` | Reviewed system and service logs |
| `dmesg` | Reviewed kernel diagnostics and runtime errors |
| `OpenSearch / Elasticsearch APIs` | Validated index creation and ingestion behavior |
| `nano` | Created and edited YAML ingestion configurations |
| `Git / GitHub` | Documented findings and preserved troubleshooting artifacts |

---

### The 5 W's

**Who** caused the incident?
> N/A. This was a lab and environment compatibility issue rather than an incident caused by a threat actor.

**What** happened?
> Filebeat repeatedly failed to ingest the expected tutorial datasets into Wazuh/OpenSearch reliably. The failures included crashes, incomplete ingestion, misleading telemetry, and architecture mismatches between the lab instructions and the deployed Wazuh OVA.

**When** did it occur?
> The troubleshooting activity took place on May 7, 2026.

**Where** did it happen?
> The issue occurred in a Linux-hosted VirtualBox environment running the Wazuh OVA, with datasets mounted through a VirtualBox shared folder and later migrated into native VM storage.

**Why** did it happen?
> The most likely cause was a combination of Linux VirtualBox shared-folder behavior, Filebeat instability, permission inconsistencies, and course instructions that referenced a Logstash-based architecture that did not match the actual Wazuh OVA deployment.

---

### Additional Notes

Observed findings included:

- Filebeat sometimes appeared healthy while failing internally.
- Log ingestion counters occasionally increased despite incomplete or stalled ingestion.
- VirtualBox shared folders behaved inconsistently compared to native Linux filesystem paths.
- The provided lab instructions referenced a Logstash architecture that did not fully match the deployed Wazuh OVA environment.
- Migrating the dataset into native VM storage improved ingestion consistency but did not completely eliminate instability.
- Several Filebeat crashes produced Golang goroutine panic traces during harvesting operations.

Key troubleshooting commands included:

```bash
sudo /usr/share/filebeat/bin/filebeat test config -c /home/wazuh-user/ingest.yml

sudo /usr/share/filebeat/bin/filebeat test output -c /home/wazuh-user/ingest.yml

sudo curl -k -u admin:admin 'https://127.0.0.1:9200/_cat/indices?v'

sudo journalctl -xe | tail -50

sudo dmesg | tail -50

sudo ss -lntp | grep 5044
```

---

### Reflections / Notes

**Were there any specific activities that were challenging for you? Why or why not?**
> This activity was very challenging because I was not able to complete it using the course instructions. Because I had spent a lot of effort trying to get the configuration correct for my Linux host machine, I decided to continue troubleshooting until I could identify the cause. I was not able to fully fix the issue, but I believe I reached the point where I could conclude that it was not actually a configuration issue. Instead, Linux compatibility and VirtualBox shared-folder behavior appeared to create the problem.

**Has your understanding of incident detection and response changed since taking this course?**
> Very much so. I am learning how to document my assessments and explain the reasoning behind my findings.

**Was there a specific tool or concept that you enjoyed the most? Why?**
> I like GitHub. The more I use it, the more I want to use it. I have been building Linux tools, and some of them are projects I hope to share.
