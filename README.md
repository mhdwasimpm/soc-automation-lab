# SOC Automation Lab

> Automated Security Monitoring, Threat Intelligence Enrichment, and Incident Notification using Wazuh, Shuffle SOAR, VirusTotal, and Telegram.

## Project Overview

SOC Automation Lab is a practical Security Operations Center (SOC) project designed to demonstrate how security events can be automatically detected, enriched, and delivered to analysts in real time.

The lab integrates **Wazuh SIEM**, **Shuffle SOAR**, **VirusTotal Threat Intelligence**, and **Telegram Notifications** to create an end-to-end security monitoring and response workflow.

This project focuses on reducing manual investigation effort by automating alert enrichment and providing actionable intelligence to security analysts.

---

## Key Features

✅ Security Monitoring using Wazuh SIEM

✅ SSH Authentication Monitoring

✅ File Integrity Monitoring (FIM)

✅ Automated Alert Enrichment

✅ VirusTotal Threat Intelligence Integration

✅ Shuffle SOAR Workflow Automation

✅ Real-Time Telegram Notifications

✅ MITRE ATT&CK Mapped Detections

✅ Custom Detection Rules

✅ Python-Based Alert Processing

---

## Architecture

### Infrastructure Layout


System 1 (Windows 11)

├── Kali Linux VM (Attacker)

└── Docker Desktop
    └── Shuffle SOAR


System 2 (Windows 11)

├── Ubuntu Server VM
│   └── Wazuh Manager

└── Kali Linux VM
    └── Wazuh Agent (Monitored Endpoint)


---

## End-to-End Security Workflow


┌─────────────────┐
│ Kali Attacker   │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ Kali Endpoint   │
│ (Wazuh Agent)   │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ Wazuh Manager   │
│ SIEM Detection  │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ Shuffle SOAR    │
│ Automation      │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ VirusTotal      │
│ Enrichment      │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ Telegram Alert  │
│ Analyst Notice  │
└─────────────────┘


---

## Technologies Used

### Security Monitoring

* Wazuh SIEM
* Wazuh Agent

### SOAR Automation

* Shuffle SOAR
* Python

### Threat Intelligence

* VirusTotal API

### Notifications

* Telegram Bot API

### Infrastructure

* Windows 11
* Oracle VirtualBox
* Docker Desktop
* Ubuntu Server
* Kali Linux

---

## Architecture Diagram

Refer to: - architecture/11-project-architecture.png

---

## Project Screenshots

### Wazuh Dashboard

```text
screenshots/01-wazuh-dashboard.png
```

### Agent Registration

```text
screenshots/02-agent-connected.png
```

### Alert Generation

```text
screenshots/03-alert-generated.png
screenshots/04-alert-details.png
```

### Shuffle Workflow

```text
screenshots/05-shuffle-workflow.png
screenshots/12-shuffle-workflow-design.png
```

### VirusTotal Enrichment

```text
screenshots/06-virustotal-enrichment.png
```

### Telegram Notifications

```text
screenshots/07-telegram-notification.png
```

### File Integrity Monitoring

```text
screenshots/08-fim-test-file-modification.png
screenshots/09-fim-alert-triggered.png
```

### End-to-End Workflow Validation

```text
screenshots/10-end-to-end-workflow.png
```

---

# Detection Scenarios

The SOC Automation Lab validates security monitoring and automation using two primary detection scenarios.

## Scenario 1: SSH Authentication Monitoring

This scenario demonstrates the detection of unauthorized SSH authentication attempts against the monitored endpoint.

### Detection Capabilities

* Invalid user login attempts
* Failed SSH authentications
* SSH brute-force activity
* Suspicious source IP identification

### Workflow


SSH Attack Attempt
        │
        ▼
Wazuh Authentication Alert
        │
        ▼
Shuffle SOAR
        │
        ▼
VirusTotal IP Lookup
        │
        ▼
Telegram Notification


### Associated Wazuh Rules

| Rule ID | Description                      |
| ------- | -------------------------------- |
| 5710    | Invalid SSH User Login           |
| 5712    | Multiple Authentication Failures |
| 5758    | SSH Authentication Attack        |
| 5763    | SSH Brute Force Detection        |

---

## Scenario 2: File Integrity Monitoring (FIM)

This scenario demonstrates detection of unauthorized file system changes on the monitored endpoint.

### Detection Capabilities

* File Creation
* File Modification
* File Deletion
* Integrity Checksum Changes

### Workflow


File System Change
        │
        ▼
Wazuh FIM Alert
        │
        ▼
SHA256 Extraction
        │
        ▼
VirusTotal File Lookup
        │
        ▼
Telegram Notification


### Associated Wazuh Rules

| Rule ID | Description   |
| ------- | ------------- |
| 550     | File Modified |
| 553     | File Deleted  |
| 554     | File Created  |

---

# SOAR Automation Workflow

The project uses Shuffle SOAR to automate alert processing and threat intelligence enrichment.

## Workflow Components


Webhook Trigger
        │
        ▼
Python Enrichment Playbook
        │
        ▼
VirusTotal Intelligence Lookup
        │
        ▼
Alert Classification
        │
        ▼
Telegram Notification


## Automated Actions

### SSH Alerts

* Extract Source IP
* Perform VirusTotal Reputation Lookup
* Classify Severity
* Generate Analyst Notification

### FIM Alerts

