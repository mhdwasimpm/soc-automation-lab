# MITRE ATT&CK Mapping

This document maps the security events detected in the SOC Automation Lab to the MITRE ATT&CK framework.

---

# Purpose

MITRE ATT&CK is a globally recognized knowledge base used to classify adversary tactics and techniques.

The SOC Automation Lab uses MITRE ATT&CK mappings provided by Wazuh rules to better understand and categorize security events.

---

# SSH Authentication Monitoring

## Technique: T1110.001 – Password Guessing

### Tactic

Credential Access

### Description

Attackers attempt to gain access to systems by guessing valid usernames and passwords through repeated authentication attempts.

### Detection

Detected through Wazuh SSH authentication monitoring rules.

### Example

* Invalid user login attempts
* Repeated failed SSH logins
* SSH brute-force activity

### Relevant Wazuh Rules

* Rule ID 5710
* Rule ID 5712
* Rule ID 5758
* Rule ID 5763

---

## Technique: T1021.004 – SSH

### Tactic

Lateral Movement

### Description

Adversaries may use Secure Shell (SSH) to access remote systems and move within a network.

### Detection

Detected when unauthorized or suspicious SSH authentication attempts occur.

### Example

* SSH login attempts from unauthorized sources
* Repeated authentication failures

### Relevant Wazuh Rules

* Rule ID 5710
* Rule ID 5712
* Rule ID 5758
* Rule ID 5763

---

# File Integrity Monitoring (FIM)

## Technique: T1565.001 – Stored Data Manipulation

### Tactic

Impact

### Description

Adversaries may modify files, configurations, or stored data to disrupt operations or alter information.

### Detection

Detected through Wazuh File Integrity Monitoring.

### Example

* File modification
* Unauthorized file changes
* Integrity checksum changes

### Relevant Wazuh Rules

* Rule ID 550
* Rule ID 554

---

## Technique: T1070 – Indicator Removal on Host

### Tactic

Defense Evasion

### Description

Attackers may delete files or artifacts to hide malicious activity and avoid detection.

### Detection

Detected through File Integrity Monitoring when monitored files are removed.

### Example

* Deletion of monitored files
* Removal of security-related artifacts

### Relevant Wazuh Rules

* Rule ID 553

---

# Mapping Summary

| Security Scenario             | MITRE Technique | Technique Name            | Tactic            |
| ----------------------------- | --------------- | ------------------------- | ----------------- |
| SSH Authentication Monitoring | T1110.001       | Password Guessing         | Credential Access |
| SSH Authentication Monitoring | T1021.004       | SSH                       | Lateral Movement  |
| File Integrity Monitoring     | T1565.001       | Stored Data Manipulation  | Impact            |
| File Integrity Monitoring     | T1070           | Indicator Removal on Host | Defense Evasion   |

---

# Benefits of MITRE Mapping

* Standardized threat classification
* Better understanding of attacker behavior
* Improved incident investigation
* Faster alert triage
* Alignment with industry security frameworks

---

# Conclusion

The SOC Automation Lab demonstrates how Wazuh detections can be mapped to MITRE ATT&CK techniques, helping analysts understand attacker behavior and prioritize response activities using a standardized threat framework.
