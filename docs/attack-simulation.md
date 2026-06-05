# Attack Simulation

This document describes the security scenarios used to test and validate the SOC Automation Lab.

---

# Objective

The purpose of the attack simulations was to verify that:

* Wazuh detects security events
* Shuffle SOAR processes alerts
* VirusTotal enriches indicators
* Telegram notifications are generated successfully

---

# Scenario 1: SSH Authentication Monitoring

## Description

This scenario tests the detection of unauthorized SSH authentication attempts against the monitored endpoint.

## Attack Source

* Kali Linux (Attacker)

## Target

* Kali Linux (Monitored Endpoint)

## Detection Method

Wazuh monitors SSH authentication logs and generates alerts when suspicious login activity is detected.

## Alert Types Generated

### Invalid User Login

Rule ID:

```text
5710
```

Description:

```text
sshd: Attempt to login using a non-existent user
```

---

### Multiple Authentication Failures

Rule IDs:

```text
5712
5758
5763
```

Description:

```text
Repeated failed SSH login attempts indicating possible brute-force activity.
```

---

## Workflow

Attacker

→ SSH Authentication Attempts

→ Wazuh Agent

→ Wazuh Manager

→ Shuffle SOAR

→ VirusTotal IP Lookup

→ Telegram Notification

---

## Expected Result

* SSH alert generated
* Source IP extracted
* VirusTotal reputation lookup performed
* Telegram notification delivered

---

## Screenshots


![End-to-End Workflow](screenshots/03-alert-generated.png)
![End-to-End Workflow](screenshots/04-alert-details.png)
![End-to-End Workflow](screenshots/07-telegram-notification.png)

---

# Scenario 2: File Integrity Monitoring (FIM)

## Description

This scenario tests Wazuh's ability to detect file system changes on the monitored endpoint.

## Detection Method

Wazuh File Integrity Monitoring (FIM) continuously monitors configured directories and generates alerts when files are created, modified, or deleted.

---

## Test Directory

```text
~/fim-test
```

---

## File Creation Test

Example:

```bash
echo "test" > test.txt
```

Expected Result:

* File creation event detected
* Wazuh alert generated

---

## File Modification Test

Example:

```bash
echo "modified" >> test.txt
```

Expected Result:

* File modification detected
* SHA256 hash collected
* VirusTotal lookup performed

---

## File Deletion Test

Example:

```bash
rm test.txt
```

Expected Result:

* File deletion alert generated

---

## Workflow

File Change

→ Wazuh Agent

→ Wazuh Manager

→ Shuffle SOAR

→ Python Playbook

→ VirusTotal File Lookup

→ Telegram Notification

---

## Expected Result

* FIM alert generated
* SHA256 extracted
* VirusTotal enrichment performed
* Severity classification applied
* Telegram notification delivered

---

## Screenshots

![End-to-End Workflow](screenshots/08-fim-test-file-modification.png)
![End-to-End Workflow](screenshots/09-fim-alert-triggered.png)
![End-to-End Workflow](screenshots/07-telegram-notification.png)


---

# Validation Results

## SSH Authentication Monitoring

| Validation Item       | Status  |
| --------------------- | ------- |
| Alert Generated       | Success |
| VirusTotal Lookup     | Success |
| Telegram Notification | Success |
| Workflow Execution    | Success |

---

## File Integrity Monitoring

| Validation Item       | Status  |
| --------------------- | ------- |
| Alert Generated       | Success |
| SHA256 Extraction     | Success |
| VirusTotal Lookup     | Success |
| Telegram Notification | Success |
| Workflow Execution    | Success |

---

# Conclusion

The attack simulations successfully validated the end-to-end SOC workflow. Security events generated on the monitored endpoint were detected by Wazuh, processed by Shuffle SOAR, enriched using VirusTotal, and delivered to the analyst through Telegram notifications.
