# Wazuh Deployment on Ubuntu Server

## Overview

This document describes the deployment of **Wazuh SIEM** on an **Ubuntu Server** within an **Enterprise Security Homelab**. The Wazuh platform provides centralized log collection, security monitoring, alerting, and visualization for both Windows and Linux endpoints.

This deployment is designed to mirror **real-world SOC environments** while remaining safe, reproducible, and suitable for a public GitHub portfolio.

---

## Architecture Context

The Wazuh stack is deployed on an **Ubuntu Server VM** hosted on **Proxmox VE** and positioned behind a firewall (pfSense). It monitors multiple endpoints across the LAN and management networks using Wazuh agents.

**Wazuh components deployed:**

* Wazuh Manager
* Wazuh Indexer (OpenSearch-based)
* Wazuh Dashboard

> 📌 All IP addresses, hostnames, and credentials referenced are examples only.

---

## Prerequisites

* Ubuntu Server (LTS) installed and updated
* Minimum system resources:

  | Resource | Recommended |
  | -------- | ----------- |
  | vCPU     | 2–4         |
  | RAM      | 4–8 GB      |
  | Storage  | 50 GB       |
* Network connectivity to monitored endpoints
* Root or sudo privileges

---

## Step 1 – Prepare the Ubuntu Server

Update the system and install required packages:

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install curl apt-transport-https ca-certificates gnupg -y
```

Set the system hostname (example):

```bash
sudo hostnamectl set-hostname wazuh-server
```

---

## Step 2 – Install Wazuh Using the Quickstart Script

Wazuh provides an official installation script that deploys all core components.

Download and run the installer:

```bash
curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
sudo bash wazuh-install.sh -a
```

This process installs:

* Wazuh Manager
* Wazuh Indexer
* Wazuh Dashboard

Installation may take several minutes.

---

## Step 3 – Verify Wazuh Services

After installation, confirm all services are running:

```bash
sudo systemctl status wazuh-manager
sudo systemctl status wazuh-indexer
sudo systemctl status wazuh-dashboard
```

All services should show **active (running)**.

---

## Step 4 – Access the Wazuh Dashboard

From a browser on an authorized network:

```
https://<WAZUH_SERVER_IP>
```

Log in using the credentials provided at the end of the installation script.

---

## Step 5 – Agent Communication & Firewall Considerations

Ensure the following ports are allowed between endpoints and the Wazuh server:

| Port  | Protocol | Purpose             |
| ----- | -------- | ------------------- |
| 1514  | TCP/UDP  | Agent communication |
| 1515  | TCP      | Agent enrollment    |
| 55000 | TCP      | Wazuh API           |
| 443   | TCP      | Dashboard access    |

Firewall rules should follow **least-privilege principles**.

---

## Step 6 – Agent Enrollment (High-Level)

Agents are installed on endpoints and enrolled with the Wazuh Manager.

Typical process:

1. Install agent package (Windows/Linux)
2. Configure manager address
3. Register agent
4. Start agent service

Detailed agent installation steps are documented separately.

---

## Validation Checklist

* Wazuh dashboard accessible
* Manager, indexer, and dashboard services running
* Agent successfully registers
* Security events visible in dashboard

---

## Security Considerations

* Admin dashboard access restricted to management network
* Strong passwords enforced
* Default credentials rotated post-install
* Firewall rules limit agent and API exposure

---

## Operational Notes

* Alert noise reduction requires tuning rules over time
* Windows audit policy configuration significantly impacts visibility
* File integrity monitoring increases storage usage

---

## Future Enhancements

* Custom Wazuh rules and decoders
* Sysmon integration
* MITRE ATT&CK mapping and detection validation
* Automated response actions

---

## Disclaimer

This deployment is for **educational and portfolio demonstration purposes only**. All configurations are sanitized and do not represent a production environment.
