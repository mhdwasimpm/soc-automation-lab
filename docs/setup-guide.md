# Setup Guide

This document describes the environment, architecture, installation steps, and configuration used to build the SOC Automation Lab.

---

# Physical Lab Layout

System 1 (Windows 11)

├── Kali Linux VM (Attacker)

└── Docker Desktop

    └── Shuffle SOAR

        ├── Webhook

        ├── Python Enrichment

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

# Communication Flow

Kali Linux (Attacker)

→ Kali Linux (Monitored Endpoint)

→ Wazuh Agent

→ Wazuh Manager

→ Shuffle SOAR

→ VirusTotal

→ Telegram Notification

---

# Network Configuration

All virtual machines were configured using Bridged Networking in Oracle VirtualBox.

This configuration enabled direct communication between:

* Attacker VM
* Monitored Endpoint
* Wazuh Manager
* Shuffle SOAR Host

The setup simulates a small enterprise SOC environment where security events are collected, enriched, and automatically delivered to analysts.


Workflow:

Kali Linux (Attacker)

→ Kali Linux (Monitored Endpoint)

→ Wazuh Manager

→ Shuffle SOAR

→ VirusTotal

→ Telegram Notification


---

# Technologies Used

* Windows 11
* Oracle VirtualBox
* Ubuntu Server
* Ubuntu Desktop
* Kali Linux
* Wazuh SIEM
* Shuffle SOAR
* Docker Desktop
* VirusTotal API
* Telegram Bot API
* Python

---

# Step 1: Install Oracle VirtualBox

Install Oracle VirtualBox on both Windows systems.

Recommended Resources:

### Ubuntu Server VM

* RAM: 8 GB
* CPU: 2–4 Cores
* Storage: 50 GB

### Kali Linux VM (Monitored Endpoint)

- RAM: 2–4 GB
- CPU: 2 Cores
- Storage: 30 GB

### Kali Linux VM (Attacker)

* RAM: 2–4 GB
* CPU: 2 Cores
* Storage: 30 GB

Configure all virtual machines using Bridged Network Adapter mode.

---

# Step 2: Install Ubuntu Server

Purpose:

Host the Wazuh Manager.

Installation:

```bash
sudo apt update && sudo apt upgrade -y
```

Verify network configuration:

```bash
ip a
```

Record the Ubuntu Server IP address.

---

# Step 3: Install Wazuh Manager

```bash
curl -sO https://packages.wazuh.com/4.x/wazuh-install.sh
sudo bash wazuh-install.sh -a
```

Verify installation:

```bash
sudo systemctl status wazuh-manager
```

Access the dashboard:

```text
https://<ubuntu-server-ip>
```

---

# Step 4: Install Kali Linux (Monitored Endpoint)

Purpose:

Monitored endpoint used for security monitoring and File Integrity Monitoring.

Update packages:

```bash
sudo apt update && sudo apt upgrade -y
```

---

# Step 5: Install Wazuh Agent

Install the Wazuh Agent on the Kali Linux monitored endpoint.

Configure the manager IP address:

```bash
sudo nano /var/ossec/etc/ossec.conf
```

Start the agent:

```bash
sudo systemctl enable wazuh-agent
sudo systemctl start wazuh-agent
```

Verify agent connectivity from the Wazuh dashboard.

---

# Step 6: Install Kali Linux

Purpose:

Attack simulation and security testing.

Update packages:

```bash
sudo apt update && sudo apt upgrade -y
```

Verify communication with the monitored endpoint and Wazuh environment.

---

# Step 7: Install Docker Desktop

Install Docker Desktop on System 1.

Verify installation:

```powershell
docker --version
docker ps
```

---

# Step 8: Deploy Shuffle SOAR

Create Docker network:

```powershell
docker network create shuffle
```

Deploy Shuffle using Docker.

Verify running containers:

```powershell
docker ps
```

Access Shuffle:

```text
http://localhost:3001
```

Create the administrator account and configure integrations.

---

# Step 9: Configure VirusTotal

Purpose:

Threat intelligence enrichment.

Configuration Steps:

1. Create a VirusTotal account.
2. Generate an API key.
3. Configure the API key within the Shuffle workflow.
4. Verify API connectivity.

Used For:

* File hash reputation lookup
* IP reputation lookup
* Threat intelligence enrichment

---

# Step 10: Configure Telegram

Purpose:

Real-time analyst notifications.

Configuration Steps:

1. Create a Telegram bot using BotFather.
2. Obtain Bot Token.
3. Obtain Chat ID.
4. Configure Telegram integration inside Shuffle.

---

# Step 11: Build Shuffle Workflow

Workflow Components:

* Webhook Trigger
* Python Processing Node
* VirusTotal Enrichment
* Telegram Notification

Workflow:

Wazuh Alert

→ Shuffle Webhook

→ Python Playbook

→ VirusTotal Lookup

→ Telegram Notification

---

# Step 12: Configure File Integrity Monitoring

Create monitoring directory:

```bash
mkdir ~/fim-test
```

Configure File Integrity Monitoring within Wazuh.

Restart the agent:

```bash
sudo systemctl restart wazuh-agent
```

---

# Step 13: Simulate Security Events

## SSH Authentication Monitoring

Generate failed authentication attempts from Kali Linux against the monitored endpoint.

Expected Result:

* Wazuh Authentication Alert
* Shuffle Processing
* VirusTotal IP Enrichment
* Telegram Notification

---

## File Integrity Monitoring

Create a file:

```bash
echo "test" > eicar-test1.txt
```

Modify the file:

```bash
echo "modified" >> eicar-test1.txt
```

Expected Result:

* Wazuh FIM Alert
* VirusTotal File Lookup
* Telegram Notification

---

# Validation Checklist

✅ Wazuh Manager Operational

✅ Wazuh Agent Connected

✅ Docker Desktop Installed

✅ Shuffle SOAR Running

✅ VirusTotal Integrated

✅ Telegram Integrated

✅ SSH Authentication Alerts Generated

✅ FIM Alerts Generated

✅ End-to-End SOAR Workflow Verified

---

# Project Outcome

The SOC Automation Lab demonstrates how security alerts can be automatically collected, enriched, and delivered to analysts using Wazuh, Shuffle SOAR, VirusTotal, and Telegram. The project showcases SIEM monitoring, threat intelligence integration, File Integrity Monitoring, alert enrichment, and automated incident notification workflows.