* Extract SHA256 Hash
* Perform VirusTotal File Lookup
* Classify Severity
* Generate Analyst Notification

---

# Alert Enrichment Playbook

A custom Python playbook was developed to automate indicator enrichment and notification generation.

### Core Functions

✅ Alert Parsing

✅ Source IP Extraction

✅ SHA256 Hash Extraction

✅ VirusTotal IP Reputation Lookup

✅ VirusTotal File Reputation Lookup

✅ Alert Severity Classification

✅ Telegram Message Formatting

### Playbook Location

- playbooks/alert_enrichment_playbook.py

---

# Detection Rules

The project uses a combination of built-in and custom Wazuh rules.

## Built-in Rules

```text
5710 - Invalid SSH User Login
5712 - Multiple Authentication Failures
5758 - SSH Authentication Attack
5763 - SSH Brute Force Detection

550  - File Modified
553  - File Deleted
554  - File Created
```

## Custom Rules

Custom rules were created to enhance:

* SSH Monitoring
* Brute Force Detection
* File Integrity Monitoring
* Alert Prioritization

Location:

- detection-rules/custom_rules.xml


---

# MITRE ATT&CK Mapping

The project maps detected activities to the MITRE ATT&CK framework.

| Technique ID | Technique                 | Tactic            |
| ------------ | ------------------------- | ----------------- |
| T1110.001    | Password Guessing         | Credential Access |
| T1021.004    | SSH                       | Lateral Movement  |
| T1565.001    | Stored Data Manipulation  | Impact            |
| T1070        | Indicator Removal on Host | Defense Evasion   |

### MITRE Coverage

```text
SSH Attack
├── T1110.001 Password Guessing
└── T1021.004 SSH

File Integrity Monitoring
├── T1565.001 Stored Data Manipulation
└── T1070 Indicator Removal
```

Detailed mapping:

```text
docs/mitre-mapping.md
```

---

# Repository Structure

```text
soc-automation-lab/
│
├── architecture/
│   └── 11-project-architecture.png
│
├── screenshots/
│   ├── 01-wazuh-dashboard.png
│   ├── 02-agent-connected.png
│   ├── 03-alert-generated.png
│   ├── 04-alert-details.png
│   ├── 05-shuffle-workflow.png
│   ├── 06-virustotal-enrichment.png
│   ├── 07-telegram-notification.png
│   ├── 08-fim-test-file-modification.png
│   ├── 09-fim-alert-triggered.png
│   ├── 10-end-to-end-workflow.png
│   └── 12-shuffle-workflow-design.png
│
├── workflow/
├── detection-rules/
├── sample-alerts/
├── playbooks/
└── docs/
```

---

# Skills Demonstrated

## Security Operations

* Security Monitoring
* Alert Triage
* Incident Investigation
* Threat Detection
* Threat Intelligence Analysis

---

## SIEM & Detection Engineering

* Wazuh SIEM
* Security Event Analysis
* Log Monitoring
* Detection Rule Analysis
* File Integrity Monitoring

---

## SOAR & Automation

* Shuffle SOAR
* Workflow Automation
* Alert Enrichment
* Incident Notification
* Security Process Automation

---

## Threat Intelligence

* VirusTotal Integration
* IP Reputation Analysis
* File Hash Reputation Analysis
* Threat Context Enrichment

---

## Infrastructure & Administration

* Linux Administration
* VirtualBox
* Docker Desktop
* Network Configuration
* Endpoint Monitoring

---

## Programming & Scripting

* Python
* API Integration
* JSON Processing
* Alert Parsing
* Automation Logic

---

# Learning Outcomes

Through this project, I gained practical experience in:

* Building and managing a SIEM environment
* Monitoring security events across endpoints
* Implementing File Integrity Monitoring
* Creating automated SOAR workflows
* Integrating external threat intelligence sources
* Mapping security events to MITRE ATT&CK techniques
* Investigating security alerts using contextual intelligence
* Developing automation scripts for SOC operations

---

# Future Improvements

Potential enhancements for future versions include:

### Detection Enhancements

* Web attack detection
* Malware detection use cases
* Suspicious process monitoring
* Privilege escalation detection

### Automation Enhancements

* Automated IP blocking
* Automated incident ticket creation
* Multi-source threat intelligence enrichment
* Email-based alerting

### Visualization Enhancements

* Security dashboards
* Threat intelligence reporting
* Alert trend analysis
* Incident metrics visualization

---

# Project Outcome

This project successfully demonstrates an end-to-end Security Operations Center workflow using industry-relevant tools and techniques.

The implementation showcases how security alerts can be:

1. Detected by Wazuh SIEM
2. Processed by Shuffle SOAR
3. Enriched using VirusTotal
4. Classified based on threat intelligence
5. Delivered to analysts through Telegram notifications

The result is a streamlined and automated incident monitoring process that reduces manual investigation effort while improving analyst visibility into security events.

---

# Documentation

Additional project documentation is available in the `docs/` directory:

```text
docs/
├── setup-guide.md
├── architecture-overview.md
├── attack-simulation.md
└── mitre-mapping.md
```

---

# Disclaimer

This project was developed for educational and defensive cybersecurity purposes only.

All testing, attack simulations, and security validations were performed within a controlled laboratory environment owned and managed by the author.

No unauthorized systems or third-party environments were targeted during the development of this project.
