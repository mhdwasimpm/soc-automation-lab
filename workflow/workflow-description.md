# Workflow Description

## Overview

This SOC Automation Lab uses Wazuh, Shuffle, VirusTotal, and Telegram to automate alert enrichment and notification.

Two workflow implementations were developed and tested during the project.

---

## Workflow 1: Dedicated VirusTotal Node

File:
`shuffle-workflow-virustotal-node.json`

Flow:

Wazuh Alert
→ Analyze Log
→ VirusTotal Node
→ Python Processing
→ Telegram Notification

Advantages:

* Easy to visualize
* Simple troubleshooting
* Clear SOAR workflow representation
* Suitable for demonstrations and documentation

---

## Workflow 2: VirusTotal Lookup Inside Python

File:
`shuffle-workflow-python-vt.json`

Flow:

Wazuh Alert
→ Python Processing (VirusTotal API Query)
→ Telegram Notification

Advantages:

* Fewer workflow nodes
* More customization through code
* Flexible logic handling

---

## Implemented Use Cases

### SSH Brute Force Detection

1. Wazuh detects multiple failed SSH login attempts.
2. Shuffle processes the alert.
3. Threat intelligence enrichment is performed.
4. Telegram notification is generated.

### File Integrity Monitoring (FIM)

1. Wazuh detects file creation or modification.
2. SHA256 hash is extracted.
3. VirusTotal reputation lookup is performed.
4. Enriched alert is sent through Telegram.

---

## Technologies Used

* Wazuh SIEM
* Shuffle SOAR
* VirusTotal API
* Telegram Bot API
* Python
* Ubuntu
* Kali Linux

---

## Outcome

The project demonstrates automated detection, enrichment, and notification workflows for common SOC use cases, reducing manual investigation effort and improving response efficiency.
