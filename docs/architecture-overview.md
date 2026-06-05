# Architecture Overview

This document describes the architecture, communication flow, and major components used in the SOC Automation Lab.

---

# Physical Lab Layout

System 1 (Windows 11)

├── Kali Linux VM (Attacker)

└── Docker Desktop

    └── Shuffle SOAR

        ├── Webhook Trigger

        ├── Python Enrichment Playbook

        ├── VirusTotal Integration

        └── Telegram Notifications

---

System 2 (Windows 11)

├── Ubuntu Server VM

│   └── Wazuh Manager

│

└── Kali Linux VM

    └── Wazuh Agent (Monitored Endpoint)

---

# Network Configuration

All virtual machines were configured using Bridged Networking in Oracle VirtualBox.

This configuration enabled direct communication between:

* Kali Linux Attacker VM
* Kali Linux Monitored Endpoint
* Ubuntu Wazuh Manager
* Shuffle SOAR Host

The setup simulates a small enterprise SOC environment where security events are collected, enriched, and automatically delivered to analysts.

---

# Communication Flow

Kali Linux (Attacker)

→ Kali Linux (Monitored Endpoint)

→ Wazuh Agent

→ Wazuh Manager

→ Shuffle SOAR

→ VirusTotal

→ Telegram Notification

---

# Alert Processing Workflow

1. Security events are generated on the monitored Kali Linux endpoint.

2. The Wazuh Agent collects logs and monitoring events.

3. The Wazuh Manager analyzes incoming events and generates alerts.

4. Wazuh forwards alerts to Shuffle SOAR through a webhook.

5. Shuffle executes an automated workflow.

6. The Python playbook extracts relevant indicators such as:

   * Source IP addresses
   * SHA256 file hashes
   * Alert metadata

7. VirusTotal enriches the indicators with threat intelligence.

8. Alert severity is classified based on enrichment results.

9. A formatted notification is generated and delivered through Telegram.

---

# Component Description

## Wazuh Manager

Acts as the central Security Information and Event Management (SIEM) platform.

Responsibilities:

* Log collection
* Alert generation
* Agent management
* Event correlation
* File Integrity Monitoring

---

## Wazuh Agent

Installed on the monitored Kali Linux endpoint.

Responsibilities:

* Log collection
* File monitoring
* Event forwarding
* Security event reporting

---

## Shuffle SOAR

Acts as the Security Orchestration, Automation, and Response platform.

Responsibilities:

* Alert processing
* Workflow automation
* Threat intelligence integration
* Notification delivery

---

## Python Enrichment Playbook

Custom automation logic used within Shuffle.

Responsibilities:

* Alert parsing
* IP extraction
* File hash extraction
* VirusTotal queries
* Severity classification
* Notification formatting

---

## VirusTotal

Provides external threat intelligence.

Used For:

* IP reputation analysis
* File hash reputation analysis
* Threat enrichment

---

## Telegram

Used for real-time analyst notifications.

Notification Content:

* Alert details
* Source information
* Threat intelligence results
* Severity classification
* Recommended response actions

---

# Security Scenarios Demonstrated

## SSH Authentication Monitoring

Detects:

* Invalid user login attempts
* Failed SSH authentication
* SSH brute-force activity

Associated MITRE ATT&CK Techniques:

* T1110.001 – Password Guessing
* T1021.004 – SSH

---

## File Integrity Monitoring (FIM)

Detects:

* File creation
* File modification
* File deletion

Associated MITRE ATT&CK Techniques:

* T1565.001 – Stored Data Manipulation
* T1070 – Indicator Removal on Host

---

# Project Benefits

* Centralized security monitoring
* Automated alert enrichment
* Reduced manual investigation effort
* Real-time incident notification
* Threat intelligence integration
* Practical SOC workflow implementation
* MITRE ATT&CK aligned detection use cases

---

# Architecture Diagram


![project-architecture](architecture/project-architecture.png)


