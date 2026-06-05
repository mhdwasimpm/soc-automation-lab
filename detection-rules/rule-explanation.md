# Detection Rules

This folder contains the built-in Wazuh rules and custom detection rules used in the SOC Automation Lab. These rules were used to monitor SSH authentication activity and File Integrity Monitoring (FIM) events, which were then processed through Shuffle SOAR for automated enrichment and notification.

---

# Built-in Wazuh Rules

The following built-in Wazuh rules were used during the project.

## SSH Authentication Monitoring

| Rule ID | Description                                 |
| ------- | ------------------------------------------- |
| 5710    | SSH invalid user login attempt              |
| 5712    | Multiple SSH authentication failures        |
| 5763    | SSH brute-force detection threshold reached |

### MITRE ATT&CK

* T1110.001 – Password Guessing
* T1021.004 – SSH

### Use Case

These rules detect failed SSH authentication attempts, invalid user logins, and brute-force attack patterns targeting the monitored endpoint.

---

## File Integrity Monitoring (FIM)

| Rule ID | Description                           |
| ------- | ------------------------------------- |
| 550     | Integrity checksum changed            |
| 553     | File deleted from monitored directory |
| 554     | File added to monitored directory     |

### MITRE ATT&CK

* T1565.001 – Stored Data Manipulation
* T1070 – Indicator Removal on Host

### Use Case

These rules detect file creation, modification, and deletion activities within monitored directories.

---

# Custom Rules

Custom rules were created to demonstrate detection engineering, alert tuning, and security monitoring concepts.

## Rule ID 100100

**Description:** SOAR Lab: SSH login attempt using invalid user detected

**Based On:** Rule 5710

**Purpose:**
Generates a customized alert when an invalid SSH login attempt is detected.

### MITRE ATT&CK

* T1110.001 – Password Guessing
* T1021.004 – SSH

---

## Rule ID 100101

**Description:** SOAR Lab: Possible SSH brute force activity detected

**Based On:** Rule 5710

**Purpose:**
Detects repeated SSH authentication failures within a short timeframe and increases alert severity for investigation.

### MITRE ATT&CK

* T1110.001 – Password Guessing
* T1021.004 – SSH

---

## Rule ID 100102

**Description:** SOAR Lab: Monitored file modified - FIM alert generated

**Based On:** Rule 550

**Purpose:**
Detects modifications to monitored files and directories.

### MITRE ATT&CK

* T1565.001 – Stored Data Manipulation

---

## Rule ID 100103

**Description:** SOAR Lab: New file added in monitored directory

**Based On:** Rule 554

**Purpose:**
Detects file creation events within monitored directories.

### MITRE ATT&CK

* T1565.001 – Stored Data Manipulation

---

## Rule ID 100104

**Description:** SOAR Lab: File deleted from monitored directory

**Based On:** Rule 553

**Purpose:**
Detects file deletion activity within monitored directories.

### MITRE ATT&CK

* T1070 – Indicator Removal on Host

---

# Rule Mapping

The project combines built-in Wazuh rules with custom rules to provide enhanced visibility and alert tuning.

| Built-in Rule | Description                           | Custom Rule | Purpose                            |
| ------------- | ------------------------------------- | ----------- | ---------------------------------- |
| 5710          | SSH invalid user login attempt        | 100100      | Custom SSH invalid login detection |
| 5710          | SSH invalid user login attempt        | 100101      | SSH brute-force pattern detection  |
| 550           | Integrity checksum changed            | 100102      | Custom FIM modification detection  |
| 554           | File added to monitored directory     | 100103      | Custom file creation detection     |
| 553           | File deleted from monitored directory | 100104      | Custom file deletion detection     |

---

# SOC Automation Integration

## SSH Brute Force Detection Flow

SSH Authentication Failure
→ Wazuh Built-in Rule (5710)
→ Custom Rule (100100 / 100101)
→ Shuffle SOAR
→ Telegram Notification

---

## File Integrity Monitoring Flow

File Created / Modified / Deleted
→ Wazuh Built-in Rule (550 / 553 / 554)
→ Custom Rule (100102 / 100103 / 100104)
→ VirusTotal Enrichment
→ Telegram Notification

---

# MITRE ATT&CK Coverage

| Technique ID | Technique                 |
| ------------ | ------------------------- |
| T1110.001    | Password Guessing         |
| T1021.004    | SSH                       |
| T1565.001    | Stored Data Manipulation  |
| T1070        | Indicator Removal on Host |

---

# Purpose

These rules demonstrate how Wazuh can be used for authentication monitoring, file integrity monitoring, and basic detection engineering. Combined with Shuffle SOAR, VirusTotal, and Telegram, they form an automated workflow for alert enrichment, threat intelligence integration, and incident notification.
