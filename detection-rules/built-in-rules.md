# Built-in Wazuh Rules

This project primarily uses built-in Wazuh detection rules to identify security events and generate alerts for automated processing through Shuffle SOAR.

## Rule ID 5710

**Description:** SSH invalid user login attempt

**Severity Level:** 5

**Category:** Authentication Monitoring

**MITRE ATT&CK:**

* T1110.001 – Password Guessing
* T1021.004 – SSH

**Use Case:**
Generated when a login attempt is made using a non-existent user account through SSH.

---

## Rule ID 5712

**Description:** Multiple SSH authentication failures

**Severity Level:** Medium to High

**Category:** Authentication Monitoring

**MITRE ATT&CK:**

* T1110.001 – Password Guessing

**Use Case:**
Generated when multiple failed SSH authentication attempts occur within a defined timeframe.

---

## Rule ID 5763

**Description:** SSH brute-force detection threshold reached

**Severity Level:** High

**Category:** Brute Force Detection

**MITRE ATT&CK:**

* T1110.001 – Password Guessing

**Use Case:**
Generated when repeated SSH login failures indicate possible brute-force activity.

---

## Rule ID 550

**Description:** Integrity checksum changed

**Severity Level:** 7

**Category:** File Integrity Monitoring

**MITRE ATT&CK:**

* T1565.001 – Stored Data Manipulation

**Use Case:**
Generated when a monitored file is modified and its checksum changes.

---

## Rule ID 554

**Description:** File added to monitored directory

**Severity Level:** Medium

**Category:** File Integrity Monitoring

**MITRE ATT&CK:**

* T1565.001 – Stored Data Manipulation

**Use Case:**
Generated when a new file is created in a monitored location.

---

## Rule ID 553

**Description:** File deleted from monitored directory

**Severity Level:** Medium

**Category:** File Integrity Monitoring

**MITRE ATT&CK:**

* T1070 – Indicator Removal on Host

**Use Case:**
Generated when a monitored file is removed.
