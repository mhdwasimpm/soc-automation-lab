# Sample Alerts

This folder contains sanitized Wazuh alerts collected during the SOC Automation Lab. The alerts demonstrate how security events are detected and processed through an automated workflow using Wazuh, Shuffle, VirusTotal, and Telegram.

## Files

### ssh-bruteforce-alert.json

Sample alert generated when multiple SSH authentication attempts were made using an invalid user account.

**Detection Details**

* Rule ID: 5710
* Severity Level: 5
* Event Type: Failed SSH Authentication
* MITRE ATT&CK:

  * T1110.001 – Password Guessing
  * T1021.004 – SSH

**Workflow**
SSH Authentication Failure → Wazuh Detection → Shuffle Processing → Telegram Notification

---

### fim-alert.json

Sample alert generated when a monitored file was modified on the endpoint.

**Detection Details**

* Rule ID: 550
* Severity Level: 7
* Event Type: File Integrity Monitoring (FIM)
* MITRE ATT&CK:

  * T1565.001 – Stored Data Manipulation

**Workflow**
File Modification → Wazuh FIM Detection → SHA256 Extraction → VirusTotal Enrichment → Telegram Notification

---

