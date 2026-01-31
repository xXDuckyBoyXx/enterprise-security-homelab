# Enterprise-Security-Homelab
A segmented SOC-style homelab using Proxmox, pfSense, Wazuh SIEM, and Windows/Linux endpoints with detections mapped to MITRE ATT&CK.

## Overview

This project is an **enterprise-style security homelab** designed to demonstrate real-world defensive security, networking, and SIEM operations. The lab simulates a small organizational environment using consumer hardware combined with enterprise security tooling, emphasizing **network segmentation, visibility, and detection engineering**.

The homelab is intentionally documented and structured to be **portfolio-ready**, reproducible, and safe to publish publicly.

---

## Objectives

* Simulate an enterprise network using realistic trust boundaries
* Deploy and document a firewall-based segmentation strategy
* Implement centralized logging and security monitoring
* Validate detections mapped to the MITRE ATT&CK framework
* Demonstrate operational documentation and runbook creation

---

## Architecture Summary

The environment is built around a layered network design:

* **Edge / ISP Layer:** Consumer router providing internet access
* **Security Layer:** Firewall enforcing segmentation and policy
* **Internal Network:** Wired and wireless endpoints
* **Monitoring Layer:** Centralized SIEM collecting and analyzing logs

All routing and access control decisions are enforced at the firewall layer.

📁 Full architecture diagrams are located in:
``
docs/diagrams/
``

---

## Network Design

### Network Zones

* **WAN:** Internet-facing connectivity
* **LAN (Trusted):** User and consumer devices
* **Management (Logical):** Security tooling and administrative access

> Logical segmentation is used to mirror enterprise designs without requiring enterprise hardware.

### Connectivity

* Wired and wireless devices are intentionally separated at the logical level
* East–west traffic is restricted where possible
* North–south traffic is explicitly controlled

---

## Devices & Systems

### Endpoints

* Windows Desktop (hardwired)
* ASUS Laptop (WiFi)
* Samsung Smart TV (hardwired)

### Infrastructure

* Proxmox VE (virtualization platform)
* pfSense (firewall and routing)
* Ubuntu Server (Wazuh SIEM)

---

## Security Tooling

### Firewall

* pfSense deployed as the primary firewall
* Default-deny principles applied
* Explicit rules controlling:

  * LAN → WAN
  * Management access
  * Monitoring traffic

📁 Firewall documentation:
``
docs/setup-guides/
``

### SIEM / Monitoring

* **Wazuh** deployed on Ubuntu Server
* Centralized collection of:

  * Windows Security Events
  * Linux authentication and system logs
  * File integrity monitoring
* Dashboards and alerts used to validate detections

---

## Detection Engineering

The lab includes simulated adversary activity to validate alerting and visibility.

Example detections:

* Authentication brute-force attempts
* Privilege escalation events
* Suspicious process execution
* Unauthorized configuration changes

Each detection includes:

* Test method
* Observed logs
* Triggered alerts
* MITRE ATT&CK technique mapping

📁 Detection documentation:
``detections/``

---

## Validation & Testing

* Firewall rules verified via controlled traffic tests
* SIEM ingestion confirmed from all endpoints
* Alerts validated through test activity
* Dashboard visibility reviewed for accuracy and noise

---

## Lessons Learned

* Proper network segmentation significantly limits attack surface
* SIEM effectiveness depends heavily on endpoint configuration
* Documentation is as important as technical implementation
* Alert tuning is an ongoing operational task

---

## Future Enhancements

* Additional network segmentation
* Expanded MITRE ATT&CK coverage
* Automated response actions
* Vulnerability scanning integration
* Improved alert tuning and correlation
* Deploy VPN for access outside network

---

## Disclaimer

This project is for **educational and portfolio demonstration purposes only**. All configurations, diagrams, and data are sanitized and do not represent a production environment.

---

## Author

**Michael Garriott**
Enterprise Security Homelab Project
