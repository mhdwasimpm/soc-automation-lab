# Playbooks

This folder contains the Python automation logic used in the SOC Automation Lab.

## alert_enrichment_playbook.py

This playbook processes Wazuh alerts received through Shuffle SOAR and performs threat intelligence enrichment using VirusTotal before generating analyst-friendly Telegram notifications.

## Supported Use Cases

### SSH Authentication Monitoring & Brute Force Detection

The playbook extracts attacker IP addresses from SSH-related alerts and enriches them using VirusTotal IP reputation data.

Workflow:

Wazuh SSH Alert
→ Shuffle SOAR
→ Python Playbook
→ VirusTotal IP Lookup
→ Telegram Notification

### File Integrity Monitoring (FIM)

The playbook extracts SHA256 hashes from File Integrity Monitoring alerts and enriches them using VirusTotal file reputation data.

Workflow:

Wazuh FIM Alert
→ Shuffle SOAR
→ Python Playbook
→ VirusTotal File Hash Lookup
→ Telegram Notification

## Main Functions

* Parses Wazuh alert fields
* Extracts rule ID, agent information, file hashes, and source IP addresses
* Performs VirusTotal file and IP reputation lookups
* Classifies alert severity based on threat intelligence results
* Generates structured Telegram notifications
* Provides recommended response actions for analysts

## Security Note

The VirusTotal API key has been removed from the public version of the script and replaced with `REDACTED`.

## Requirements

```bash
pip install requests
```

## Technologies Used

* Wazuh SIEM
* Shuffle SOAR
* VirusTotal API
* Python
* Telegram Bot API

## Purpose

This playbook demonstrates SOAR-driven alert enrichment and automated incident notification, reducing manual investigation effort and providing analysts with actionable threat intelligence in real time.
